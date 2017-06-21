---
layout: post
title: win10安全模式及常用操作
category: 技术
tags: 安全模式
keywords: WIN10,安全模式
---

## 进入安全模式

### shift+重启 首选

![关机重启](http://pic.yupoo.com/bztd/gTZeDmIH/abc06421.jpg)

### 更新和安全--恢复--立即重启

![高级启动](http://pic.yupoo.com/bztd/gTZeDpxd/161e1679.jpg)

### 系统配置

![系统配置](http://pic.yupoo.com/bztd/gTZeDr9n/4941fbbb.jpg)

### 此法未用过

win10光盘进入安装界面  shift+F10 进入win+X+A命令行
bcdedit /set {default} bootmenupolicy legacy
恢复默认
bcdedit /set {default} bootmenupolicy standard


## 系统引导记录

```
:备份原有的系统引导记录到 F:\BACK\bcd
bcdedit /export F:\BACK\bcd
:记录文件信息导入到系统引导记录
bcdedit /import F:\BACK\bcd
:设置等待时间为1秒
bcdedit /timeout 1
```

## 系统文件

备份`C:\Windows\System32\config`

## 查看系统版本

运行`winver` 或者 `dxdiag` 

## 关于用户

运行`netplwiz` 、 `compmgmt.msc`、`lusrmgr.msc`

PowerShell禁用用户`net user username /active:no`

## 神奇的服务必须开启

`Windows Firewall` && `Windows Update` 关系到Microsoft账户、应用商店、搜索功能。。。

## 还有一招

重新新建管理员账户