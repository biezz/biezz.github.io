---
title: SQL中left join，right join，inner join用法和区别
date: 2018-07-28 19:18:00
categories:
- sql
tags:
- sql
---

### 简单介绍
left join(左联接)： 返回包括左表中的所有记录和右表中联结字段相等的记录  
right join(右联接) ：返回包括右表中的所有记录和左表中联结字段相等的记录  
inner join(等值连接) ：只返回两个表中联结字段相等的行  

### 用法
假设数据库中有2个表，myclass和Class，分别有如下内容：
```
MariaDB [form]> select * from myclass;
+----+------------+----------+
| id | phone      | name     |
+----+------------+----------+
|  1 | 2147483647 | xiaoming |
|  2 | 2147483647 | xiaowu   |
|  3 | 2147483647 | xiaotian |
+----+------------+----------+
3 rows in set (0.00 sec)

MariaDB [form]> select * from Class;
+----+----------+-------+-------+-----+
| id | name     | sex   | score | age |
+----+----------+-------+-------+-----+
|  1 | xiaoming | man   |    80 |   0 |
|  2 | xiaowu   | man   |    65 |   0 |
|  3 | xiaotian | woman |    77 |  18 |
|  4 | xiaohu   | 0     |    88 |  21 |
+----+----------+-------+-------+-----+
4 rows in set (0.00 sec)

```
   
left join 的用法：
```
MariaDB [form]> select * from Class left join myclass on Class.id=myclass.id;
+----+----------+-------+-------+-----+------+------------+----------+
| id | name     | sex   | score | age | id   | phone      | name     |
+----+----------+-------+-------+-----+------+------------+----------+
|  1 | xiaoming | man   |    80 |   0 |    1 | 2147483647 | xiaoming |
|  2 | xiaowu   | man   |    65 |   0 |    2 | 2147483647 | xiaowu   |
|  3 | xiaotian | woman |    77 |  18 |    3 | 2147483647 | xiaotian |
|  4 | xiaohu   | 0     |    88 |  21 | NULL |       NULL | NULL     |
+----+----------+-------+-------+-----+------+------------+----------+

```
right join 的用法：
```
MariaDB [form]> select * from Class right join myclass on Class.id=myclass.id;
+------+----------+-------+-------+------+----+------------+----------+
| id   | name     | sex   | score | age  | id | phone      | name     |
+------+----------+-------+-------+------+----+------------+----------+
|    1 | xiaoming | man   |    80 |    0 |  1 | 2147483647 | xiaoming |
|    2 | xiaowu   | man   |    65 |    0 |  2 | 2147483647 | xiaowu   |
|    3 | xiaotian | woman |    77 |   18 |  3 | 2147483647 | xiaotian |
+------+----------+-------+-------+------+----+------------+----------+

```
inner join 的用法：
```
MariaDB [form]> select * from Class inner join myclass on Class.id=myclass.id;
+----+----------+-------+-------+-----+----+------------+----------+
| id | name     | sex   | score | age | id | phone      | name     |
+----+----------+-------+-------+-----+----+------------+----------+
|  1 | xiaoming | man   |    80 |   0 |  1 | 2147483647 | xiaoming |
|  2 | xiaowu   | man   |    65 |   0 |  2 | 2147483647 | xiaowu   |
|  3 | xiaotian | woman |    77 |  18 |  3 | 2147483647 | xiaotian |
+----+----------+-------+-------+-----+----+------------+----------+

```
