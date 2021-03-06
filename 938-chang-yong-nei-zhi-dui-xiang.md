# 常用内置对象

所谓内置对象就是ECMAScript提供出来的一些对象，我们知道对象都是有相应的属性和方法，其实这里很多的js对象跟python的很多语法类似

### 数组Array

1.数组的创建方式

* 字面量方式创建（推荐大家使用这种方式，简单粗暴）

```js
  var colors = ['red','color','yellow'];
```

* 使用构造函数（后面会讲）的方式创建 使用new关键词对构造函数进行创建对象

```js
  var colors2 = new Array();
```

2.数组的赋值

```js
var arr = [];
//通过下标进行一一赋值
arr[0] = 123;
arr[1] = '哈哈哈';
arr[2] = '嘿嘿嘿'
```

3.数组的常用方法

| 方法 | 描述 |
| :--- | :--- |
| concat\(\) | 把几个数组合并成一个数组 |
| join\(\) | 返回字符串，其中包含了连接到一起的数组中的所有元素，元素由指定的分割符分割开来 |
| pop\(\) | 移除数组的最后一个元素 |
| shift\(\) | 移除数组的第一个元素 |
| unshift\(\) | 往数组的开头添加一个元素，并且返回新的长度 |
| slice\(start,end\) | 返回数组的一段 |
| push\(\) | 往数组的最后添加一个元素，并返回新的长度 |
| sort\(\) | 对数组进行排序 |
| reverse\(\) | 对数组进行反转 |
| length | 它是一个属性，唯一的一个，获取数组的长度，可以结合for循环遍历操作 |

### 字符串String

字符串方法

| 方法 | 描述 |
| :--- | :--- |
| charAt\(\) | 返回指定索引的位置的字符 |
| concat\(\) | 返回字符串值，表示两个或多个字符串的拼接 |
| match\(\) | 返回正则表达式模式对字符串进行产找，并将包含查找结果作为结果返回（后面正则表达式课程会详细讲） |
| replace\(a,b\) | 字符串b替换了a |
| search\(stringObject\) | 知名是否存在相应匹配。如果找到一个匹配，search方法将返回一个整数值，指明这个匹配距离字符串开始的偏移位置。如果没有找到匹配，返回-1 |
| slice\(start，end\) | 返回start到end-1之间的字符串，索引从0开始 |
| split\(’a‘,1\) | 字符串拆分,以a拆分，第一个参数返回数组的最大长度 |
| substr\(start,end\) | 字符串截取，左闭右开 |
| toUpperCase\(\) | 返回一个新的字符串，该字符串字母都变成了大写 |
| toLowerCase\(\) | 返回一个新的字符串，该字符串字母都变成了小写 |

```js
//1.将number类型转换成字符串类型
var num = 132.32522;
var numStr = num.toString()
console.log(typeof numStr)
```

```js
//四舍五入
var newNum = num.toFixed(2)
console.log(newNum)
```

### Date日期对象

创建日期对象只有构造函数一种方式,使用new关键字

```js
//创建了一个date对象
var myDate = new Date();
```

**常用的方法**

| 语法 | 含义 |
| :--- | :--- |
| getDate\(\) | 根据本地时间返回指定日期对象的月份中的第几天（1-31）。 |
| Date\(\) | 根据本地时间返回当天的日期和时间 |
| getMonth\(\) | 根据本地时间返回指定日期对象的月份（0-11） |
| getFullYear\(\) | 根据本地时间返回指定日期对象的年份（四位数年份时返回四位数字） |
| getDay\(\) | 根据本地时间返回指定日期对象的星期中的第几天（0-6） |
| getHours\(\) | 根据本地时间返回指定日期对象的小时（0-23） |
| getMinutes\(\) | 根据本地时间返回指定日期对象的分钟（0-59） |
| getSeconds\(\) | 根据本地时间返回指定日期对象的秒数（0-59） |

### **Math 内置对象**

**常用内置对象**

| 方法 | 含义 |
| :--- | :--- |
| Math.floor\(\) | 向下取整,称为"地板函数" |
| Math.ceil\(\) | 向上取整,称为'地板函数' |
| Math.max\(a,b\) | 求a和b中的最大值 |
| Math.min\(a,b\) | 求a和b中的最小值 |
| Math.random\(\) | 随机数,默认0-1之间的随机数,公式min+Math.random\(\)\*\(max-min\),求min~max之间的数 |



