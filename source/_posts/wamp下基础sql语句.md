---
title: wamp下基础sql语句
tags: sql语句
categories: MySQL
abbrlink: 34883
date: 2018-11-22 18:47:07
---

### 环境搭建
#### 实验环境：wamp-SQL控制台
<!--more-->
1.	设置MySQL的密码
2.	默认密码为空，直接回车登录
3.	use mysql;
4.	修改密码
```
update user set authentication_string = PASSWORD('你自己的密码') where user='root';
```

5.	使设定立即生效

```
flush privileges; 
```
6.	exit 退出；

### 基础语句
1. 登陆wamp；
2. 查看基本配置
   * 查询服务器版本 select version（）
   * 查询用户权限  select user（） 
   * 查询当前所在的库 select database（）
3. 显示数据库列表  show databases
4. 建库  create database user
5. 建表  use user 
 ```  
 create table （id int username varchar(20)password varchar(20）
 ```
6. 往表中加入记录
```
  insert into admin values(1,'admin','hhh')
```

7. 显示表的字段信息  desc 表名

```
mysql> desc admin;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int(11)     | YES  |     | NULL    |       |
| username | varchar(20) | YES  |     | NULL    |       |
| password | varchar(20) | YES  |     | NULL    |       |
+----------+-------------+------+-----
```

8. 查询操作
* 查询admin中所有数据   select * from 表名;

```
mysql> select * from admin;
+------+----------+----------+
| id   | username | password |
+------+----------+----------+
|    1 | admin    | hhh      |
|    1 | user     | dida     |
|    1 | hack     | zzz      |
|    2 | use      | ida      |
|    3 | hak      | zz       |
+------+----------+----------+
```

（因为手残所以多加了两个id=1的  以后忽略）
* 查询admin中id=2的信息
select * from 表名 where id =2

```
mysql> select * from admin where id =2;
+------+----------+----------+
| id   | username | password |
+------+----------+----------+
|    2 | use      | ida      |
+------+----------+----------+
```

* 查询admin中id=2的用户名和密码 
select username,password from admin where id =2;

```
mysql> select username,password from admin where id =2;
+----------+----------+
| username | password |
+----------+----------+
| use      | ida      |
+----------+----------+

```
9. 判断其他表是否存在

```
select * from admin where id=‘1’and exists(select * from task）
```

如果不存在 会出现Table 'user.task' doesn't exist

```
 mysql> select * from admin where id='2'and exists(select * from task );
ERROR 1146 (42S02): Table 'user.task' doesn't exist
```

#### 一些不常用的
* @@version_compile_os显示服务器系统
* @@basedir   显示MySQL的安装路径
* @@datadir   显示MySQL数据库文件的路径

1. order by n  查字段与排序
```
mysql> select * from admin  order by 4;
ERROR 1054 (42S22): Unknown column '4' in 'order clause'
mysql> select * from admin  order by 3;
+------+----------+----------+
| id   | username | password |
+------+----------+----------+
|    1 | user     | dida     |
|    1 | admin    | hhh      |
|    2 | use      | ida      |
|    3 | hak      | zz       |
|    1 | hack     | zzz      |
+------+----------+--
```

联合查询：前后字段必须一致。
2. 告诉服务器你的字符集

```
mysql>set names gbk/utf-8   
```

10. 快速清空表
truncate 表名
11. distinct 在结果中去除重复行

```
mysql> select distinct name from aaa;
```

12. order by 对结果排序

```
select * from hhh order by id;
```

13. 修改数据表记录

```
mysql> update hhh set age='15' where id='3';
```

14. concat联合多列

```
mysql> select id,concat(name,":",age) from hhh;
```

15. 修改字符编码

```
alter table users modify username char(20) character set gbk;
```

16. 建立索引

```
create unique index <索引名> on <表名> <列名>
```

<!--more-->