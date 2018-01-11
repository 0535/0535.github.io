---
layout: post
title: Apache下配置域名 端口及虚拟目录
category: 技术
tags: Apache
keywords: Apache,域名,端口,虚拟目录
---

## Apache下实现本机域名访问

### 修改HOSTS文件

文件位置 `C:\Windows\System32\drivers\etc`

![hosts文件添加内容](http://pic.yupoo.com/bztd/GoHgckKL/tFhkP.jpg)

### 修改httpd.conf开启httpd-vhosts.conf

![开启vhosts功能](http://pic.yupoo.com/bztd/GoHgcAMl/UW0TN.jpg)

### 虚拟主机配置

`D:\wamp64\bin\apache\apache2.4.17\conf\extra\httpd-vhosts.conf` 下开启配置：

```
# 保留默认配置
<VirtualHost *:80>
    DocumentRoot "D:/wamp64/www/"
    ServerName localhost
</virtualHost>

# 配置a.com  注意路径是否有权限
<VirtualHost *:80>
    ServerAdmin admin@a.com
    DocumentRoot "D:/wamp64/site/"
    ServerName www.a.com
    ServerAlias a.com
    ErrorLog "logs/a-error.log"
    CustomLog "logs/a-access.log" common
</VirtualHost>

#配置目录权限 如果是www目录下则会自动继承www权限
<Directory "D:/wamp64/site/">
    Options Indexes FollowSymLinks Multiviews
    AllowOverride All
# 允许外部访问    
    Require all granted
# Require local  #只允许本机访问
</Directory>
```

## 配置实现虚拟目录

本案例在 `D:\wamp64\alias` 下新增 `a.conf`，可实现 `http://localhost/a` 的访问，文件内容如下：

```
Alias /a "D:/site/"

# 配置目录权限
<Directory "D:/site/">
    Options Indexes FollowSymLinks
    AllowOverride all
    Require all granted
</Directory>
```

## 开启外网访问 （Apache2.4需要开启）

将 `httpd.conf` 中 `Directory` 的 `Require all denied`、`Require local` 换成 `Require all granted` 即可。

```
<Directory />
    AllowOverride ALL
#    Require all denied
	Require all granted
</Directory>


<Directory "D:/wamp64/www/">
    Options Indexes FollowSymLinks
    AllowOverride all
#   onlineoffline tag - don't remove
#    Require local
    Require all granted
</Directory>
```

虚拟目录 `http://localhost/phpmyadmin` 如果需要外网访问可以修改 `phpmyadmin.conf`。

## 开启基于端口的访问

`http.conf` 中添加如下代码
```
Listen 0.0.0.0:90
Listen [::0]:90
```

其次，需要设置好虚拟主机配置中的端口。