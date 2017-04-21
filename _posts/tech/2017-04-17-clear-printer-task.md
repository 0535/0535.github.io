---
layout: post
title: 怎么样清除无法删除的打印机任务
category: 技术
tags: 打印机
keywords: 打印机
---

打印机任务经常会出现一些无法删除的任务，导致后面的打印任务无法进行；或者打印了一些文件，又不想要了，无法正常取消这些打印任务。这些问题工作也经常遇到，我是使用下面的方法解决的，做篇经验和大家分享下。

## 批处理解决

```
@echo off
echo 计划任务开始执行 
echo 停止打印服务
net stop Spooler
echo 清理打印暂存
del /s /q /f %windir%\System32\spool\PRINTERS\*.*
echo 重新启动打印服务
net start Spooler
echo 完成!!!!(5秒后自动关闭)
ping -n 5 127.0.0.1>nul
exit
```

“运行”中输入 spool 可快速打开 C:\Windows\System32\spool 目录。