## 本节重点

* 掌握枚举类型与集合类型

> **本节时长需控制在5分钟内**

### 枚举类型与集合类型

字段的值只能在给定范围中选择，如单选框，多选框

enum 单选 只能在给定的范围内选一个值，如性别 sex 男male/女female

set 多选 在给定的范围内可以选择一个或一个以上的值（爱好1,爱好2,爱好3...）

```
MariaDB [db1]> create table consumer( 
    -> name varchar(50),
    -> sex enum('male','female'),
    -> level enum('vip1','vip2','vip3','vip4','vip5'), #在指定范围内，多选一
    -> hobby set('play','music','read','study') #在指定范围内，多选多
    -> );

MariaDB [db1]> insert into consumer values  
    -> ('egon','male','vip5','read,study'),
    -> ('alex','female','vip1','girl');

MariaDB [db1]> select * from consumer;
+------+--------+-------+------------+
| name | sex    | level | hobby      |
+------+--------+-------+------------+
| egon | male   | vip5  | read,study |
| alex | female | vip1  |            |
+------+--------+-------+------------+
```



