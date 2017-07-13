---
layout: post
title: MySql定时任务计划任务
category: 资源
tags: 定时任务,计划
keywords: 定时任务,计划
---

```
[mysqld]
event_scheduler=ON # my.ini打开定时任务

# show variables like '%event_scheduler%'; #查看数值
# SET GLOBAL event_scheduler = 1; #临时开启 重启服务后需重新设置
# 创建语句
CREATE EVENT [IF NOT EXISTS] event_name
ON SCHEDULE schedule
[ON COMPLETION [NOT] PRESERVE] #默认not 我没有发现又什么区别
[ENABLE | DISABLE]
[COMMENT 'comment']
DO sql_statement;
```

```
每秒插入一条数据
USE test;
CREATE TABLE aaa (timeline TIMESTAMP);
CREATE EVENT e_test_insert
ON SCHEDULE EVERY 10 SECOND
on completion not preserve
# DISABLE
DO INSERT INTO test.aaa VALUES(CURRENT_TIMESTAMP);
```


```
5天后执行一次 然后系统会自动清除这个任务
ON SCHEDULE at CURRENT_TIMESTAMP + INTERVAL 5 DAY

2007年7月20日12点整清空test表：
ON SCHEDULE AT TIMESTAMP '2007-07-20 12:00:00'

每天定时清空test表：
ON SCHEDULE EVERY 1 DAY

5天后开启每天定时清空test表
ON SCHEDULE EVERY 1 DAY STARTS CURRENT_TIMESTAMP+ INTERVAL 5 DAY # 1 MONTH
　　
每天定时清空test表，5天后停止执行：
ON SCHEDULE EVERY 1 DAY ENDS CURRENT_TIMESTAMP+ INTERVAL 5 DAY
```


```
ALTER EVENT event_name
[ON SCHEDULE schedule]
[RENAME TOnew_event_name]
[ON COMPLETION [NOT] PRESERVE]
[COMMENT 'comment']
[ENABLE | DISABLE]
[DO sql_statement]


DROP EVENT [IF EXISTS] event_name;

如果在运行中想要临时关闭一下某个任务
alter event `Slave_Monitor` DISABLE;
alter event `Slave_Monitor` ENABLE;
```