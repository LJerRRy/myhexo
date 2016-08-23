---
title: gitlearn
date: 2016-08-23 19:00:22
tags: git
categories: github
---
## git起步
### 配置

    #配置 用户名，邮箱
    $ git config --global user.name "Jerry"
    $ git config --global user.email 20121954@cqu.edu.cn
    #检查配置信息
    $ git config --list

### 帮助手册命令

    #三种方法找到git使用手册
    $ git help <verb>
    $ git <verb> --help
    $ man git -<verb>
    #例如，想获得config命令的手册
    $ git help config
    $ git config --help
    $ man git -config


## git基础

    #初始存在的一个仓库
    $ git init
    #指定所有文件的跟踪，也可以指定一些文件
    $ git add *
    #将跟踪文件提交
    $ git commit -m 'initial project version'


