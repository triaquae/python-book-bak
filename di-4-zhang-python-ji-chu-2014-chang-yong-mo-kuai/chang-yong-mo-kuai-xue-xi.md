## 本节重点：

* 使学员掌握time and datetime模块的使用

> **本节时长需控制在25分钟内**

## time & datetime 模块

在平常的代码中，我们常常需要与时间打交道。在Python中，与时间处理有关的模块就包括：time，datetime,calendar\(很少用，不讲\)，下面分别来介绍。

在开始之前，首先要说明几点：

**一、在Python中，通常有这几种方式来表示时间：**

1. 时间戳 
2. 格式化的时间字符串 
3. 元组（struct\_time）共九个元素。由于Python的time模块实现主要调用C库，所以各个平台可能有所不同。

**二、几个定义**

UTC（Coordinated Universal Time，世界协调时）亦即格林威治天文时间，世界标准时间。在中国为UTC+8。DST（Daylight Saving Time）即夏令时。

时间戳（timestamp）的方式：通常来说，时间戳表示的是从1970年1月1日00:00:00开始按秒计算的偏移量。我们运行“type\(time.time\(\)\)”，返回的是float类型。

元组（struct\_time）方式：struct\_time元组共有9个元素，返回struct\_time的函数主要有gmtime\(\)，localtime\(\)，strptime\(\)。下面列出这种方式元组中的几个元素：

```
索引（Index）    属性（Attribute）    值（Values）
0     tm_year（年）                 比如2011 
1     tm_mon（月）             1 - 12
2     tm_mday（日）                 1 - 31
3     tm_hour（时）                 0 - 23
4     tm_min（分）             0 - 59
5     tm_sec（秒）             0 - 61
6     tm_wday（weekday）            0 - 6（0表示周日）
7     tm_yday（一年中的第几天）    1 - 366
8     tm_isdst（是否是夏令时）            默认为-1
```

#### time模块的方法

* time.localtime\(\[secs\]\)：将一个时间戳转换为当前时区的struct\_time。secs参数未提供，则以当前时间为准。
* time.gmtime\(\[secs\]\)：和localtime\(\)方法类似，gmtime\(\)方法是将一个时间戳转换为UTC时区（0时区）的struct\_time。
* time.time\(\)：返回当前时间的时间戳。
* time.mktime\(t\)：将一个struct\_time转化为时间戳。
* time.sleep\(secs\)：线程推迟指定的时间运行。单位为秒。
* time.asctime\(\[t\]\)：把一个表示时间的元组或者struct\_time表示为这种形式：'Sun Oct  1 12:04:38 2017'。如果没有参数，将会将time.localtime\(\)作为参数传入。
* time.ctime\(\[secs\]\)：把一个时间戳（按秒计算的浮点数）转化为time.asctime\(\)的形式。如果参数未给或者为None的时候，将会默认time.time\(\)为参数。它的作用相当于time.asctime\(time.localtime\(secs\)\)。
* time.strftime\(format\[, t\]\)：把一个代表时间的元组或者struct\_time（如由time.localtime\(\)和time.gmtime\(\)返回）转化为格式化的时间字符串。如果t未指定，将传入time.localtime\(\)。

  * 举例：time.strftime\("%Y-%m-%d %X", time.localtime\(\)\) \#输出'2017-10-01 12:14:23'

* time.strptime\(string\[, format\]\)：把一个格式化时间字符串转化为struct\_time。实际上它和strftime\(\)是逆操作。

  * 举例：time.strptime\('2017-10-3 17:54',"%Y-%m-%d %H:%M"\) \#输出 time.struct\_time\(tm\_year=2017, tm\_mon=10, tm\_mday=3, tm\_hour=17, tm\_min=54, tm\_sec=0, tm\_wday=1, tm\_yday=276, tm\_isdst=-1\) 

| 字符串转时间格式对应表 |
| :--- |


|  | Meaning | Notes |
| :--- | :--- | :--- |
| `%a` | Locale’s abbreviated weekday name. |  |
| `%A` | Locale’s full weekday name. |  |
| `%b` | Locale’s abbreviated month name. |  |
| `%B` | Locale’s full month name. |  |
| `%c` | Locale’s appropriate date and time representation. |  |
| `%d` | Day of the month as a decimal number \[01,31\]. |  |
| `%H` | Hour \(24-hour clock\) as a decimal number \[00,23\]. |  |
| `%I` | Hour \(12-hour clock\) as a decimal number \[01,12\]. |  |
| `%j` | Day of the year as a decimal number \[001,366\]. |  |
| `%m` | Month as a decimal number \[01,12\]. |  |
| `%M` | Minute as a decimal number \[00,59\]. |  |
| `%p` | Locale’s equivalent of either AM or PM. | \(1\) |
| `%S` | Second as a decimal number \[00,61\]. | \(2\) |
| `%U` | Week number of the year \(Sunday as the first day of the week\) as a decimal number \[00,53\]. All days in a new year preceding the first Sunday are considered to be in week 0. | \(3\) |
| `%w` | Weekday as a decimal number \[0\(Sunday\),6\]. |  |
| `%W` | Week number of the year \(Monday as the first day of the week\) as a decimal number \[00,53\]. All days in a new year preceding the first Monday are considered to be in week 0. | \(3\) |
| `%x` | Locale’s appropriate date representation. |  |
| `%X` | Locale’s appropriate time representation. |  |
| `%y` | Year without century as a decimal number \[00,99\]. |  |
| `%Y` | Year with century as a decimal number. |  |
| `%z` | Time zone offset indicating a positive or negative time difference from UTC/GMT of the form +HHMM or -HHMM, where H represents decimal hour digits and M represents decimal minute digits \[-23:59, +23:59\]. |  |
| `%Z` | Time zone name \(no characters if no time zone exists\). |  |
|  | `%%` | A literal `'%'` character. |

最后为了容易记住转换关系，看下图

![](/assets/chapter4/time-convert.png)

#### 

#### datetime模块

相比于time模块，datetime模块的接口则更直观、更容易调用

**datetime模块定义了下面这几个类：**

* datetime.date：表示日期的类。常用的属性有year, month, day；
* datetime.time：表示时间的类。常用的属性有hour, minute, second, microsecond；
* datetime.datetime：表示日期时间。
* datetime.timedelta：表示时间间隔，即两个时间点之间的长度。
* datetime.tzinfo：与时区有关的相关信息。（这里不详细充分讨论该类，感兴趣的童鞋可以参考python手册）

**我们需要记住的方法仅以下几个：**

1. d=datetime.datetime.now\(\)  返回当前的datetime日期类型

```
d.timestamp(),d.today(), d.year,d.timetuple()等方法可以调用
```

2.datetime.date.fromtimestamp\(322222\)  把一个时间戳转为datetime日期类型

3.时间运算

```
>>> datetime.datetime.now()

datetime.datetime(2017, 10, 1, 12, 53, 11, 821218)

>>> datetime.datetime.now() + datetime.timedelta(4) #当前时间 +4天

datetime.datetime(2017, 10, 5, 12, 53, 35, 276589)

>>> datetime.datetime.now() + datetime.timedelta(hours=4) #当前时间+4小时

datetime.datetime(2017, 10, 1, 16, 53, 42, 876275)
```

4.时间替换

```
>>> d.replace(year=2999,month=11,day=30)

datetime.date(2999, 11, 30)
```



