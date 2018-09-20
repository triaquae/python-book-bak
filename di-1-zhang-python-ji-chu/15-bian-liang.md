<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?9cae5942a3c39f3b6fcf0a32b00277e2";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>


## 本节重点：

* 让学生掌握变量的作用
* 让学生掌握标识符的命名规范
* 掌握常量与变量的区别

> **本节时长需控制在25分钟之内**

## 变量是什么？

#### 引子 （10分钟）

计算机的主要作用之一是进行运算，用python进行数值运算非常容易，跟我们平常用计算器一样简单:

```py
>>> 4*3/2 - 1
5.0
```

那现在有一个需求，咱们同学A花钱如流水，为了帮助他理财，我们决定为他出个月底消费报表，报表中有2个重要数据,当月总花费和分类汇总费用，即总共花了多少钱吃饭、买衣服等。

![](/assets/variable_sample2.png)

现在要求你用程序 把 每个消费分类统计 和总消费依次计算并打印出来，你怎么做呢？如果不用计算机，让你用笔算，你会不会跟下面一样算呢？![](/assets/IMG_20170605_153726.jpg)你发现没有？你在最后在算总消费的时候直接用的是之前已经算好的中间结果，为什么这么做？都知道这样是为了避免重新再算一遍所有的数据。 那在程序中呢？

```py
>>> print('eat',10+15+7+4+7+3)
eat 46
>>> print('cloth',20)
cloth 20
>>> print('traffic',6+6+6+6+6)
traffic 30
>>> print('精神',300+300+400+200)
精神 1200
>>> 
>>> 
>>> print('总消费', 46+20+30+1200)
总消费 1296
```

我的亲， 你这么写是有问题的，啥问题？你最后算总消费的时候 是人肉 把之前算出来的分类结果 填进去的， 但是我们把程序写在脚本里运行时， 你肯定不会预先知道吃饭、交通、买衣服3个分类的结果的，这个结果是动态算出来的，那你如何把这3个动态结果做为总消费运算的数据源呢？答案简单， 直接把每个分类结果先起个名字存下来，然后计算总消费的时候，只需要把之前存下来的几个名字调用 一下就可以啦！

```py
>>> eat = 10+15+7+4+7+3
>>> cloth = 20
>>> traffic = 6+6+6+6+6
>>> 精神=300+300+200+400
>>> 
>>> total = eat + cloth + traffic + 精神
>>> print('总消息',total)
总消息 1296
```

eat,cloth,traffic,精神,total这几个名字的作用，就是**把程序运算的中间结果临时存到内存里，以备后面的代码继续调用，这几个名字的学名就叫做“变量”**

#### 变量的作用 （3分钟）

**Variables **are used to** store information to be referenced and manipulated in a computer program**. They also provide a way of **labeling data with a descriptive name, **so our programs can be understood more clearly by the reader and ourselves. **It is helpful to think of variables as containers that hold information**. Their sole purpose is to label and store data in memory. This data can then be used throughout your program.

## 变量定义规范 \(8-10分钟\)

#### **声明变量**

```py
name = "Alex Li"
```

#### ![](/assets/37A7B9E3-6DB2-459E-A5F7-49EFFCC33505.jpeg)

#### **变量定义规则**

1. 变量名只能是 字母、数字或下划线的任意组合
2. 变量名的第一个字符不能是数字
3. 以下关键字不能声明为变量名\['and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'exec', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'not', 'or', 'pass', 'print', 'raise', 'return', 'try', 'while', 'with', 'yield'\]

#### **定义方式**

驼峰体

```py
AgeOfOldboy = 56 
NumberOfStudents = 80
```

下划线

```
age_of_oldboy = 56 
number_of_students = 80
```

> 你觉得哪种更清晰，哪种就是官方推荐的，我想你肯定会先第2种,第一种AgeOfOldboy咋一看以为是AngelaBaby



#### 变量的修改

。。。。



#### **定义变量不好的方式举例**

* 变量名为中文、拼音
* 变量名过长
* 变量名词不达意

## 常量\(2-4分钟\)

常量即指不变的量，如pai 3.141592653...,  或在程序运行过程中不会改变的量

举例，假如老男孩老师的年龄会变，那这就是个变量，但在一些情况下，他的年龄不会变了，那就是常量。在Python中没有一个专门的语法代表常量，程序员约定俗成用变量名全部大写代表常量

```py
AGE_OF_OLDBOY = 56
```

> 在c语言中有专门的常量定义语法，`const int count = 60;`一旦定义为常量，更改即会报错



