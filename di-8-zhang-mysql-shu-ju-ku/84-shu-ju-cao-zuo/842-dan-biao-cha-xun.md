## 本节重点

* [单表查询的语法](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label1)

* [关键字的执行优先级\(重点\)](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label2)

* [简单查询](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label3)

* [WHERE约束](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label4)

* [分组查询:GROUP BY](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label5)

* [HAVING过滤](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label6)

* [查询排序:ORDER BY](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label7)

* [限制查询的记录数:LIMIT](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label8)

* [使用正则表达式查询](http://www.cnblogs.com/linhaifeng/articles/7267592.html#_label9)

> **本节时长需控制在15分钟内**

### 一 单表查询的语法

```
SELECT 字段1,字段2... FROM 表名
                  WHERE 条件
                  GROUP BY field
                  HAVING 筛选
                  ORDER BY field
                  LIMIT 限制条数
```

### 二 关键字的执行优先级\(重点\)

```
重点中的重点：关键字的执行优先级
from
where
group by
having
select
distinct
order by
limit
```

**1.找到表:from**

**2.拿着where指定的约束条件，去文件/表中取出一条条记录**

**3.将取出的一条条记录进行分组group by，如果没有group by，则整体作为一组**

**4.将分组的结果进行having过滤**

**5.执行select**

**6.去重**

**7.将结果按条件排序：order by**

**8.限制结果的显示条数**

[**详细见：http://www.cnblogs.com/linhaifeng/articles/7372774.html**](http://www.cnblogs.com/linhaifeng/articles/7372774.html)

### 三 简单查询

```
company.employee
    员工id      id                  int             
    姓名        emp_name            varchar
    性别        sex                 enum
    年龄        age                 int
    入职日期     hire_date           date
    岗位        post                varchar
    职位描述     post_comment        varchar
    薪水        salary              double
    办公室       office              int
    部门编号     depart_id           int



#创建表
create table employee(
id int not null unique auto_increment,
name varchar(20) not null,
sex enum('male','female') not null default 'male', #大部分是男的
age int(3) unsigned not null default 28,
hire_date date not null,
post varchar(50),
post_comment varchar(100),
salary double(15,2),
office int, #一个部门一个屋子
depart_id int
);


#查看表结构
mysql> desc employee;
+--------------+-----------------------+------+-----+---------+----------------+
| Field        | Type                  | Null | Key | Default | Extra          |
+--------------+-----------------------+------+-----+---------+----------------+
| id           | int(11)               | NO   | PRI | NULL    | auto_increment |
| name         | varchar(20)           | NO   |     | NULL    |                |
| sex          | enum('male','female') | NO   |     | male    |                |
| age          | int(3) unsigned       | NO   |     | 28      |                |
| hire_date    | date                  | NO   |     | NULL    |                |
| post         | varchar(50)           | YES  |     | NULL    |                |
| post_comment | varchar(100)          | YES  |     | NULL    |                |
| salary       | double(15,2)          | YES  |     | NULL    |                |
| office       | int(11)               | YES  |     | NULL    |                |
| depart_id    | int(11)               | YES  |     | NULL    |                |
+--------------+-----------------------+------+-----+---------+----------------+

#插入记录
#三个部门：教学，销售，运营
insert into employee(name,sex,age,hire_date,post,salary,office,depart_id) values
('egon','male',18,'20170301','老男孩驻沙河办事处外交大使',7300.33,401,1), #以下是教学部
('alex','male',78,'20150302','teacher',1000000.31,401,1),
('wupeiqi','male',81,'20130305','teacher',8300,401,1),
('yuanhao','male',73,'20140701','teacher',3500,401,1),
('liwenzhou','male',28,'20121101','teacher',2100,401,1),
('jingliyang','female',18,'20110211','teacher',9000,401,1),
('jinxin','male',18,'19000301','teacher',30000,401,1),
('成龙','male',48,'20101111','teacher',10000,401,1),

('歪歪','female',48,'20150311','sale',3000.13,402,2),#以下是销售部门
('丫丫','female',38,'20101101','sale',2000.35,402,2),
('丁丁','female',18,'20110312','sale',1000.37,402,2),
('星星','female',18,'20160513','sale',3000.29,402,2),
('格格','female',28,'20170127','sale',4000.33,402,2),

('张野','male',28,'20160311','operation',10000.13,403,3), #以下是运营部门
('程咬金','male',18,'19970312','operation',20000,403,3),
('程咬银','female',18,'20130311','operation',19000,403,3),
('程咬铜','male',18,'20150411','operation',18000,403,3),
('程咬铁','female',18,'20140512','operation',17000,403,3)
;

#ps：如果在windows系统中，插入中文字符，select的结果为空白，可以将所有字符编码统一设置成gbk

准备表和记录
```

```
#简单查询
    SELECT id,name,sex,age,hire_date,post,post_comment,salary,office,depart_id 
    FROM employee;

    SELECT * FROM employee;

    SELECT name,salary FROM employee;

#避免重复DISTINCT
    SELECT DISTINCT post FROM employee;    

#通过四则运算查询
    SELECT name, salary*12 FROM employee;
    SELECT name, salary*12 AS Annual_salary FROM employee;
    SELECT name, salary*12 Annual_salary FROM employee;

#定义显示格式
   CONCAT() 函数用于连接字符串
   SELECT CONCAT('姓名: ',name,'  年薪: ', salary*12)  AS Annual_salary 
   FROM employee;
   
   CONCAT_WS() 第一个参数为分隔符
   SELECT CONCAT_WS(':',name,salary*12)  AS Annual_salary 
   FROM employee;
```

```
1
```

```
 查出所有员工的名字，薪资,格式为
    
<
名字:egon
>
<
薪资:3000
>

2
 查出所有的岗位（去掉重复）

3 查出所有员工名字，以及他们的年薪,年薪的字段名为annual_year
```

```
select concat('<名字:',name,'>    ','<薪资:',salary,'>') from employee;
select distinct depart_id from employee;
select name,salary*12 annual_salary from employee;
```



