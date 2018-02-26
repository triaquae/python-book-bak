## 本节重点

* 掌握函数的基本使用

> **本节时长需控制在5分钟内**

### 一 函数

MySQL中提供了许多内置函数，例如：

    一、数学函数
        ROUND(x,y)
            返回参数x的四舍五入的有y位小数的值

        RAND()
            返回０到１内的随机值,可以通过提供一个参数(种子)使RAND()随机数生成器生成一个指定的值。

    二、聚合函数(常用于GROUP BY从句的SELECT查询中)
        AVG(col)返回指定列的平均值
        COUNT(col)返回指定列中非NULL值的个数
        MIN(col)返回指定列的最小值
        MAX(col)返回指定列的最大值
        SUM(col)返回指定列的所有值之和
        GROUP_CONCAT(col) 返回由属于一组的列值连接组合而成的结果    

    三、字符串函数

        CHAR_LENGTH(str)
            返回值为字符串str 的长度，长度的单位为字符。一个多字节字符算作一个单字符。
        CONCAT(str1,str2,...)
            字符串拼接
            如有任何一个参数为NULL ，则返回值为 NULL。
        CONCAT_WS(separator,str1,str2,...)
            字符串拼接（自定义连接符）
            CONCAT_WS()不会忽略任何空字符串。 (然而会忽略所有的 NULL）。

        CONV(N,from_base,to_base)
            进制转换
            例如：
                SELECT CONV('a',16,2); 表示将 a 由16进制转换为2进制字符串表示

        FORMAT(X,D)
            将数字X 的格式写为'#,###,###.##',以四舍五入的方式保留小数点后 D 位， 并将结果以字符串的形式返回。若  D 为 0, 则返回结果不带有小数点，或不含小数部分。
            例如：
                SELECT FORMAT(12332.1,4); 结果为： '12,332.1000'
        INSERT(str,pos,len,newstr)
            在str的指定位置插入字符串
                pos：要替换位置其实位置
                len：替换的长度
                newstr：新字符串
            特别的：
                如果pos超过原字符串长度，则返回原字符串
                如果len超过原字符串长度，则由新字符串完全替换
        INSTR(str,substr)
            返回字符串 str 中子字符串的第一个出现位置。

        LEFT(str,len)
            返回字符串str 从开始的len位置的子序列字符。

        LOWER(str)
            变小写

        UPPER(str)
            变大写

        REVERSE(str)
            返回字符串 str ，顺序和字符顺序相反。

        SUBSTRING(str,pos) , SUBSTRING(str FROM pos) SUBSTRING(str,pos,len) , SUBSTRING(str FROM pos FOR len)
            不带有len 参数的格式从字符串str返回一个子字符串，起始于位置 pos。带有len参数的格式从字符串str返回一个长度同len字符相同的子字符串，起始于位置 pos。 使用 FROM的格式为标准 SQL 语法。也可能对pos使用一个负值。假若这样，则子字符串的位置起始于字符串结尾的pos 字符，而不是字符串的开头位置。在以下格式的函数中可以对pos 使用一个负值。

            mysql> SELECT SUBSTRING('Quadratically',5);
                -> 'ratically'

            mysql> SELECT SUBSTRING('foobarbar' FROM 4);
                -> 'barbar'

            mysql> SELECT SUBSTRING('Quadratically',5,6);
                -> 'ratica'

            mysql> SELECT SUBSTRING('Sakila', -3);
                -> 'ila'

            mysql> SELECT SUBSTRING('Sakila', -5, 3);
                -> 'aki'

            mysql> SELECT SUBSTRING('Sakila' FROM -4 FOR 2);
                -> 'ki'

    四、日期和时间函数
        CURDATE()或CURRENT_DATE() 返回当前的日期
        CURTIME()或CURRENT_TIME() 返回当前的时间
        DAYOFWEEK(date)   返回date所代表的一星期中的第几天(1~7)
        DAYOFMONTH(date)  返回date是一个月的第几天(1~31)
        DAYOFYEAR(date)   返回date是一年的第几天(1~366)
        DAYNAME(date)   返回date的星期名，如：SELECT DAYNAME(CURRENT_DATE);
        FROM_UNIXTIME(ts,fmt)  根据指定的fmt格式，格式化UNIX时间戳ts
        HOUR(time)   返回time的小时值(0~23)
        MINUTE(time)   返回time的分钟值(0~59)
        MONTH(date)   返回date的月份值(1~12)
        MONTHNAME(date)   返回date的月份名，如：SELECT MONTHNAME(CURRENT_DATE);
        NOW()    返回当前的日期和时间
        QUARTER(date)   返回date在一年中的季度(1~4)，如SELECT QUARTER(CURRENT_DATE);
        WEEK(date)   返回日期date为一年中第几周(0~53)
        YEAR(date)   返回日期date的年份(1000~9999)

        重点:
        DATE_FORMAT(date,format) 根据format字符串格式化date值

           mysql> SELECT DATE_FORMAT('2009-10-04 22:23:00', '%W %M %Y');
            -> 'Sunday October 2009'
           mysql> SELECT DATE_FORMAT('2007-10-04 22:23:00', '%H:%i:%s');
            -> '22:23:00'
           mysql> SELECT DATE_FORMAT('1900-10-04 22:23:00',
            ->                 '%D %y %a %d %m %b %j');
            -> '4th 00 Thu 04 10 Oct 277'
           mysql> SELECT DATE_FORMAT('1997-10-04 22:23:00',
            ->                 '%H %k %I %r %T %S %w');
            -> '22 22 10 10:23:00 PM 22:23:00 00 6'
           mysql> SELECT DATE_FORMAT('1999-01-01', '%X %V');
            -> '1998 52'
           mysql> SELECT DATE_FORMAT('2006-06-00', '%d');
            -> '00'

    五、加密函数
        MD5()    
            计算字符串str的MD5校验和
        PASSWORD(str)   
            返回字符串str的加密版本，这个加密过程是不可逆转的，和UNIX密码加密过程使用不同的算法。

    六、控制流函数            
        CASE WHEN[test1] THEN [result1]...ELSE [default] END
            如果testN是真，则返回resultN，否则返回default
        CASE [test] WHEN[val1] THEN [result]...ELSE [default]END  
            如果test和valN相等，则返回resultN，否则返回default

        IF(test,t,f)   
            如果test是真，返回t；否则返回f

        IFNULL(arg1,arg2) 
            如果arg1不是空，返回arg1，否则返回arg2

        NULLIF(arg1,arg2) 
            如果arg1=arg2返回NULL；否则返回arg1        

    七、控制流函数小练习
    #7.1、准备表
    /*
    Navicat MySQL Data Transfer

    Source Server         : localhost_3306
    Source Server Version : 50720
    Source Host           : localhost:3306
    Source Database       : student

    Target Server Type    : MYSQL
    Target Server Version : 50720
    File Encoding         : 65001

    Date: 2018-01-02 12:05:30
    */

    SET FOREIGN_KEY_CHECKS=0;

    -- ----------------------------
    -- Table structure for course
    -- ----------------------------
    DROP TABLE IF EXISTS `course`;
    CREATE TABLE `course` (
      `c_id` int(11) NOT NULL,
      `c_name` varchar(255) DEFAULT NULL,
      `t_id` int(11) DEFAULT NULL,
      PRIMARY KEY (`c_id`),
      KEY `t_id` (`t_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

    -- ----------------------------
    -- Records of course
    -- ----------------------------
    INSERT INTO `course` VALUES ('1', 'python', '1');
    INSERT INTO `course` VALUES ('2', 'java', '2');
    INSERT INTO `course` VALUES ('3', 'linux', '3');
    INSERT INTO `course` VALUES ('4', 'web', '2');

    -- ----------------------------
    -- Table structure for score
    -- ----------------------------
    DROP TABLE IF EXISTS `score`;
    CREATE TABLE `score` (
      `id` int(11) NOT NULL AUTO_INCREMENT,
      `s_id` int(10) DEFAULT NULL,
      `c_id` int(11) DEFAULT NULL,
      `num` double DEFAULT NULL,
      PRIMARY KEY (`id`)
    ) ENGINE=InnoDB AUTO_INCREMENT=12 DEFAULT CHARSET=utf8;

    -- ----------------------------
    -- Records of score
    -- ----------------------------
    INSERT INTO `score` VALUES ('1', '1', '1', '79');
    INSERT INTO `score` VALUES ('2', '1', '2', '78');
    INSERT INTO `score` VALUES ('3', '1', '3', '35');
    INSERT INTO `score` VALUES ('4', '2', '2', '32');
    INSERT INTO `score` VALUES ('5', '3', '1', '66');
    INSERT INTO `score` VALUES ('6', '4', '2', '77');
    INSERT INTO `score` VALUES ('7', '4', '1', '68');
    INSERT INTO `score` VALUES ('8', '5', '1', '66');
    INSERT INTO `score` VALUES ('9', '2', '1', '69');
    INSERT INTO `score` VALUES ('10', '4', '4', '75');
    INSERT INTO `score` VALUES ('11', '5', '4', '66.7');

    -- ----------------------------
    -- Table structure for student
    -- ----------------------------
    DROP TABLE IF EXISTS `student`;
    CREATE TABLE `student` (
      `s_id` varchar(20) NOT NULL,
      `s_name` varchar(255) DEFAULT NULL,
      `s_age` int(10) DEFAULT NULL,
      `s_sex` char(1) DEFAULT NULL,
      PRIMARY KEY (`s_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

    -- ----------------------------
    -- Records of student
    -- ----------------------------
    INSERT INTO `student` VALUES ('1', '鲁班', '12', '男');
    INSERT INTO `student` VALUES ('2', '貂蝉', '20', '女');
    INSERT INTO `student` VALUES ('3', '刘备', '35', '男');
    INSERT INTO `student` VALUES ('4', '关羽', '34', '男');
    INSERT INTO `student` VALUES ('5', '张飞', '33', '女');

    -- ----------------------------
    -- Table structure for teacher
    -- ----------------------------
    DROP TABLE IF EXISTS `teacher`;
    CREATE TABLE `teacher` (
      `t_id` int(10) NOT NULL,
      `t_name` varchar(50) DEFAULT NULL,
      PRIMARY KEY (`t_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

    -- ----------------------------
    -- Records of teacher
    -- ----------------------------
    INSERT INTO `teacher` VALUES ('1', '大王');
    INSERT INTO `teacher` VALUES ('2', 'alex');
    INSERT INTO `teacher` VALUES ('3', 'egon');
    INSERT INTO `teacher` VALUES ('4', 'peiqi');

    #7.2、统计各科各分数段人数.显示格式:课程ID,课程名称,[100-85],[85-70],[70-60],[ <60]

    select  score.c_id,
              course.c_name, 
          sum(CASE WHEN num BETWEEN 85 and 100 THEN 1 ELSE 0 END) as '[100-85]',
          sum(CASE WHEN num BETWEEN 70 and 85 THEN 1 ELSE 0 END) as '[85-70]',
          sum(CASE WHEN num BETWEEN 60 and 70 THEN 1 ELSE 0 END) as '[70-60]',
          sum(CASE WHEN num < 60 THEN 1 ELSE 0 END) as '[ <60]'
    from score,course where score.c_id=course.c_id GROUP BY score.c_id;

```
#1 基本使用
mysql> SELECT DATE_FORMAT('2009-10-04 22:23:00', '%W %M %Y');
        -> 'Sunday October 2009'
mysql> SELECT DATE_FORMAT('2007-10-04 22:23:00', '%H:%i:%s');
        -> '22:23:00'
mysql> SELECT DATE_FORMAT('1900-10-04 22:23:00',
    ->                 '%D %y %a %d %m %b %j');
        -> '4th 00 Thu 04 10 Oct 277'
mysql> SELECT DATE_FORMAT('1997-10-04 22:23:00',
    ->                 '%H %k %I %r %T %S %w');
        -> '22 22 10 10:23:00 PM 22:23:00 00 6'
mysql> SELECT DATE_FORMAT('1999-01-01', '%X %V');
        -> '1998 52'
mysql> SELECT DATE_FORMAT('2006-06-00', '%d');
        -> '00'


#2 准备表和记录
CREATE TABLE blog (
    id INT PRIMARY KEY auto_increment,
    NAME CHAR (32),
    sub_time datetime
);

INSERT INTO blog (NAME, sub_time)
VALUES
    ('第1篇','2015-03-01 11:31:21'),
    ('第2篇','2015-03-11 16:31:21'),
    ('第3篇','2016-07-01 10:21:31'),
    ('第4篇','2016-07-22 09:23:21'),
    ('第5篇','2016-07-23 10:11:11'),
    ('第6篇','2016-07-25 11:21:31'),
    ('第7篇','2017-03-01 15:33:21'),
    ('第8篇','2017-03-01 17:32:21'),
    ('第9篇','2017-03-01 18:31:21');

#3. 提取sub_time字段的值，按照格式后的结果即"年月"来分组
SELECT DATE_FORMAT(sub_time,'%Y-%m'),COUNT(1) FROM blog GROUP BY DATE_FORMAT(sub_time,'%Y-%m');

#结果
+-------------------------------+----------+
| DATE_FORMAT(sub_time,'%Y-%m') | COUNT(1) |
+-------------------------------+----------+
| 2015-03                       |        2 |
| 2016-07                       |        4 |
| 2017-03                       |        3 |
+-------------------------------+----------+
rows in set (0.00 sec)

需要掌握函数：date_format
```

更多函数：[中文猛击这里](http://doc.mysql.cn/mysql5/refman-5.1-zh.html-chapter/functions.html#encryption-functions) OR [官方猛击这里](https://dev.mysql.com/doc/refman/5.7/en/functions.html)

#### **一 自定义函数**

```
#！！！注意！！！
#函数中不要写sql语句（否则会报错），函数仅仅只是一个功能，是一个在sql中被应用的功能
#若要想在begin...end...中写sql，请用存储过程
```

```
delimiter //
create function f1(
    i1 int,
    i2 int)
returns int
BEGIN
    declare num int;
    set num = i1 + i2;
    return(num);
END //
delimiter ;
```

```
delimiter //
create function f5(
    i int
)
returns int
begin
    declare res int default 0;
    if i = 10 then
        set res=100;
    elseif i = 20 then
        set res=200;
    elseif i = 30 then
        set res=300;
    else
        set res=400;
    end if;
    return res;
end //
delimiter ;
```

#### **二 删除函数**

```
drop function func_name;
```

#### **三 执行函数**

```
# 获取返回值
select UPPER('egon') into @res;
SELECT @res;


# 在查询中使用
select f1(11,nid) ,name from tb2;
```



