---
title: git learning day 2
date: 2016-08-24 11:07:57
tags: git 
categories: 学习笔记
---
## Git基础

### 撤销操作(昨天没看懂的地方，没细心看。。。)

一次提交过程，漏了几个文件未提交，此时可以运行带有`--amend`选修的提交命令

```bash
#某一次commit
$ git commit -m 'initial commit'
#补上之前未git add 的文件
$ git add forgotten_file
#直接进行下面操作，则将这些文件提交到该次commit,不需要-m
$ git commit --amend
```
*最终只会有一个提交结果，第二次提交将代替第一次提交*

#### 取消暂存的文件

某一次执行`git add`时不小心多添加几个文件到暂存区去，如何取消这几个文件？

```bash
#下面假设add了所有文件到暂存区
$ git add *
#查看文件状态
$ git status
#假设要取消README文件,使用git reset
$ git reset HEAD README
#其中HEAD是当前分支引用的指针，它指向该分支上的最后一次提交，这表示HEAD
#将是下一次提交的父节点。即可以将其看作你的上一次提交的快照
```

#### 撤销对文件的修改
想对一个已修改文件，将其还原成上次提交的样子，`git status`会提示你如何做,即使用`git checkout -- <file> ...`,

```bash
$ vim README
$ git status
$ git checkout -- README
$ git status
```

*你需要知道*`git checkout -- [file]`*是一个危险的命令*，这很重要。 你对那个文件做的任何修改都会消失 - 你只是拷贝了另一个文件来覆盖它。 除非你确实清楚不想要那个文件了，否则不要使用这个命令。
如果你仍然想保留对那个文件做出的修改，但是现在仍然需要撤消，将会在 *Git 分支*部分 介绍保存进度与分支；这些通常是更好的做法。
在git中任何*已提交的*东西总是可以恢复的。然而，你任何未提交的东西丢失后很可能再也找不回来。

## Git分支

*Git的分支很重要*,是Git区分其他版本控制系统的一个重要原因。

### 分支简介

在进行提交操作时，Git会保存一个提交对象（commit object）。该对象包括一个指向暂存内容快照的指针，作者的姓名、邮箱，和提交时所输入的信息，以及一个指向其父对象的指针。首次提交没有父对象，普通提交操作产生一个父对象，而*由多个分支合并产生的提交对象有多个父对象*。

```bash
#假设一个工作目录有三个文件分别为L,B,J，进行暂存操作，该过程会对每个文件计算一个校验和，
#然后把当前版本的文件快照报错到Git仓库中（Git使用blob对象来保存），最终将校验和加入到暂存区域等待提交：
$ git add L B J
$ git commit -m 'The initial commit of my project'
[master (root-commit) 27b7e34] The initial commit of my project
 3 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 L
 create mode 100644 B
 create mode 100644 J
```
1. 现在Git 仓库中有五个对象：三个 blob 对象（保存着文件快照）、一个树对象（记录着目录结构和 blob 对象索引）以及一个提交对象（包含着指向前述树对象的指针和所有提交信息）。
2. 然后做些修改后再次提交，那么这次产生的提交对象会包含一个指向上次提交对象（父对象）的指针。
3. Git 的分支，其实本质上仅仅是指向提交对象的可变指针。 Git 的默认分支名字是 master。 在多次提交操作之后，你其实已经有一个指向最后那个提交对象的 master 分支。 它会在每次的提交操作中自动向前移动。
*Git 的 “master” 分支并不是一个特殊分支。* 它就跟其它分支完全没有区别。 之所以几乎每一个仓库都有 master 分支，是因为 git init 命令默认创建它，并且大多数人都懒得去改动它。

#### 分支创建与查看

```bash
#创建一个名称为testing分支，新创建的分支会在当前的提交对象上创建一个指针
$ git branch testing
#可以通过git log命令查看各个分支所指的对象
$ git log --online --decorate
```

#### 分支切换

```bash
# git checkout <branch>来切换（ps. git checkout --<file> 用来撤销对文件的修改，不过一般不用，太危险了），加一个-b可以直接创建并切换到该分支
$ git checkout testing
Switched to branch 'testing'
#这样HEAD就指向testing分支了
$ vim B
$ git commit -a -m 'made a change'
$ git log --online --decorate
be33a7d (HEAD -> testing) made a change
27b7e34 (master) The initial commit of my project
#切换到master分支
$ git checkout master
#该命令做了两件事，一是使HEAD指向master分支，二是将工作目录恢复成master分支所指向的快照内容，也就是说现在你修改的话，将相对于一个较旧的版本
#现在在master分支上改变B文件
$ vim B
$ git commit -a -m 'made a change'
#通过下面指令输出提交历史、各个分支的指向以及项目分支交叉情况
$ git log --oneline  --decorate --graph --all
* 084ec94 (HEAD -> master) made a other changes
| * be33a7d (testing) made a change
|/
* 27b7e34 The initial commit of my project
```

由于 Git 的分支实质上仅是包含所指对象校验和（长度为 40 的 SHA-1 值字符串）的文件，所以它的*创建和销毁都异常高效。 创建一个新分支就像是往一个文件中写入 41 个字节（40 个字符和 1 个换行符），如此的简单能不快吗？

### 分支的合并

#### 普通合并

#### 遇到冲突合并

```bash
$ git merge testing
Auto-merging B
CONFLICT (content): Merge conflict in READE
Automatic merge failed; fix conflicts and then commit the result.
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   READE

no changes added to commit (use "git add" and/or "git commit -a")
#使用图形化工具来解决冲突，你可以运行git mergetool
$ git mergetool
```

