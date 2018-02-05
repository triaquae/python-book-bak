## 本节重点

* 掌握数据类型

> **本节时长需控制在5分钟内**

### 介绍

存储引擎决定了表的类型，而表内存放的数据也要有不同的类型，每种数据类型都有自己的宽度，但宽度是可选的

详细参考：

* [http://www.runoob.com/mysql/mysql-data-types.html](http://www.runoob.com/mysql/mysql-data-types.html)
* [http://dev.mysql.com/doc/refman/5.7/en/data-type-overview.html](http://dev.mysql.com/doc/refman/5.7/en/data-type-overview.html)

mysql常用数据类型概览

```
#1. 数字：
    整型：tinyinit  int  bigint
    小数：
        float ：在位数比较短的情况下不精准
        double ：在位数比较长的情况下不精准
            0.000001230123123123
            存成：0.000001230000

        decimal：（如果用小数，则用推荐使用decimal）
            精准
            内部原理是以字符串形式去存

#2. 字符串：
    char（10）：简单粗暴，浪费空间，存取速度快
        root存成root000000
    varchar：精准，节省空间，存取速度慢

    sql优化：创建表时，定长的类型往前放，变长的往后放
                    比如性别           比如地址或描述信息

    >255个字符，超了就把文件路径存放到数据库中。
            比如图片，视频等找一个文件服务器，数据库中只存路径或url。


#3. 时间类型：
    最常用：datetime


#4. 枚举类型与集合类型
```

### 



