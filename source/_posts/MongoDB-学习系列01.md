---
title: MongoDB学习系列01
date: 2019-03-25 21:40:30
categories: 
    - 数据库
    - MongoDB
tags:
series:
description: MongoDB介绍和基本特性
keywords: 
- MongoDB
- 数据库
---
# MongoDB 学习系列01
## MongoDB 介绍
[参考学习的网站](http://www.runoob.com/mongodb/mongodb-intro.html)

**关系型数据库RDBMS遵循ACID规则**
* A-原子性
* C-一致性
* I-独立性
* D-持久性

**RDBMS** 
- 高度组织化结构化数据 
- 结构化查询语言（SQL） (SQL) 
- 数据和关系都存储在单独的表中。 
- 数据操纵语言，数据定义语言 
- 严格的一致性
- 基础事务

**NoSQL** 
- 代表着不仅仅是SQL
- 没有声明性查询语言
- 没有预定义的模式
-键 - 值对存储，列存储，文档存储，图形数据库
- 最终一致性，而非ACID属性
- 非结构化和不可预知的数据
- CAP定理 
- 高性能，高可用性和可伸缩性

**MongoDB主要特点**
- C++语言编写的，是一个基于分布式文件存储的开源数据库系统
- MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成
- Mongo支持丰富的查询表达式。查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组

**MongoDB下载地址**
https://www.mongodb.com/download-center#community

## MongoDB 介绍

**MongoDB术语/概念**

SQL术语/概念 | MongoDB术语/概念 | 解释/说明
---------|--------------|------
database | database | 数据库
table | collection | 数据库表/集合
row | document | 数据记录行/文档
column | field | 数据字段/域
index | index | 索引
table joins |   | 表连接,MongoDB不支持
primary key | primary key | 主键,MongoDB自动将_id字段设置为主键

**MongoDB常用命令**
* "show dbs" 命令可以显示所有数据的列表
* "db" 命令可以显示当前数据库对象或集合
* "use"命令，可以连接到一个指定的数据库