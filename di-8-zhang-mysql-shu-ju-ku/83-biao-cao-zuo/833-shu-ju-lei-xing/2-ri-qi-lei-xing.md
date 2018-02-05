## 本节重点

* 掌握整型
* 掌握浮点型

> **本节时长需控制在15分钟内**

### 日期类型

**DATE TIME DATETIME TIMESTAMP YEAR **

**作用：存储用户注册时间，文章发布时间，员工入职时间，出生时间，过期时间等**

```
        YEAR
            YYYY（1901/2155）

        DATE
            YYYY-MM-DD（1000-01-01/9999-12-31）

        TIME
            HH:MM:SS（'-838:59:59'/'838:59:59'）

        DATETIME

            YYYY-MM-DD HH:MM:SS（1000-01-01 00:00:00/9999-12-31 23:59:59    Y）

        TIMESTAMP

            YYYYMMDD HHMMSS（1970-01-01 00:00:00/2037 年某时）
```

**验证**

```
============year===========
MariaDB [db1]> create table t10(born_year year); #无论year指定何种宽度，最后都默认是year(4)
MariaDB [db1]> insert into t10 values  
    -> (1900),
    -> (1901),
    -> (2155),
    -> (2156);
MariaDB [db1]> select * from t10;
+-----------+
| born_year |
+-----------+
|      0000 |
|      1901 |
|      2155 |
|      0000 |
+-----------+


============date,time,datetime===========
MariaDB [db1]> create table t11(d date,t time,dt datetime);
MariaDB [db1]> desc t11;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| d     | date     | YES  |     | NULL    |       |
| t     | time     | YES  |     | NULL    |       |
| dt    | datetime | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+

MariaDB [db1]> insert into t11 values(now(),now(),now());
MariaDB [db1]> select * from t11;
+------------+----------+---------------------+
| d          | t        | dt                  |
+------------+----------+---------------------+
| 2017-07-25 | 16:26:54 | 2017-07-25 16:26:54 |
+------------+----------+---------------------+



============timestamp===========
MariaDB [db1]> create table t12(time timestamp);
MariaDB [db1]> insert into t12 values();
MariaDB [db1]> insert into t12 values(null);
MariaDB [db1]> select * from t12;
+---------------------+
| time                |
+---------------------+
| 2017-07-25 16:29:17 |
| 2017-07-25 16:30:01 |
+---------------------+



============注意啦，注意啦，注意啦===========
1. 单独插入时间时，需要以字符串的形式，按照对应的格式插入
2. 插入年份时，尽量使用4位值
3. 插入两位年份时，<=69，以20开头，比如50,  结果2050      
                >=70，以19开头，比如71，结果1971
MariaDB [db1]> create table t12(y year);
MariaDB [db1]> insert into t12 values  
    -> (50),
    -> (71);
MariaDB [db1]> select * from t12;
+------+
| y    |
+------+
| 2050 |
| 1971 |
+------+



============综合练习===========
MariaDB [db1]> create table student(
    -> id int,
    -> name varchar(20),
    -> born_year year,
    -> birth date,
    -> class_time time,
    -> reg_time datetime);

MariaDB [db1]> insert into student values
    -> (1,'alex',"1995","1995-11-11","11:11:11","2017-11-11 11:11:11"),
    -> (2,'egon',"1997","1997-12-12","12:12:12","2017-12-12 12:12:12"),
    -> (3,'wsb',"1998","1998-01-01","13:13:13","2017-01-01 13:13:13");

MariaDB [db1]> select * from student;
+------+------+-----------+------------+------------+---------------------+
| id   | name | born_year | birth      | class_time | reg_time            |
+------+------+-----------+------------+------------+---------------------+
|    1 | alex |      1995 | 1995-11-11 | 11:11:11   | 2017-11-11 11:11:11 |
|    2 | egon |      1997 | 1997-12-12 | 12:12:12   | 2017-12-12 12:12:12 |
|    3 | wsb  |      1998 | 1998-01-01 | 13:13:13   | 2017-01-01 13:13:13 |
+------+------+-----------+------------+------------+---------------------+
```

**datetime与timestamp的区别**

```
在实际应用的很多场景中，MySQL的这两种日期类型都能够满足我们的需要，存储精度都为秒，但在某些情况下，会展现出他们各自的优劣。
下面就来总结一下两种日期类型的区别。

1.DATETIME的日期范围是1001——9999年，TIMESTAMP的时间范围是1970——2038年。

2.DATETIME存储时间与时区无关，TIMESTAMP存储时间与时区有关，显示的值也依赖于时区。在mysql服务器，
操作系统以及客户端连接都有时区的设置。

3.DATETIME使用8字节的存储空间，TIMESTAMP的存储空间为4字节。因此，TIMESTAMP比DATETIME的空间利用率更高。

4.DATETIME的默认值为null；TIMESTAMP的字段默认不为空（not null）,默认值为当前时间（CURRENT_TIMESTAMP），
如果不做特殊处理，并且update语句中没有指定该列的更新值，则默认更新为当前时间。
```



