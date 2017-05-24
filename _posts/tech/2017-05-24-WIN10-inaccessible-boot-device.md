---
layout: post
title: WIN10开机INACCESSIBLE_BOOT_DEVICE解决办法
category: 技术
tags: INACCESSIBLE
keywords: WIN10,INACCESSIBLE
---

WIN10出现的蓝屏，INACCESSIBLE_BOOT_DEVICE，开不了机。

![Win10蓝屏](http://pic.yupoo.com/bztd/gT4lvH0h/64c78674.jpg)

可以进入安全模式的，可以进去禁用显卡。[参考资料](http://jingyan.baidu.com/article/ff411625b02f1b12e482379e.html)


安全模式进不去的，使用文件`Windows\System32\config\RegBack\SYSTEM`替换`Windows\System32\config\SYSTEM`。[参考资料](http://jingyan.baidu.com/article/454316ab681d03f7a6c03a54.html)


