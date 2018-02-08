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





