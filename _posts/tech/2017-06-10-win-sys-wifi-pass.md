---
layout: post
title: Windows查看已保存的WIFI密码
category: 技术
tags: wifi
keywords: wifi
---

![Windows查看WIFI密码](http://pic.yupoo.com/bztd/gV5nFNLU/7c9bec41.jpg)

## 查看WIFI名称
`netsh wlan show profiles`

## 查询密码
`netsh wlan show profiles 无线名称 key=clear | findstr "关键内容"`
