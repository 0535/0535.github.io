---
layout: post
title: 系统自动关机，重启–利用at及shutdown命令
category: 技术
tags: 自动关机
keywords: shutdown,自动关机,定时
---

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


