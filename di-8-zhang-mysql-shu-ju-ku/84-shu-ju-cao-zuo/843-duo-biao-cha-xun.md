## 本节重点

* [多表连接查询](http://www.cnblogs.com/linhaifeng/articles/7267596.html#_label2)

* [符合条件连接查询](http://www.cnblogs.com/linhaifeng/articles/7267596.html#_label3)

* [子查询](http://www.cnblogs.com/linhaifeng/articles/7267596.html#_label4)

> **本节时长需控制在15分钟内**

### 一 介绍

本节主题

* 多表连接查询
* 复合条件连接查询
* 子查询

准备表

```
#建表
create table department(
id int,
name varchar(20) 
);

create table employee(
id int primary key auto_increment,
name varchar(20),
sex enum('male','female') not null default 'male',
age int,
dep_id int
);

#插入数据
insert into department values
(200,'技术'),
(201,'人力资源'),
(202,'销售'),
(203,'运营');

insert into employee(name,sex,age,dep_id) values
('egon','male',18,200),
('alex','female',48,201),
('wupeiqi','male',38,201),
('yuanhao','female',28,202),
('liwenzhou','male',18,200),
('jingliyang','female',18,204)
;


#查看表结构和数据
mysql> desc department;
+-------+-------------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id | int(11) | YES | | NULL | |
| name | varchar(20) | YES | | NULL | |
+-------+-------------+------+-----+---------+-------+

mysql> desc employee;
+--------+-----------------------+------+-----+---------+----------------+
| Field | Type | Null | Key | Default | Extra |
+--------+-----------------------+------+-----+---------+----------------+
| id | int(11) | NO | PRI | NULL | auto_increment |
| name | varchar(20) | YES | | NULL | |
| sex | enum('male','female') | NO | | male | |
| age | int(11) | YES | | NULL | |
| dep_id | int(11) | YES | | NULL | |
+--------+-----------------------+------+-----+---------+----------------+

mysql> select * from department;
+------+--------------+
| id | name |
+------+--------------+
| 200 | 技术 |
| 201 | 人力资源 |
| 202 | 销售 |
| 203 | 运营 |
+------+--------------+

mysql> select * from employee;
+----+------------+--------+------+--------+
| id | name | sex | age | dep_id |
+----+------------+--------+------+--------+
| 1 | egon | male | 18 | 200 |
| 2 | alex | female | 48 | 201 |
| 3 | wupeiqi | male | 38 | 201 |
| 4 | yuanhao | female | 28 | 202 |
| 5 | liwenzhou | male | 18 | 200 |
| 6 | jingliyang | female | 18 | 204 |
+----+------------+--------+------+--------+

表department与employee
```

### 二 多表连接查询

```
#重点：外链接语法

SELECT 字段列表
    FROM 表1 INNER|LEFT|RIGHT JOIN 表2
    ON 表1.字段 = 表2.字段;
```

**1 交叉连接：不适用任何匹配条件。生成笛卡尔积**

```
mysql> select * from employee,department;
+----+------------+--------+------+--------+------+--------------+
| id | name       | sex    | age  | dep_id | id   | name         |
+----+------------+--------+------+--------+------+--------------+
|  1 | egon       | male   |   18 |    200 |  200 | 技术         |
|  1 | egon       | male   |   18 |    200 |  201 | 人力资源     |
|  1 | egon       | male   |   18 |    200 |  202 | 销售         |
|  1 | egon       | male   |   18 |    200 |  203 | 运营         |
|  2 | alex       | female |   48 |    201 |  200 | 技术         |
|  2 | alex       | female |   48 |    201 |  201 | 人力资源     |
|  2 | alex       | female |   48 |    201 |  202 | 销售         |
|  2 | alex       | female |   48 |    201 |  203 | 运营         |
|  3 | wupeiqi    | male   |   38 |    201 |  200 | 技术         |
|  3 | wupeiqi    | male   |   38 |    201 |  201 | 人力资源     |
|  3 | wupeiqi    | male   |   38 |    201 |  202 | 销售         |
|  3 | wupeiqi    | male   |   38 |    201 |  203 | 运营         |
|  4 | yuanhao    | female |   28 |    202 |  200 | 技术         |
|  4 | yuanhao    | female |   28 |    202 |  201 | 人力资源     |
|  4 | yuanhao    | female |   28 |    202 |  202 | 销售         |
|  4 | yuanhao    | female |   28 |    202 |  203 | 运营         |
|  5 | liwenzhou  | male   |   18 |    200 |  200 | 技术         |
|  5 | liwenzhou  | male   |   18 |    200 |  201 | 人力资源     |
|  5 | liwenzhou  | male   |   18 |    200 |  202 | 销售         |
|  5 | liwenzhou  | male   |   18 |    200 |  203 | 运营         |
|  6 | jingliyang | female |   18 |    204 |  200 | 技术         |
|  6 | jingliyang | female |   18 |    204 |  201 | 人力资源     |
|  6 | jingliyang | female |   18 |    204 |  202 | 销售         |
|  6 | jingliyang | female |   18 |    204 |  203 | 运营         |
+----+------------+--------+------+--------+------+--------------+
```

**2 内连接：只连接匹配的行**

```
#找两张表共有的部分，相当于利用条件从笛卡尔积结果中筛选出了正确的结果
#department没有204这个部门，因而employee表中关于204这条员工信息没有匹配出来
mysql> select employee.id,employee.name,employee.age,employee.sex,department.name from employee inner join department on employee.dep_id=department.id; 
+----+-----------+------+--------+--------------+
| id | name      | age  | sex    | name         |
+----+-----------+------+--------+--------------+
|  1 | egon      |   18 | male   | 技术         |
|  2 | alex      |   48 | female | 人力资源     |
|  3 | wupeiqi   |   38 | male   | 人力资源     |
|  4 | yuanhao   |   28 | female | 销售         |
|  5 | liwenzhou |   18 | male   | 技术         |
+----+-----------+------+--------+--------------+

#上述sql等同于
mysql> select employee.id,employee.name,employee.age,employee.sex,department.name from employee,department where employee.dep_id=department.id;
```

**3 外链接之左连接：优先显示左表全部记录**

```
#以左表为准，即找出所有员工信息，当然包括没有部门的员工
#本质就是：在内连接的基础上增加左边有右边没有的结果
mysql> select employee.id,employee.name,department.name as depart_name from employee left join department on employee.dep_id=department.id;
+----+------------+--------------+
| id | name       | depart_name  |
+----+------------+--------------+
|  1 | egon       | 技术         |
|  5 | liwenzhou  | 技术         |
|  2 | alex       | 人力资源     |
|  3 | wupeiqi    | 人力资源     |
|  4 | yuanhao    | 销售         |
|  6 | jingliyang | NULL         |
+----+------------+--------------+
```

**4 外链接之右连接：优先显示右表全部记录**

```
#以右表为准，即找出所有部门信息，包括没有员工的部门
#本质就是：在内连接的基础上增加右边有左边没有的结果
mysql> select employee.id,employee.name,department.name as depart_name from employee right join department on employee.dep_id=department.id;
+------+-----------+--------------+
| id   | name      | depart_name  |
+------+-----------+--------------+
|    1 | egon      | 技术         |
|    2 | alex      | 人力资源     |
|    3 | wupeiqi   | 人力资源     |
|    4 | yuanhao   | 销售         |
|    5 | liwenzhou | 技术         |
| NULL | NULL      | 运营         |
+------+-----------+--------------+
```

**5 全外连接：显示左右两个表全部记录**

```
全外连接：在内连接的基础上增加左边有右边没有的和右边有左边没有的结果
#注意：mysql不支持全外连接 full JOIN
#强调：mysql可以使用此种方式间接实现全外连接
select * from employee left join department on employee.dep_id = department.id
union
select * from employee right join department on employee.dep_id = department.id
;
#查看结果
+------+------------+--------+------+--------+------+--------------+
| id   | name       | sex    | age  | dep_id | id   | name         |
+------+------------+--------+------+--------+------+--------------+
|    1 | egon       | male   |   18 |    200 |  200 | 技术         |
|    5 | liwenzhou  | male   |   18 |    200 |  200 | 技术         |
|    2 | alex       | female |   48 |    201 |  201 | 人力资源     |
|    3 | wupeiqi    | male   |   38 |    201 |  201 | 人力资源     |
|    4 | yuanhao    | female |   28 |    202 |  202 | 销售         |
|    6 | jingliyang | female |   18 |    204 | NULL | NULL         |
| NULL | NULL       | NULL   | NULL |   NULL |  203 | 运营         |
+------+------------+--------+------+--------+------+--------------+

#注意 union与union all的区别：union会去掉相同的纪录
```

### 三 符合条件连接查询

```
#示例1：以内连接的方式查询employee和department表，并且employee表中的age字段值必须大于25,即找出年龄大于25岁的员工以及员工所在的部门
select employee.name,department.name from employee inner join department
    on employee.dep_id = department.id
    where age > 25;

#示例2：以内连接的方式查询employee和department表，并且以age字段的升序方式显示
select employee.id,employee.name,employee.age,department.name from employee,department
    where employee.dep_id = department.id
    and age > 25
    order by age asc;
```

### 四 子查询

```
#1：子查询是将一个查询语句嵌套在另一个查询语句中。
#2：内层查询语句的查询结果，可以为外层查询语句提供查询条件。
#3：子查询中可以包含：IN、NOT IN、ANY、ALL、EXISTS 和 NOT EXISTS等关键字
#4：还可以包含比较运算符：= 、 !=、> 、<等
```

**1 带IN关键字的子查询**

```
#查询平均年龄在25岁以上的部门名
select id,name from department
    where id in 
        (select dep_id from employee group by dep_id having avg(age) > 25);

#查看技术部员工姓名
select name from employee
    where dep_id in 
        (select id from department where name='技术');

#查看不足1人的部门名
select name from department
    where id in 
        (select dep_id from employee group by dep_id having count(id) <=1);
```

**2 带比较运算符的子查询**

```
#比较运算符：=、!=、>、>=、<、<=、<>
#查询大于所有人平均年龄的员工名与年龄
mysql> select name,age from emp where age > (select avg(age) from emp);
+---------+------+
| name | age |
+---------+------+
| alex | 48 |
| wupeiqi | 38 |
+---------+------+
rows in set (0.00 sec)


#查询大于部门内平均年龄的员工名、年龄
select t1.name,t1.age from emp t1
inner join 
(select dep_id,avg(age) avg_age from emp group by dep_id) t2
on t1.dep_id = t2.dep_id
where t1.age > t2.avg_age;
```

**3 带EXISTS关键字的子查询**



