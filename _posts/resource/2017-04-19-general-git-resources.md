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
git checkout -b master develop #创建并切换到develop分支
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
