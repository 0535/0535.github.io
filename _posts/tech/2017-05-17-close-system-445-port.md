---
layout: post
title: 关闭445端口及修改危险后缀默认打开程序
category: 技术
tags: 445,病毒
keywords: 局域网,445
---

## 批处理关闭445端口

```
@echo off
mode con: cols=85 lines=30
:NSFOCUSXA
title  WannaCry勒索病毒安全加固工具  
color 0A
cls
echo.                   
echo.                      
echo -----------------------  WannaCry勒索病毒安全加固工具  --------------------------
echo.                                                                         
echo.       
echo    * WannaCry勒索软件可加密硬盘文件，受害者必须支付高额赎金才有可能解密恢复，安
echo      全风险高，影响范围广！
echo.                                                                     
echo    * 网络层面：建议边界防火墙阻断445端口的访问，可通过IPS、防火墙相关安全设备配
echo      置相关阻断策略。    
echo.
echo    * 终端层面：暂时关闭Server服务,使用命令"netstat -ano | findstr ":445""，确保
echo      关闭445端口，建议在微软官网下载MS17-010补丁,选择对应的版本进行补丁安装，补
echo      丁下载地址：http://www.catalog.update.microsoft.com/Search.aspx?q=KB4012598。        
echo.     
echo    * 必须以系统管理员身份运行，以下提供此工具所做的操作的介绍：
echo.
echo       1：WIN7加固 2：WIN10加固 3：WIN2003加固 4：WIN2008加固 5：WIN2012加固
echo       6.WIN2016加固          
echo.  
echo       7: 退出                                                              
echo                                                       绿盟科技 V1.3                      
echo                                                      www.nsfocus.com 
echo                                                                  
echo ---------------------------------------------------------------------------------
echo.
set start=
set /p start=    输入(1 2 3 4 5 6)后按回车键:
if "%start%"=="1" goto WIN7
if "%start%"=="2" goto WIN10
if "%start%"=="3" goto WIN2003
if "%start%"=="4" goto WIN2008
if "%start%"=="5" goto WIN2012
if "%start%"=="6" goto WIN2016
if "%start%"=="7" goto quit
goto NSFOCUSXA

:WIN7
net stop server /Y > nul
sc config lanmanserver start= disabled
netsh advfirewall set currentprofile state on > nul
netsh advfirewall firewall add rule name="DenyEquationTCP" dir=in action=block localport=445 remoteip=any protocol=tcp > nul
netsh advfirewall firewall add rule name="DenyEquationUDP" dir=in action=block localport=445 remoteip=any protocol=udp > nul
echo ---------------------------------------------------------------------------------
echo    *  Windows 7系统加固命令执行完毕！
echo .
pause
goto NSFOCUSXA
:WIN10
net stop server > nul
sc config lanmanserver start= disabled
netsh firewall set opmode enable > nul
netsh advfirewall firewall add rule name="DenyEquationTCP" dir=in action=block localport=445 remoteip=any protocol=tcp > nul
netsh advfirewall firewall add rule name="DenyEquationUDP" dir=in action=block localport=445 remoteip=any protocol=udp > nul
echo ---------------------------------------------------------------------------------
echo    *  Windows 10系统加固命令执行完毕！
echo .
pause
goto NSFOCUSXA
:WIN2003
net stop server > nul
net start sharedaccess > nul
sc config lanmanserver start= disabled
netsh firewall add portopening protocol = ALL port = 445 name = DenyEquationTCP mode = DISABLE scope = ALL profile = ALL > nul
echo ---------------------------------------------------------------------------------
echo    *  Windows Server 2003系统加固命令执行完毕！
echo .
pause
goto NSFOCUSXA

:WIN2008
net stop server /Y > nul
sc config lanmanserver start= disabled
netsh advfirewall set currentprofile state on > nul
netsh advfirewall firewall add rule name="DenyEquationTCP" dir=in action=block localport=445 remoteip=any protocol=tcp > nul
netsh advfirewall firewall add rule name="DenyEquationUDP" dir=in action=block localport=445 remoteip=any protocol=udp > nul
echo ---------------------------------------------------------------------------------
echo    *  Windows Server 2008系统加固命令执行完毕！
echo .
pause
goto NSFOCUSXA

:WIN2012
net stop server > nul
net start MpsSvc > nul
sc config lanmanserver start= disabled
netsh advfirewall firewall add rule name="DenyEquationTCP" dir=in action=block localport=445 remoteip=any protocol=tcp > nul
netsh advfirewall firewall add rule name="DenyEquationUDP" dir=in action=block localport=445 remoteip=any protocol=udp > nul
echo ---------------------------------------------------------------------------------
echo    *  Windows Server 2012系统加固命令执行完毕！
echo .
pause
goto NSFOCUSXA
:WIN2016
net stop server > nul
sc config lanmanserver start= disabled
netsh advfirewall firewall add rule name="DenyEquationTCP" dir=in action=block localport=445 remoteip=any protocol=tcp > nul
netsh advfirewall firewall add rule name="DenyEquationUDP" dir=in action=block localport=445 remoteip=any protocol=udp > nul
echo ---------------------------------------------------------------------------------
echo    *  Windows Server 2016系统加固命令执行完毕！
echo .
pause
goto NSFOCUSXA
```




### 验证445端口是否关闭

本机 cmd 窗口执行命令`netstat -ano | findstr ":445"`，回车后无任何返回即关闭成功。

---

### 使用软件关闭445端口

[大鱼端口查看器](http://baoku.360.cn/soft/show/appid/1900007366)

[大鱼端口查看器](http://soft.360.cn/static/baoku/info_7_0/softinfo_1900007366.html)

### 软件恢复445端口

[免疫工具](http://dl.360safe.com/nsa/nsatool.exe)


## 修改危险后缀默认打开程序

在高权限的cmd里执行，将以下后缀的文件默认打开程序变为记事本：

```
ftype JSFile=C:\Windows\System32\Notepad.exe %1
ftype JSEFile=C:\Windows\System32\Notepad.exe %1
ftype VBSFile=C:\Windows\System32\Notepad.exe %1
ftype VBEFile=C:\Windows\System32\Notepad.exe %1
ftype WSFFile=C:\Windows\System32\Notepad.exe %1
ftype WSHFile=C:\Windows\System32\Notepad.exe %1
```