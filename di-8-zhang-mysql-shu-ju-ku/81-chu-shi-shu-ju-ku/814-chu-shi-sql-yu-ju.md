## 本节重点

* 了解数据库的作用
* 掌握概念库、表、记录

> **本节时长需控制在15分钟内**

### 初识sql语句

有了mysql这个数据库软件，就可以将程序员从对数据的管理中解脱出来，专注于对程序逻辑的编写

mysql服务端软件即mysqld帮我们管理好文件夹以及文件，前提是作为使用者的我们，需要下载mysql的客户端，或者其他模块来连接到mysqld，然后使用mysql软件规定的语法格式去提交自己命令，实现对文件夹或文件的管理。该语法即sql（Structured Query Language 即结构化查询语言）

```
SQL语言主要用于存取数据、查询数据、更新数据和管理关系数据库系统,SQL语言由IBM开发。SQL语言分为3种类型：
```

```
1、DDL语句    数据库定义语言： 数据库、表、视图、索引、存储过程，例如CREATE DROP ALTER

2、DML语句    数据库操纵语言： 插入数据INSERT、删除数据DELETE、更新数据UPDATE、查询数据SELECT

3、DCL语句    数据库控制语言： 例如控制用户的访问权限GRANT、REVOKE
```

```
#1. 操作文件夹
        增：create database db1 charset utf8;
        查：show databases;
        改：alter database db1 charset latin1;
        删除: drop database db1;


#2. 操作文件
    先切换到文件夹下：use db1
        增：create table t1(id int,name char);
        查：show tables
        改：alter table t1 modify name char(3);
              alter table t1 change name name1 char(2);
        删：drop table t1;


#3. 操作文件中的内容/记录
        增：insert into t1 values(1,'egon1'),(2,'egon2'),(3,'egon3');
        查：select * from t1;
        改：update t1 set name='sb' where id=2;
        删：delete from t1 where id=1;
```



