---
title: mysql8.0的安装
tags: MySQL
categories: MySQL
abbrlink: 30461
date: 2018-10-02 14:43:26
---

### Windows下MySQL安装
## 今天闲来无事，就脑残的想安装个MySQL玩玩，结果遇到了各种各样的麻烦，搞得心态差点炸了，还好最后安装完了。
## 1.官网下载社区版MySQL（zip包），然后解压。
## 2.配置环境变量。
<!--more-->
我的电脑->右键->高级系统设置->环境变量，在系统变量的path后添加解压后的MySQL文件夹里的bin目录的路径
## 3.添加配置文件

在MySQL文件夹下创建my.ini文件
```
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[mysqld]
# 设置3306端口
port = 3306
# 设置mysql的安装目录
basedir=C:\web\mysql-8.0.11
# 设置mysql数据库的数据的存放目录
datadir=C:\web\sqldata
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
```
## 4.以管理员身份运行cmd（在搜索框敲cmd，右键，以管理员身份运行）
这里一定一定要用管理员身份运行cmd，不然在后续步骤时会报错
进入cmd后切到bin目录下，初始化数据库
```
mysqld --initialize --console
```
待执行完成后，会出现root的初始密码
root@localhost后面的字符串就是密码
记住密码，保存下来，之后第一次登陆时会用到。
## 5.安装mysqld
```
mysqld -install
```
## 6.启动MySQL
```
net start mysql
```
这里就是上文提到的如果不是管理员身份运行，会提示安装失败。
## 7.上述步骤完成后，就不需要管理员权限了，直接cmd
```
mysql -u root -p
```
回车后会提示输入密码，把刚才保存的输入密码输入之后就可以登录了
## 8.修改密码
因为初始密码过于难记，所以大部分人都需要重置密码，重置密码有很多种方法，我试了很多，只有下面这条能用
```
alter user 'root'@'localhost' identified by '你的密码';
```
其他的都会报错，这里一定要有耐心，因为我不知道试了多少语句。
## 9.刷新，使修改生效
```
flush privileges;
```
## 10.退出，重新登陆MySQL
退出mysql
```
exit
```
重新登陆MySQL
```
mysql -u root -p
```
然后输入你修改后的密码，发现能够登陆，MySQL安装完成

# 附：mysql的导入导出
## 1.导入：
   * 运行cmd
   * mysql -u 用户名 -p 密码
   * source 数据库名 < 要导入的文件名.sql
## 2.导出：
   * 到MySQL的bin目录下，运行cmd
   * 输入 mysqldump 数据库名 > 文件名.sql。如果要指定路径，例如如果想放到C盘下，可以直接 mysqldump 数据库名 >  c:\\文件名.sql
## 当然还有一种更简单的方法，就是直接用图形化界面，直接导出。
<!--more-->