---
layout: post
title: 优酷路由宝刷机过程
category: 其他
tags: 优酷路由宝
keywords: 优酷路由宝
---

## 刷入具有root权限的固件

本次使用`YKL1_2.1.0613.8617.bin`

## 刷入breed

```
telnet 192.168.11.1
mtd unlock Bootloader #返回unlocking bootloader 证明成功了
mtd -r write /mnt/sda1/breed-youku.bin Bootloader
#或者 wget https://breed.hackpascal.net/breed-mt7620-youku-yk1.bin #下载breed文件
```

![刷入breed](https://pic.yupoo.com/bztd/c1bd93f0/f96c13be.jpg)

## 刷固件

### 进入恢复控制台

进入breed方法：路由断电后一直按住reset键，后插电，led灯全闪完成后，松开reset键，输入网址`192.168.1.1`进入Breed管理界面

![登陆Breed](https://pic.yupoo.com/bztd/e18e772e/afeea40a.jpg)

[固件地址](http://www.right.com.cn/forum/thread-161324-1-1.html)

### 更新固件

![更新固件](https://pic.yupoo.com/bztd/4ab3e119/3566b964.jpg)

```
固件更新完成后的管理信息
固件地址 http://my.router/ 或者 192.168.123.1
管理账号：admin/admin
wifi:1234567890
```
---
相关链接：

[刷机使用的文件](https://pan.baidu.com/s/1geFkF3H)