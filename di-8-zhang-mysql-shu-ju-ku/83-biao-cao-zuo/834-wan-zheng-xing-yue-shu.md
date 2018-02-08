## 本节重点

* [not null与default](http://www.cnblogs.com/linhaifeng/articles/7238814.html#_label2)

* [unique](http://www.cnblogs.com/linhaifeng/articles/7238814.html#_label3)

* [primary key](http://www.cnblogs.com/linhaifeng/articles/7238814.html#_label4)

* [auto\_increment](http://www.cnblogs.com/linhaifeng/articles/7238814.html#_label5)

* [foreign key](http://www.cnblogs.com/linhaifeng/articles/7238814.html#_label6)

> **本节时长需控制在15分钟内**

### 一、介绍

约束条件与数据类型的宽度一样，都是可选参数

作用：用于保证数据的完整性和一致性  
主要分为：

```
PRIMARY KEY (PK)    标识该字段为该表的主键，可以唯一的标识记录
FOREIGN KEY (FK)    标识该字段为该表的外键
NOT NULL    标识该字段不能为空
UNIQUE KEY (UK)    标识该字段的值是唯一的
AUTO_INCREMENT    标识该字段的值自动增长（整数类型，而且为主键）
DEFAULT    为该字段设置默认值

UNSIGNED 无符号
ZEROFILL 使用0填充
```

说明：

```
1. 是否允许为空，默认NULL，可设置NOT NULL，字段不允许为空，必须赋值
2. 字段是否有默认值，缺省的默认值是NULL，如果插入记录时不给字段赋值，此字段使用默认值
sex enum('male','female') not null default 'male'
age int unsigned NOT NULL default 20 必须为正值（无符号） 不允许为空 默认是20
3. 是否是key
主键 primary key
外键 foreign key
索引 (index,unique...)
```

### 二、not null与default









auto\_increment时增加新内容

清空表：

delete from t1; \#如果有自增id，新增的数据，仍然是以删除前的最后一样作为起始。

truncate table t1;数据量大，删除速度比上一条快，且直接从零开始，



