## 本章总节

### 作业

现要求你写一个简单的员工信息增删改查程序，需求如下：

1.可进行模糊查询，语法至少支持下面3种查询语法:

```py
find name,age from staff_table where age > 22

find * from staff_table where dept = "IT"

find * from staff_table where enroll_date like "2013"
```

2.可创建新员工纪录，以phone做唯一键\(即不允许表里有手机号重复的情况\)，staff\_id需自增

```py
语法: add staff_table Alex Li,25,134435344,IT,2015-10-29
```

3.可删除指定员工信息纪录，输入员工id，即可删除

```py
语法: del from staff where  id=3
```

4.可修改员工信息，语法如下:

```py
UPDATE staff_table SET dept="Market" WHERE  dept = "IT" 把所有dept=IT的纪录的dept改成Market
UPDATE staff_table SET age=25 WHERE  name = "Alex Li"  把name=Alex Li的纪录的年龄改成25
```

5.以上每条语名执行完毕后，要显示这条语句影响了多少条纪录。 比如查询语句 就显示 查询出了多少条、修改语句就显示修改了多少条等。

