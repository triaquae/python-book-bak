## 什么是数据类型？

我们人类可以很容易的分清数字与字符的区别，但是计算机并不能呀，计算机虽然很强大，但从某种角度上看又很傻，除非你明确的告诉它，1是数字，“汉”是文字，否则它是分不清1和‘汉’的区别的，因此，在每个编程语言里都会有一个叫数据类型的东东，其实就是对常用的各种数据类型进行了明确的划分，你想让计算机进行数值运算，你就传数字给它，你想让他处理文字，就传字符串类型给他。Python中常用的数据类型包括多种，今天我们暂只讲4种， 数字、字符串、布尔类型、列表。



## 数字

**int（整型）**

在64位系统上，整数的位数为64位，取值范围为-2**63～2**63-1，即-9223372036854775808～9223372036854775807

**long（长整型）**

跟C语言不同，Python的长整数没有指定位宽，即：Python没有限制长整数数值的大小，但实际上由于机器内存有限，我们使用的长整数数值不可能无限大。

注意，自从Python2.2起，如果整数发生溢出，Python会自动将整数数据转换为长整数，所以如今在长整数数据后面不加字母L也不会导致严重后果了。

> 注意：在Python3里不再有long类型了，全都是int



```py
>>> a= 2**64
>>> type(a)  #type()是查看数据类型的方法
>>> b = 2**60
>>> type(b)
```

**float \(浮点型\)**

即小数

```
>>> type(2.32)
```

## 

## 字符串

**在Python中,加了引号的字符都被认为是字符串！**

```py
>>> name = "Alex Li" #双引号
>>> age = "22"       #只要加引号就是字符串
>>> age2 = 22          #int
>>> 
>>> msg = '''My name is Alex, I am 22 years old!'''  #我擦，3个引号也可以
>>> 
>>> hometown = 'ShanDong'   #单引号也可以
```

那单引号、双引号、多引号有什么区别呢？ 让我大声告诉你，单双引号木有任何区别，只有下面这种情况 你需要考虑单双的配合

```py
msg = "My name is Alex , I'm 22 years old!"
```

多引号什么作用呢？作用就是多行字符串必须用多引号

```py
msg = '''
今天我想写首小诗，
歌颂我的同桌，
你看他那乌黑的短发，
好像一只炸毛鸡。
'''
print(msg)
```

**字符串拼接**

数字可以进行加减乘除等运算，字符串呢？让我大声告诉你，也能？what ?是的，但只能进行”相加”和”相乘”运算。

```py
>>> name
'Alex Li'
>>> age
'22'
>>> 
>>> name + age  #相加其实就是简单拼接
'Alex Li22'
>>> 
>>> name * 10 #相乘其实就是复制自己多少次，再拼接在一起
'Alex LiAlex LiAlex LiAlex LiAlex LiAlex LiAlex LiAlex LiAlex LiAlex Li'
```

注意，字符串的拼接只能是双方都是字符串，不能跟数字或其它类型拼接

```py
>>> type(name),type(age2)
(<type 'str'>, <type 'int'>)
>>> 
>>> name
'Alex Li'
>>> age2
22
>>> name + age2
Traceback (most recent call last):
  File "", line 1, in 
TypeError: cannot concatenate 'str' and 'int' objects #错误提示数字 和 字符 不能拼接
```

## 

## 布尔型\(bool\)

布尔类型很简单，就两个值 ，一个True\(真\)，一个False\(假\), 主要用记逻辑判断

但其实你们并不明白对么？ let me explain, 我现在有2个值 ， a=3, b=5 , 我说a&gt;b你说成立么? 我们当然知道不成立，但问题是计算机怎么去描述这成不成立呢？或者说a&lt; b是成立，计算机怎么描述这是成立呢？

没错，答案就是，用布尔类型

```py
>>> a=3
>>> b=5
>>> 
>>> a > b #不成立就是False,即假
False
>>> 
>>> a < b #成立就是True, 即真
True
```

计算机为什么要描述这种条件呢？因为接下来就可以根据条件结果来干不同的事情啦呀！比如

```js
if a > b 
   print(a is bigger than b )
else 
   print(a is smaller than b )
```

上面是伪代码，但是不是意味着， 计算机就可以根据判断结果不同，来执行不同的动作啦？



## 列表\(List\)

如果要把全班的人名在内存里存下来，用上面的字符串类型可以做到，但取的时候不方便。

```
names = "Alex,Jack,Rain,Rachel,Mack..."
```

你print\(names\)它打印的是所有人的信息，如果想取出Rain，没办法\(可以用字符串切割方式，但是很麻烦\)。此时，用列表就比较合适。

```py
>>> names = ["Alex","Jack","Rain","Rachel","Mack"]
>>> names[2] #为何names[2]就能取出Rain?
'Rain'
```

因为列表的是通过下标来标记元素位置的。 下标从0开始，每添加一个元素，就自动+1



  


| 元素名 | Alex | Jack | Rain | Rachel | Mack |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 下标\(索引\) | 0 | 1 | 2 | 3 | 4 |

### **元素添加**

元素的添加有2种方式，插入、追加，插入指可以插入到列表的任意位置

**插入**

```py
>>> names
['Alex', 'Jack', 'Rain', 'Rachel', 'Mack']
>>> names.insert(3,"小明")  #3代表你想插入的位置
>>> names
['Alex', 'Jack', 'Rain', '小明', 'Rachel', 'Mack']
>>> 
```

**追加**

添加到列表的尾部

```py
>>> names
['Alex', 'Jack', 'Rain', '小明', 'Rachel', 'Mack']
>>> names.append("小强")
>>> names
['Alex', 'Jack', 'Rain', '小明', 'Rachel', 'Mack', '小强']
```

### **修改**

直接根据下标找到元素重新赋值即可

```py
>>> names[0] = "金角大王Alex"
>>> names
['金角大王Alex', 'Jack', 'Rain', '小明', 'Rachel', 'Mack', '小强']
```

### **删除元素**

这个不是通过下标了，是根据元素名子。

```py
>>> names
['金角大王Alex', 'Jack', 'Rain', '小明', 'Rachel', 'Mack', '小强']
>>> names.remove("小明")
>>> names
['金角大王Alex', 'Jack', 'Rain', 'Rachel', 'Mack', '小强']
```

上面的命令会删除从左开始找到的第一个小明， 如果有多个小明，则只删除找到的第一个。

### **判断元素是否在列表里**

```py
>>> names
['金角大王Alex', 'Jack', 'Rain', 'Rachel', 'Mack', '小强']
>>> 
>>> "Mack" in names
True
```



