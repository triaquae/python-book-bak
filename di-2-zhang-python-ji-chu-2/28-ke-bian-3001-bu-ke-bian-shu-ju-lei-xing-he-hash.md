## 本节重点

1.让学生了解可变和不可变数据类型

2.了解hash函数

## 可变与不可变类型

截止到目前为止我们已经学过很多数据类型：数字类型、字符串类型、列表类型、元祖类型。

在python中，我们对数据类型还有另外一种分类方式，我们给数据类型分为可变数据类型和不可变数据类型。在了解原理之前，我们先来看看分类情况：

| 可变类型 | 不可变类型 |
| :--- | :--- |
| 列表 | 数字 |
|  | 字符串 |
|  | 元祖 |

看着上面这句话，我们来看看什么叫可变什么叫不可变

列表

```py
>>> l = [1,2,3,4]
>>> id(l)
4392665160
>>> l[1] = 1.5
>>> l
[1, 1.5, 3, 4]
>>> id(l)
4392665160
```

数字

```py
>>> a = 1
>>> id(a)
4297537952 
>>> a+=1
>>> id(a)
4297537984
```

从内存角度看列表与数字的变与不变

![](/assets/list中的值变化内存图.png)

![](/assets/数字改变内存图.png)

字符串

```py
>>> s = 'hello'
>>> s[1] = 'a'
Traceback (most recent call last):
  File "<pyshell#5>", line 1, in <module>
    s[1] = 'a'
TypeError: 'str' object does not support item assignment
>>> 
```

元组

```py
>>> t = (1,2,3,4)
>>> t[1] = 1.5
Traceback (most recent call last):
  File "<pyshell#10>", line 1, in <module>
    t[1] = 1.5
TypeError: 'tuple' object does not support item assignment
```

## hash





