---
title: git learning day 1
date: 2016-08-23 19:00:22
tags: git
categories: 学习笔记
---
## git起步
### 配置
```bash
    #配置 用户名，邮箱
    $ git config --global user.name "Jerry"
    $ git config --global user.email 20121954@cqu.edu.cn
    #检查配置信息
    $ git config --list
```
### 帮助手册命令
```bash
    #三种方法找到git使用手册
    $ git help <verb>
    $ git <verb> --help
    $ man git -<verb>
    #例如，想获得config命令的手册
    $ git help config
    $ git config --help
    $ man git -config
```

## git基础
### 获取一个仓库
初始化一个存在的仓库
```bash
    #初始存在的一个仓库
    $ git init
    #指定所有文件的跟踪，也可以指定一些文件
    $ git add *
    #将跟踪文件提交
    $ git commit -m 'initial project version'
```
克隆一个git仓库
```bash
    #git clone + 路径（则生成一个仓库名的文件夹，里面为仓库的数据）
    $ git clone https://github.com/LJerRRy/Hadoop.git
    #git clone + 路径 + 名称（自己命名的）
    $ git clone https://github.com/LJerRRy/Hadoop.git myhadoop
    #上述是使用https协议，也可以ssh传输协议的
```
### 文件操作
检查文件状态
```bash
    #文件状态 已跟踪或未跟踪
    #已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，
    #在工作一段时间后，它们的状态可能处于未修改，已修改或已放入暂存区（staged）。 
    $ git status
    $ echo 'My World' > README
    #将新建文件跟踪，或者暂存已修改文件
    $ git add README
    #状态简览
    $ git status -s
    #git diff 查看未暂存(unstaged)文件*具体*修改情况
    $ git diff
    #git diff --staged查看已暂存文件修改情况==git diff --cached
    $ git diff --staged
```
忽略文件（无需git管理的文件）
```bash
   #新建一个.gitignore文件，然后列出要忽然的文件模式
    $ echo "*.log" >> .gitignore
    #上面表示将.log文件忽略
```
提交更新
```bash
    #直接用git commit 会启动文本编辑器以便输入本次提交的说明。
    $ git commit
    #直接提交并设置本次跟新的说明
    $ git commit -m "此次更新的说明"
    #使用git commit -a git会自动把所有已经跟踪的文件暂存起来并一起提交，跳过git add步骤
    $ git commit -a -m
```
移除文件
```bash
    #rm README.md从暂存文件中移除，只是简单地从工作目录中手工删除文件
    $ rm README.md
    #git rm README.md从git中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。
    $ git rm README.md
    # 如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f
    $ git rm -f README.md
    #从暂存区删除
    $ git rm --cached README
```
移动文件（重命名文件）
```bash
    $ git mv file_from file_to
    #上面一句话等价于下面三句话
    $ mv file_from file_to
    $ git rm file_from
    $ git add file_to
```
### 查看提交历史
```bash
    #git log会按提交时间列出所有的更新，最近的更新排在最上面。
    $ git log
    #git log 有许多选项可以帮助你搜寻你所要找的提交， 接下来我们介绍些最常用的。
    #一个常用的选项是 -p，用来显示每次提交的内容差异。 你也可以加上 -2 来仅显示最近两次提交
    $ git log -p -2
    #你想看到每次提交的简略的统计信息，你可以使用 --stat 选项：
    $ git log --stat
    #--pretty选项可以指定使用不同于默认格式的方式展示提交历史
    #用oneline将每个提交放在一行显示，查看的提交数很大时非常有用
```
### 撤销操作
看不懂！！！

### 远程仓库的使用
#### 查看远程仓库
```bash
    $ git clone  https://github.com/LJerRRy/myhexo.git
    $ cd myhexo
    #git remote是获取给你克隆仓库服务器的默认名称
    $ git remote
    #可以指定选项-v，显示读写远程仓库使用的Git报错的简写和其对应的URL
    $ git remote -v
    #查看远程仓库
    $ git remote show origin
```
#### 添加远程仓库  
```bash
    #运行git remote add <shortname> <url>添加一个新的远程 Git 仓库，同时指定一个你可以轻松引用的简写：
    $ git remote add pb https://github.com/LJerRRy/myhexo.git
    $ git remote -v
    #现在你可以在命令行中使用字符串 pb 来代替整个 URL。
    #如果你想拉取 Paul 的仓库中有但你没有的信息，可以运行git fetch pb：
    $ git fetch pb
    #当你想分享你的项目时，必须将其推送到上游。
    #这个命令很简单：git push [remote-name] [branch-name]。
    $ git push origin master
#### 远程仓库的移除与重命名
    $ git remote rename pb paul
    $ git remote rm paul
```