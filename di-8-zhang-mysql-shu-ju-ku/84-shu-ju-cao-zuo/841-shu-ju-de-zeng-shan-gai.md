## 本节重点

* [插入数据INSERT](http://www.cnblogs.com/linhaifeng/articles/7267587.html#_label2)

* [更新数据UPDATE](http://www.cnblogs.com/linhaifeng/articles/7267587.html#_label3)

* [删除数据DELETE](http://www.cnblogs.com/linhaifeng/articles/7267587.html#_label4)

* [权限管理](http://www.cnblogs.com/linhaifeng/articles/7267587.html#_label6)

> **本节时长需控制在15分钟内**

### 一 介绍

MySQL数据操作： DML

========================================================

在MySQL管理软件中，可以通过SQL语句中的DML语言来实现数据的操作，包括

1. _使用INSERT实现数据的插入_
2. _UPDATE实现数据的更新_
3. _使用DELETE实现数据的删除_
4. _使用SELECT查询数据以及。_

_========================================================_

本节内容包括：

插入数据  
更新数据  
删除数据  
查询数据

### 二 插入数据INSERT

```
1. 插入完整数据（顺序插入）
    语法一：
    INSERT INTO 表名(字段1,字段2,字段3…字段n) VALUES(值1,值2,值3…值n);

    语法二：
    INSERT INTO 表名 VALUES (值1,值2,值3…值n);

2. 指定字段插入数据
    语法：
    INSERT INTO 表名(字段1,字段2,字段3…) VALUES (值1,值2,值3…);

3. 插入多条记录
    语法：
    INSERT INTO 表名 VALUES
        (值1,值2,值3…值n),
        (值1,值2,值3…值n),
        (值1,值2,值3…值n);

4. 插入查询结果
    语法：
    INSERT INTO 表名(字段1,字段2,字段3…字段n) 
                    SELECT (字段1,字段2,字段3…字段n) FROM 表2
                    WHERE …;
```

### 三 更新数据UPDATE

```
语法：
    UPDATE 表名 SET
        字段1=值1,
        字段2=值2,
        WHERE CONDITION;

示例：
    UPDATE mysql.user SET password=password(‘123’) 
        where user=’root’ and host=’localhost’;
```

### 四 删除数据DELETE

```
语法：
    DELETE FROM 表名 
        WHERE CONITION;

示例：
    DELETE FROM mysql.user 
        WHERE password=’’;

练习：
    更新MySQL root用户密码为mysql123
    删除除从本地登录的root用户以外的所有用户
```

### 五 权限管理

![](/assets/chapter8/8-4-1权限管理图.png)

```
#授权表
user #该表放行的权限，针对：所有数据，所有库下所有表，以及表下的所有字段
db #该表放行的权限，针对：某一数据库，该数据库下的所有表，以及表下的所有字段
tables_priv #该表放行的权限。针对：某一张表，以及该表下的所有字段
columns_priv #该表放行的权限，针对：某一个字段

#按图解释：
user：放行db1，db2及其包含的所有
db：放行db1，及其db1包含的所有
tables_priv:放行db1.table1，及其该表包含的所有
columns_prive:放行db1.table1.column1，只放行该字段
```

```
#创建用户
create user 'egon'@'1.1.1.1' identified by '123';
create user 'egon'@'192.168.1.%' identified by '123';
create user 'egon'@'%' identified by '123';


#授权：对文件夹，对文件，对文件某一字段的权限
查看帮助：help grant
常用权限有：select,update,alter,delete
all可以代表除了grant之外的所有权限

#针对所有库的授权:*.*
grant select on *.* to 'egon1'@'localhost' identified by '123'; #只在user表中可以查到egon1用户的select权限被设置为Y

#针对某一数据库：db1.*
grant select on db1.* to 'egon2'@'%' identified by '123'; #只在db表中可以查到egon2用户的select权限被设置为Y

#针对某一个表：db1.t1
grant select on db1.t1 to 'egon3'@'%' identified by '123';  #只在tables_priv表中可以查到egon3用户的select权限

#针对某一个字段：
mysql> select * from t3;
+------+-------+------+
| id   | name  | age  |
+------+-------+------+
|    1 | egon1 |   18 |
|    2 | egon2 |   19 |
|    3 | egon3 |   29 |
+------+-------+------+

grant select (id,name),update (age) on db1.t3 to 'egon4'@'localhost' identified by '123'; 
#可以在tables_priv和columns_priv中看到相应的权限
mysql> select * from tables_priv where user='egon4'\G
*************************** 1. row ***************************
       Host: localhost
         Db: db1
       User: egon4
 Table_name: t3
    Grantor: root@localhost
  Timestamp: 0000-00-00 00:00:00
 Table_priv:
Column_priv: Select,Update
row in set (0.00 sec)

mysql> select * from columns_priv where user='egon4'\G
*************************** 1. row ***************************
       Host: localhost
         Db: db1
       User: egon4
 Table_name: t3
Column_name: id
  Timestamp: 0000-00-00 00:00:00
Column_priv: Select
*************************** 2. row ***************************
       Host: localhost
         Db: db1
       User: egon4
 Table_name: t3
Column_name: name
  Timestamp: 0000-00-00 00:00:00
Column_priv: Select
*************************** 3. row ***************************
       Host: localhost
         Db: db1
       User: egon4
 Table_name: t3
Column_name: age
  Timestamp: 0000-00-00 00:00:00
Column_priv: Update
rows in set (0.00 sec)

#删除权限
revoke select on db1.* to 'alex'@'%';

权限相关操作
```



