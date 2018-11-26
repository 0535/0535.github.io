---
layout: post
title: Pages 静态网站总结
category: 资源
tags: Git
keywords: Git
---

## 宽带接入

```
ifconfig eth0 up
pppoeconf 之后一路Yes
启动 pon dsl-provider
断开 poff dsl-provider
```

##

```
设置静态IP
gpedit /etc/network/interfaces
# 动态DHCP
auto eth0
iface eth0 inet dhcp
# 静态ip有关的参数
auto eth0
iface eth0 inet static
address 192.168.0.10
netmask 255.255.255.0
gateway 192.168.0.1

gpedit /etc/resolv.conf
#添加DNS
nameserver 1.2.4.8
nameserver 114.114.114.110
启用新设置
/etc/init.d/networking restart
或者
sudo ifdown eth0
sudo ifup eth0 
```

## 删除无用的软件

```
dpkg -l :显示软件列表
apt-get remove noise audience //复制
sudo apt-get remove capnet-assist midori-granite scratch-text-editor

```

##安装输入法

```
apt-get install fcitx-table-wbpy
```

## Linux Windows时间同步问题 Linux不使用UTC

```
sudo gedit /etc/default/rcS utc=yes
```

## 启动等待时间

```
chmod +w /boot/grub/grub.cfg
/boot/grub/grub.cfg  set timeout=10的改为1
gedit /etc/default/grub 修改时间，要不经常恢复成10秒
update-grub
```

## 备份源文件

```
sudo -i
apt-get install gedit
cd /etc/apt
cp sources.list sources.list_backup
gedit source.list
sudo apt-get update
sudo apt-get upgrade
```

