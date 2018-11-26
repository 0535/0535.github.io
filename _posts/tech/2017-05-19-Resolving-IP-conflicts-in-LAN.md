---
layout: post
title: 解决局域网中的IP冲突&修改网络连接中的名称&无线网络显示名称
category: 技术
tags: IP冲突
keywords: 局域网,IP冲突
---

## 解决局域网中的IP冲突

第一 可以“安抚”系统服务，来巧妙地将本地连接图标隐藏起来。 
“services.msc”–“Plug and play”服务设置为“禁止”   

第二 反注册网络连接图标的方法。

```
regsvr32 Netcfgx.dll /u
regsvr32 Netman.dll /u
regsvr32 Netshell.dll /u
:regsvr32 Netcfgx.dll 就会恢复Netcfgx.dll
```
如此一来本地连接图标就会被自动隐藏起来了，非法用户自然也就没有办法进入网络参数设置窗口，进行胡乱更改IP地址操作了。

第三 可以修改本地系统组策略，禁止非法用户随意访问网络连接属性。  
 “gpedit.msc”–“用户配置”、“管理模板”、“网络”、“网络连接”–“禁止访问lan连接组件的属性”组策略选项，–选中其中的“已启用”选项，再单击“确定”按钮。

## 修改网络连接中显示的名称

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles`找下面各项右边的`ProfileName`即可

## 无线网络显示名称

`C:\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces`中文件的name字段

忘记网络：搜索更改WLAN设置-管理已知网络
