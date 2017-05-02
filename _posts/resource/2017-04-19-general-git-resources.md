---
layout: post
title: Git 常用资源
category: 资源
tags: Git
keywords: Git
---

## 克隆库

```
git clone https://github.com/abc.git
git clone --depth=1 https://github.com/abc.git #只抓取最近的一次commit
```

## 取消文件的修改

```
git checkout -- a.php #取消单个文件
git checkout -- #取消所有文件的修改 
```

## 删除文件

```
git rm a.php #直接删除文件
git rm --cached a.php #删除文件的暂存状态
```


# 分支管理

## 创建分支

```
git branch develop # 只创建分支
#git checkout -b master develop #创建并切换到develop分支
git checkout -b develop #检查develop分支是否存在，不存在就创建并切换过去
```

## 合并分支
```
git checkout master #切换到master分支
git merge --no-ff develop #把 develop 合并到 master 分支，no-ff 选项的作用是保留原分支记录
git rebase develop # rebase 当前分支到 develop
git branch -d develop # 删除 develop 分支
```

## 克隆远程分支

```
git branch -r # 显示所有分支，包含远程分支
git checkout origin/android
```

## TAG 操作

```
git tag # 查看tag
git tag -a v1.0-m 'first version' # 创建tag
git tag -d v1.0 # 删除tag
git push origin --tags #共享tag

git checkout -f v1.0 #切换到TAG

根据 TAG 创建分支
git branch newbranch v1.0 # 根据 TAG 创建新分支
git checkout newbranch # 切换到新分支
git push origin newbranch # 把本地创建的分支提交到远程仓库
```


# Git 设置

## 设置 commit 的用户和邮箱
```
git config user.name "xx"
git config user.email "xx@xx.com"
```
## push命令不再需要密码

已有项目.git目录下的config文件中的配置
```
[remote "origin"]
    url = git@github.com:suyan/suyan.github.io.git
    fetch = +refs/heads/*:refs/remotes/origin/*
```

相关链接：

[Git 根据tag创建分支](http://blog.csdn.net/lhcxwjh/article/details/51083249)
[github创建tag](http://caibaojian.com/github-create-tag.html)