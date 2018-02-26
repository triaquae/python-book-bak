## 本节重点

* 掌握存储过程的基本使用

> **本节时长需控制在5分钟内**

### 一 存储过程

#### **一 存储过程介绍**

存储过程包含了一系列可执行的sql语句，存储过程存放于MySQL中，通过调用它的名字可以执行其内部的一堆sql

使用存储过程的优点：

```
#1. 用于替代程序写的SQL语句，实现程序与sql解耦

#2. 基于网络传输，传别名的数据量小，而直接传sql数据量大
```

使用存储过程的缺点：

```
#1. 程序员扩展功能不方便
```

**补充：程序与数据库结合使用的三种方式**

```
#方式一：
    MySQL：存储过程
    程序：调用存储过程

#方式二：
    MySQL：
    程序：纯SQL语句

#方式三：
    MySQL:
    程序：类和对象，即ORM（本质还是纯SQL语句）
```

#### **二 创建简单存储过程（无参）**

```
delimiter //
create procedure p1()
BEGIN
    select * from blog;
    INSERT into blog(name,sub_time) values("xxx",now());
END //
delimiter ;

#在mysql中调用
call p1() 

#在python中基于pymysql调用
cursor.callproc('p1') 
print(cursor.fetchall())
```

#### **三 创建存储过程（有参）**

```
对于存储过程，可以接收参数，其参数有三类：

#in          仅用于传入参数用
#out        仅用于返回值用
#inout     既可以传入又可以当作返回值
```

```
delimiter //
create procedure p2(
    in n1 int,
    in n2 int
)
BEGIN

    select * from blog where id > n1;
END //
delimiter ;

#在mysql中调用
call p2(3,2)

#在python中基于pymysql调用
cursor.callproc('p2',(3,2))
print(cursor.fetchall())

in:传入参数
```

```
delimiter //
create procedure p3(
    in n1 int,
    out res int
)
BEGIN
    select * from blog where id > n1;
    set res = 1;
END //
delimiter ;

#在mysql中调用
set @res=0; #0代表假（执行失败），1代表真（执行成功）
call p3(3,@res);
select @res;

#在python中基于pymysql调用
cursor.callproc('p3',(3,0)) #0相当于set @res=0
print(cursor.fetchall()) #查询select的查询结果

cursor.execute('select @_p3_0,@_p3_1;') #@p3_0代表第一个参数，@p3_1代表第二个参数，即返回值
print(cursor.fetchall())

out：返回值
```

```
delimiter //
create procedure p4(
    inout n1 int
)
BEGIN
    select * from blog where id > n1;
    set n1 = 1;
END //
delimiter ;

#在mysql中调用
set @x=3;
call p4(@x);
select @x;


#在python中基于pymysql调用
cursor.callproc('p4',(3,))
print(cursor.fetchall()) #查询select的查询结果

cursor.execute('select @_p4_0;') 
print(cursor.fetchall())

inout:既可以传入又可以返回
```

#### **四 执行存储过程**

```
-- 无参数
call proc_name()

-- 有参数，全in
call proc_name(1,2)

-- 有参数，有in，out，inout
set @t1=0;
set @t2=3;
call proc_name(1,2,@t1,@t2)

执行存储过程

在MySQL中执行存储过程-- 无参数
call proc_name()

-- 有参数，全in
call proc_name(1,2)

-- 有参数，有in，out，inout
set @t1=0;
set @t2=3;
call proc_name(1,2,@t1,@t2)

执行存储过程

在MySQL中执行存储过程
```

```
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import pymysql

conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='123', db='t1')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
# 执行存储过程
cursor.callproc('p1', args=(1, 22, 3, 4))
# 获取执行完存储的参数
cursor.execute("select @_p1_0,@_p1_1,@_p1_2,@_p1_3")
result = cursor.fetchall()

conn.commit()
cursor.close()
conn.close()


print(result)

在python中基于pymysql执行存储过程
```

#### **五 删除存储过程**

```
drop procedure proc_name;
```



