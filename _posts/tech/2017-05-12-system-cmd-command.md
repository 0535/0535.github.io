---
layout: post
title: windows系统常用命令cmd
category: 技术
tags: 自动关机,用户管理
keywords: 用户,shutdown,自动关机,定时
---
## 管理命令

```
lusrmgr.msc :本地用户和组
NETSH WINSOCK RESET :网络参数重置

dxdiag :DirectX诊断工具
winver #查看系统版本
slmgr /dlv:系统版本
certmgr.msc :证书管理工具
```

## 端口 进程
```
查看指定端口的占用情况
netstat -aon|findstr "9050"
查看PID对应的进程 
C:\>tasklist | findstr "2016" 
结束该进程 
C:\>taskkill /f /t /im tor.exe  
```

## 命令配置IP网关DNS地址
```
@ ECHO OFF
color 17
mode con cols=40 lines=20
title 自动----程序
@ ECHO.
@ ECHO. 說明
@ ECHO -----------------------------------------------------
@ ECHO 此命令將自動更改ip
@ ECHO 172.16.8.x
@ ECHO -----------------------------------------------------
rem 设置变量
set Nic=WLAN
set dns1=202.102.128.68
set dns2=219.147.1.66
:IP地址自动获取
netsh interface ip set address name=%Nic% source=dhcp
:固定IP + 网关
:netsh interface ip add address %Nic% 172.18.10.10 255.255.255.0 gateway=172.18.10.250
netsh interface ip set address name=%Nic% source=static addr=172.18.10.1 mask=255.255.255.0 gateway=172.18.10.250
:DNS自动获取
netsh interface ip set dns name=%Nic% source=dhcp
:多个DNS
netsh interface ip set dns name=%Nic% source=static addr=%dns1% register=PRIMARY >nul
netsh interface ip add dns name=%Nic% addr=%dns2% index=2 >nul
:单个DNS
:netsh interface ip set dns name=%Nic% source=static addr=%dns1% register=PRIMARY >nul
:禁用网卡
:netsh interface set interface %Nic% disabled
:ping /n 3 127.1>nul
@ ECHO ON
@ ECHO IP已設置
@ ECHO OFF
PAUSE
EXIT
```

## Hash校验

`certutil -hashfile Ethereum-Wallet-installer-0-10-0.exe sha256 :md5 sha1`

## 其他常用
```
清楚共享访问记录
net use * /delete
强制注册表更新组策略
gpupdate /force
```

## Win共享

```
netplwiz 网络用户登录向导net person login wizard 或者 control userpasswords2
用户--要使用本计算机 用户必须输入用户名和密码[可以设置开机免输密码]
高级--管理密码--凭据管理器[control keymgr.dll共享保存的账户密码]
共享
net use Z: \\10.128.10.231 123456 /user:admin
net use z: \\IP\c$ "密码" /user:"帐号" #将对方的c盘映射为自己的z盘  
net use \\IP\ipc$ /del #删除与指定IP的IPC$连接  
net use z: /del #删除本机映射的z盘  
net use * /del #删除本机所有映射和IPC$连接  
net use /persistent:yes #控制持久网络连接的使用
```

## 主板生产日期

```
debug
-d ffff:5 格式:月日年
```
## 系统自动关机，重启–利用at及shutdown命令

每月的1、5号的0点自动关机

`at 00:00 /every:1,5 shutdown /f /s /t 0`

每周一的16:50自动关机

`at 16:50 /every:Monday shutdown /f /s /t 0`

每天16:50自动关机

`at 16:50 /every:Sunday,Monday,Tuesday,Wednesday,Thursday,Friday,Saturday shutdown /f /s /t 0`

服务器版的定时关机命令
`at 21:00 /every:Sunday,Monday,Tuesday,Wednesday,Thursday,Friday,Saturday shutdown -p`


取消定时计划的话，命令行中先用`at`查看作业号，然后`at 1 /delete`删除相应作业。 


另外，在倒计时过程输入`shutdown /a`可以取消关机或重启，不加`/t`参数执行则倒计时30秒。


