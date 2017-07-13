---
layout: post
title: MySQL 常用资源
category: 资源
tags: MySQL
keywords: MySQL
---

创建数据库编码格式`utf8_general_ci`

## 常用命令

```
show databases/tables; #显示数据库/表
use test; #使用test数据库
desc tabl_name; #查询表结构
show create table table_name; #显示创建的语句
select * from mysql.event \G #查看定时任务
```

## 登录数据库

```
mysql -h localhost -uroot -p
```

## 修改密码

```
SET PASSWORD = PASSWORD("123456"); # 修改当前用户密码
SET PASSWORD FOR 'root'@'%' = PASSWORD("123456"); # 修改其他用户密码
```

## 导出数据库

```
mysqldump -uroot -p db > db.sql
```

## 导入数据库

```
mysqldump -uroot -p db < db.sql
```

## 创建用户

```
CREATE USER 'test'@'localhost' IDENTIFIED BY '123456'; # 任意主机% 指定主机192.168.1.10
grant all privileges on *.* to test@'localhost'; # 授予所有权限及所有数据库
GRANT SELECT,INSERT ON Typecho.tablename TO 'test'@'localhost'; #授予部分权限
```

## 创建表

```
CREATE SCHEMA testdb DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```

## 赋予数据库权限

```
GRANT ALL ON testdb.* TO 'test'@'localhost';
```

