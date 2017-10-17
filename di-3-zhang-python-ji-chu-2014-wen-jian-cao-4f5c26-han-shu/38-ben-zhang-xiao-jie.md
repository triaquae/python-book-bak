## 本章总节

### 作业

现要求你写一个简单的员工信息增删改查程序，需求如下：

![](/assets/chapter3/staff_table.png)

当然此表你在文件存储时可以这样表示

```
1,Alex Li,22,13651054608,IT,2013-04-01
2,Jack Wang,28,13451024608,HR,2015-01-07
3,Rain Wang,21,13451054608,IT,2017-04-01
4,Mack Qiao,44,15653354208,Sales,2016-02-01
5,Rachel Chen,23,13351024606,IT,2013-03-16
6,Eric Liu,19,18531054602,Marketing,2012-12-01
7,Chao Zhang,21,13235324334,Administration,2011-08-08
8,Kevin Chen,22,13151054603,Sales,2013-04-01
9,Shit Wen,20,13351024602,IT,2017-07-03
10,Shanshan Du,26,13698424612,Operation,2017-07-02
```

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

