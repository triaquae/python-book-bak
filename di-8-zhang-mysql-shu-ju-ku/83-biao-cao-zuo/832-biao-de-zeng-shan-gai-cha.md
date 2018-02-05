## 本节重点

* 掌握表的增删改查

> **本节时长需控制在15分钟内**

### 一、表介绍

表相当于文件，表中的一条记录就相当于文件的一行内容，不同的是，表中的一条记录有对应的标题，称为表的字段

![](/assets/chapter8/表介绍.png)

id，name，qq，age称为字段，其余的，一行内容称为一条记录

### 二、创建表

语法

```
create table 表名(
字段名1 类型[(宽度) 约束条件],
字段名2 类型[(宽度) 约束条件],
字段名3 类型[(宽度) 约束条件]
);

#注意：
1. 在同一张表中，字段名是不能相同
2. 宽度和约束条件可选
3. 字段名和类型是必须的
```

示范

```
MariaDB [(none)]> create database db1 charset utf8;

MariaDB [(none)]> use db1;

MariaDB [db1]> create table t1(  
    -> id int, 
    -> name varchar(50),
    -> sex enum('male','female'),
    -> age int(3)
    -> );

MariaDB [db1]> show tables; #查看db1库下所有表名

MariaDB [db1]> desc t1;
+-------+-----------------------+------+-----+---------+-------+
| Field | Type                  | Null | Key | Default | Extra |
+-------+-----------------------+------+-----+---------+-------+
| id    | int(11)               | YES  |     | NULL    |       |
| name  | varchar(50)           | YES  |     | NULL    |       |
| sex   | enum('male','female') | YES  |     | NULL    |       |
| age   | int(3)                | YES  |     | NULL    |       |
+-------+-----------------------+------+-----+---------+-------+

MariaDB [db1]> select id,name,sex,age from t1;
Empty set (0.00 sec)

MariaDB [db1]> select * from t1;
Empty set (0.00 sec)

MariaDB [db1]> select id,name from t1;
Empty set (0.00 sec)
```

往表中插入数据

```
MariaDB [db1]> insert into t1 values
    -> (1,'egon',18,'male'),
    -> (2,'alex',81,'female')
    -> ;
MariaDB [db1]> select * from t1;
+------+------+------+--------+
| id   | name | age  | sex    |
+------+------+------+--------+
|    1 | egon |   18 | male   |
|    2 | alex |   81 | female |
+------+------+------+--------+



MariaDB [db1]> insert into t1(id) values 
    -> (3),
    -> (4);
MariaDB [db1]> select * from t1;
+------+------+------+--------+
| id   | name | age  | sex    |
+------+------+------+--------+
|    1 | egon |   18 | male   |
|    2 | alex |   81 | female |
|    3 | NULL | NULL | NULL   |
|    4 | NULL | NULL | NULL   |
+------+------+------+--------+
```

**注意注意注意：表中的最后一个字段不要加逗号 **

### 三、查看表结构

```
MariaDB [db1]> describe t1; #查看表结构，可简写为desc 表名
+-------+-----------------------+------+-----+---------+-------+
| Field | Type                  | Null | Key | Default | Extra |
+-------+-----------------------+------+-----+---------+-------+
| id    | int(11)               | YES  |     | NULL    |       |
| name  | varchar(50)           | YES  |     | NULL    |       |
| sex   | enum('male','female') | YES  |     | NULL    |       |
| age   | int(3)                | YES  |     | NULL    |       |
+-------+-----------------------+------+-----+---------+-------+


MariaDB [db1]> show create table t1\G; #查看表详细结构，可加\G
```

### 四、修改表结构

```
语法：
1. 修改表名
      ALTER TABLE 表名 
                          RENAME 新表名;

2. 增加字段
      ALTER TABLE 表名
                          ADD 字段名  数据类型 [完整性约束条件…],
                          ADD 字段名  数据类型 [完整性约束条件…];
      ALTER TABLE 表名
                          ADD 字段名  数据类型 [完整性约束条件…]  FIRST;
      ALTER TABLE 表名
                          ADD 字段名  数据类型 [完整性约束条件…]  AFTER 字段名;
                            
3. 删除字段
      ALTER TABLE 表名 
                          DROP 字段名;

4. 修改字段
      ALTER TABLE 表名 
                          MODIFY  字段名 数据类型 [完整性约束条件…];
      ALTER TABLE 表名 
                          CHANGE 旧字段名 新字段名 旧数据类型 [完整性约束条件…];
      ALTER TABLE 表名 
                          CHANGE 旧字段名 新字段名 新数据类型 [完整性约束条件…];
```

示范

```
示例：
1. 修改存储引擎
mysql> alter table service 
    -> engine=innodb;

2. 添加字段
mysql> alter table student10
    -> add name varchar(20) not null,
    -> add age int(3) not null default 22;
    
mysql> alter table student10
    -> add stu_num varchar(10) not null after name;                //添加name字段之后

mysql> alter table student10                        
    -> add sex enum('male','female') default 'male' first;          //添加到最前面

3. 删除字段
mysql> alter table student10
    -> drop sex;

mysql> alter table service
    -> drop mac;

4. 修改字段类型modify
mysql> alter table student10
    -> modify age int(3);
mysql> alter table student10
    -> modify id int(11) not null primary key auto_increment;    //修改为主键

5. 增加约束（针对已有的主键增加auto_increment）
mysql> alter table student10 modify id int(11) not null primary key auto_increment;
ERROR 1068 (42000): Multiple primary key defined

mysql> alter table student10 modify id int(11) not null auto_increment;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

6. 对已经存在的表增加复合主键
mysql> alter table service2
    -> add primary key(host_ip,port);        

7. 增加主键
mysql> alter table student1
    -> modify name varchar(10) not null primary key;

8. 增加主键和自动增长
mysql> alter table student1
    -> modify id int not null primary key auto_increment;

9. 删除主键
a. 删除自增约束
mysql> alter table student10 modify id int(11) not null; 

b. 删除主键
mysql> alter table student10                                 
    -> drop primary key;
```

### 五、复制表

```
复制表结构＋记录 （key不会复制: 主键、外键和索引）
mysql> create table new_service select * from service;

只复制表结构
mysql> select * from service where 1=2;        //条件为假，查不到任何记录
Empty set (0.00 sec)
mysql> create table new1_service select * from service where 1=2;  
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> create table t4 like employees;
```

### 六、删除表

```
DROP TABLE 表名;
```



