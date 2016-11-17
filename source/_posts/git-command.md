---
title: Git命令总结备忘
date: 2016-11-16 06:56:43
tags:
	- git
	- 备忘
---

Git——著名的开源分布式版本控制系统，2005年由林纳斯发明，最早用于管理linux内核代码。

# 常用命令
## 创建新仓库
```
mkdir dirname
cd dirname
git init
```

<!-- more -->

## 克隆仓库
克隆一个本地仓库
> git clone /path/to/repository

克隆一个远端仓库
> git clone username@host:/path/to/repository

举个从github克隆的例子
> git clone https://github.com/username/repository.git

# 工作流
本地仓库主要由三部分组成

| ** workspcae **  | 工作目录是仓库内文件的实际位置 |
| :-------: | :--------: |
| ** Index  ** | ** 类似于缓存，临时保存文件改动 ** |
| ** HEAD ** | ** 指向最后一次提交提交结果 ** |

# 添加和提交
每当有文件更改,可以添加到Index:
> git add filename

修改文件太多可以用以下命令查看当前分支与远端分支的差异:
> git status

提交改动到HEAD:
> git commit -m "改动信息"

此时本地更改还没有提交到远端仓库

# 推送改动
用如下命令把改动提交到远端仓库:
> git push origin master

此处master可以改成任何想推送的分支

# 分支
分支是用来将特性开发绝缘开来的。在创建仓库的时候，master 是默认分支。先在其他分支上进行开发，完成后再将它们合并到主分支上。
创建一个叫`test`的分支，并切换过去:
> git checkout -b test

切换回主分支:
> git checkout master

如果新建的分支不需要了，删掉:
> git branch -d test

# 更新与合并
从远端下载并合并到本地仓库:
> git pull

但是这样是不安全的，最好把pull拆分成fetch和merge两部分
> git fetch

从远端仓库下载

> git merge <branch>

合并仓库
合并仓库时把任意分支的内容合并到当前分支合并之前可以用以下命令先查看当前分支和要合并进来的分支有何区别:
> git diff <branch>

