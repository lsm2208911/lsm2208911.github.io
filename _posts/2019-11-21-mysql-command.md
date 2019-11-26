---
layout:     post
title:      "mysql常用命令"
published: false
subtitle:   "世界没有难用的工具"
date:       2019-11-21
author:     "无力去闹"
header-img: "img/post-bg-js-version.jpg"
tags:
    - MYSQL
---
## 登录mysql
### windows登录
`mysql.exe -h127.0.0.1 -uroot -P3306 -p`
### linux登录
`mysql -h127.0.0.1 -uroot -P3306 -p`
## mysql常用命令
### 查看数据库与表结构
```
mysql> show databases;  #查看mysql数据库
mysql> use test; #切换到test数据库
mysql> show tables; #查看数据库中的所有表
mysql> desc t_user; 查看t_user表结构
```
### 数据相关操作
### 创建表
### 插入数据
`insert into user(id,name,age) values(1,'zhangsan',12);`
