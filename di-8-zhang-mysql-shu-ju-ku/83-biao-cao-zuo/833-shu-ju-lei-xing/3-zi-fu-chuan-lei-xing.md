## 本节重点

* 掌握char类型与varchar类型

> **本节时长需控制在15分钟内**

### 字符类型

```
#官网：https://dev.mysql.com/doc/refman/5.7/en/char.html
#注意：char和varchar括号内的参数指的都是字符的长度

#char类型：定长，简单粗暴，浪费空间，存取速度快
    字符长度范围：0-255（一个中文是一个字符，是utf8编码的3个字节）
    存储：
        存储char类型的值时，会往右填充空格来满足长度
        例如：指定长度为10，存>10个字符则报错，存<10个字符则用空格填充直到凑够10个字符存储

    检索：
        在检索或者说查询时，查出的结果会自动删除尾部的空格，除非我们打开pad_char_to_full_length SQL模式（SET sql_mode = 'PAD_CHAR_TO_FULL_LENGTH';）

#varchar类型：变长，精准，节省空间，存取速度慢
    字符长度范围：0-65535（如果大于21845会提示用其他类型 。mysql行最大限制为65535字节，字符编码为utf-8：https://dev.mysql.com/doc/refman/5.7/en/column-count-limit.html）
    存储：
        varchar类型存储数据的真实内容，不会用空格填充，如果'ab  ',尾部的空格也会被存起来
        强调：varchar类型会在真实数据前加1-2Bytes的前缀，该前缀用来表示真实数据的bytes字节数（1-2Bytes最大表示65535个数字，正好符合mysql对row的最大字节限制，即已经足够使用）
        如果真实的数据<255bytes则需要1Bytes的前缀（1Bytes=8bit 2**8最大表示的数字为255）
        如果真实的数据>255bytes则需要2Bytes的前缀（2Bytes=16bit 2**16最大表示的数字为65535）

    检索：
        尾部有空格会保存下来，在检索或者说查询时，也会正常显示包含空格在内的内容
```

官网解释如下![](/assets/chapter8/字符类型.png)测试前了解两个函数

```
length：查看字节数
char_length:查看字符数
```

**1. char填充空格来满足固定长度，但是在查询时却会很不要脸地删除尾部的空格（装作自己好像没有浪费过空间一样），然后修改sql\_mode让其现出原形**

```
mysql> create table t1(x char(5),y varchar(5));
Query OK, 0 rows affected (0.26 sec)

#char存5个字符，而varchar存4个字符
mysql> insert into t1 values('你瞅啥 ','你瞅啥 ');
Query OK, 1 row affected (0.05 sec)

mysql> SET sql_mode='';
Query OK, 0 rows affected, 1 warning (0.00 sec)

#在检索时char很不要脸地将自己浪费的2个字符给删掉了，装的好像自己没浪费过空间一样，而varchar很老实，存了多少，就显示多少
mysql> select x,char_length(x),y,char_length(y) from t1; 
+-----------+----------------+------------+----------------+
| x         | char_length(x) | y          | char_length(y) |
+-----------+----------------+------------+----------------+
| 你瞅啥    |              3 | 你瞅啥     |              4 |
+-----------+----------------+------------+----------------+
row in set (0.00 sec)

#略施小计，让char现出原形
mysql> SET sql_mode = 'PAD_CHAR_TO_FULL_LENGTH';
Query OK, 0 rows affected (0.00 sec)

#这下子char原形毕露了......
mysql> select x,char_length(x),y,char_length(y) from t1;
+-------------+----------------+------------+----------------+
| x           | char_length(x) | y          | char_length(y) |
+-------------+----------------+------------+----------------+
| 你瞅啥      |              5 | 你瞅啥     |              4 |
+-------------+----------------+------------+----------------+
row in set (0.00 sec)


#char类型：3个中文字符+2个空格=11Bytes
#varchar类型:3个中文字符+1个空格=10Bytes
mysql> select x,length(x),y,length(y) from t1;
+-------------+-----------+------------+-----------+
| x           | length(x) | y          | length(y) |
+-------------+-----------+------------+-----------+
| 你瞅啥      |        11 | 你瞅啥     |        10 |
+-------------+-----------+------------+-----------+
row in set (0.00 sec)
```

**2. 虽然 CHAR 和 VARCHAR 的存储方式不太相同,但是对于两个字符串的比较,都只比 较其值,忽略 CHAR 值存在的右填充,即使将 SQL \_MODE 设置为 PAD\_CHAR\_TO\_FULL\_ LENGTH 也一样,,但这不适用于like**

```
Values in CHAR and VARCHAR columns are sorted and compared according to the character set collation assigned to the column.

All MySQL collations are of type PAD SPACE. This means that all CHAR, VARCHAR, and TEXT values are compared without regard to any trailing spaces. “Comparison” in this context does not include the LIKE pattern-matching operator, for which trailing spaces are significant. For example:

mysql> CREATE TABLE names (myname CHAR(10));
Query OK, 0 rows affected (0.03 sec)

mysql> INSERT INTO names VALUES ('Monty');
Query OK, 1 row affected (0.00 sec)

mysql> SELECT myname = 'Monty', myname = 'Monty  ' FROM names;
+------------------+--------------------+
| myname = 'Monty' | myname = 'Monty  ' |
+------------------+--------------------+
|                1 |                  1 |
+------------------+--------------------+
row in set (0.00 sec)

mysql> SELECT myname LIKE 'Monty', myname LIKE 'Monty  ' FROM names;
+---------------------+-----------------------+
| myname LIKE 'Monty' | myname LIKE 'Monty  ' |
+---------------------+-----------------------+
|                   1 |                     0 |
+---------------------+-----------------------+
row in set (0.00 sec)
```

**3. 总结**

```
#常用字符串系列：char与varchar
注：虽然varchar使用起来较为灵活，但是从整个系统的性能角度来说，char数据类型的处理速度更快，有时甚至可以超出varchar处理速度的50%。因此，用户在设计数据库时应当综合考虑各方面的因素，以求达到最佳的平衡

#其他字符串系列（效率：char>varchar>text）
TEXT系列 TINYTEXT TEXT MEDIUMTEXT LONGTEXT
BLOB 系列    TINYBLOB BLOB MEDIUMBLOB LONGBLOB 
BINARY系列 BINARY VARBINARY

text：text数据类型用于保存变长的大字符串，可以组多到65535 (2**16 − 1)个字符。
mediumtext：A TEXT column with a maximum length of 16,777,215 (2**24 − 1) characters.
longtext：A TEXT column with a maximum length of 4,294,967,295 or 4GB (2**32 − 1) characters.
```



