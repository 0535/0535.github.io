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
show tables like 'tt_%'; #搜索类似表
use test; #使用test数据库
desc tabl_name; #查询表结构
show create table table_name; #显示创建的语句
select * from mysql.event \G #查看定时任务
通配符 name like '王%';name not like 'DB\_%' escape '\' ;%任意长度 _单字符
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

## 数据库批量导出到新表

```
-- 导入到 cmf_portal_post中
INSERT INTO `cmf_portal_post` (`parent_id`, `post_type`) select `parent_id`, `post_type` from zy_1_news where id > 127;
-- 将文章content写入表
update `cmf_portal_post`,`zy_news` set `cmf_portal_post`.post_content=`zy_news`.content where zy_news.id>128 and  cmf_portal_post.id = zy_news.id-90
-- 拼接得到需要的内容
set @front = '{"thumbnail":"';
set @last ='","template":""}';
select @img:=`more` from cmf_portal_post where id = 37;
set @myimg=concat(@front,@img,@last);
update `cmf_portal_post` set `cmf_portal_post`.more= @myimg where id = 37;
-- 使用存储过程 游标循环数据并处理
DELIMITER // 
USE `thinkcmf5`;
DROP PROCEDURE IF EXISTS `my_procedure`;
create procedure my_procedure() -- 创建存储过程  
begin -- 开始存储过程  
declare temp_text text; -- 自定义变量1
declare my_text text; -- 自定义接收得到的变量
declare my_id int; -- 自定义接收得到的变量
DECLARE done INT DEFAULT FALSE; -- 自定义控制游标循环变量,默认false  
  
DECLARE My_Cursor CURSOR FOR ( SELECT id,more FROM cmf_portal_post where id>37 ); -- 定义游标并输入结果集  
DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE; -- 绑定控制变量到游标,游标循环结束自动转true  
  
OPEN My_Cursor; -- 打开游标  
  myLoop: LOOP -- 开始循环体,myLoop为自定义循环名,结束循环时用到  
    FETCH My_Cursor into my_id,my_text; -- 将游标当前读取行的数据顺序赋予自定义变量id text 
    IF done THEN -- 判断是否继续循环  
      LEAVE myLoop; -- 结束循环  
    END IF;
    IF my_text='' THEN -- 变量加以处理
      SET temp_text = my_text;
    ELSE
      SET temp_text = concat('{"thumbnail":"',my_text,'","template":""}');
    END IF ;
    -- 自己要做的事情,在 sql 中直接使用自定义变量即可  
    -- UPDATE t_user SET c_name = my_name WHERE id = my_id and rtrim(ltrim(c_name)) = ''; -- 左右去空格  
    -- COMMIT; -- 提交事务  
	-- select temp_text; -- 查看变量
	update `cmf_portal_post` set `cmf_portal_post`.more= temp_text where id = my_id;
  END LOOP myLoop; -- 结束自定义循环体  
  CLOSE My_Cursor; -- 关闭游标  
END; -- 结束存储过程  
//
delimiter ; -- 恢复默认的delimiter
-- sql 执行存储过程  
call my_procedure();
-- sql 删除存储过程  
drop procedure my_procedure;  

-- 触发器
delimiter $
create trigger tg1
after insert on o -- 表o
for each row -- 这句话在mysql是固定的
begin
update g set num=num-new.much where id =new.gid;
end$
insert into o(gid,much) values(2,3)$
```
