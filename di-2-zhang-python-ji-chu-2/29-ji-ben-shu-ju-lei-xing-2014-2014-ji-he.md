## 本节重点

1.让学员了解什么是集合以及集合的作用

2.让学员掌握集合的定义和基本特征

3.让学员掌握集合的关系运算和常用操作

## 认识集合

由一个或多个确定的元素所构成的整体叫做集合。

**集合中的元素有三个特征：**

1.确定性（集合中的元素必须是确定的）

2.互异性（集合中的元素互不相同。例如：集合A={1，a}，则a不能等于1）

3.无序性（集合中的元素没有先后之分），如集合{3,4,5}和{3,5,4}算作同一个集合。

\*集合概念存在的目的是将不同的值存放到一起，不同的集合间用来做关系运算，无需纠结于集合中某个值

## 集合的定义

```py
s = {1,2,3,1}
#定义可变集合
>>> set_test=set('hello')
>>> set_test
{'l', 'o', 'e', 'h'}
#改为不可变集合frozenset
>>> f_set_test=frozenset(set_test)
>>> f_set_test
frozenset({'l', 'e', 'h', 'o'})
```

## **集合的常用操作**

**元素的增加**

单个元素的增加 : add\(\)，add的作用类似列表中的append

对序列的增加 : update\(\)，而update类似extend方法，update方法可以支持同时传入多个参数：

```py
>>> a={1,2}
>>> a.update([3,4],[1,2,7])
>>> a
{1, 2, 3, 4, 7}
>>> a.update("hello")
>>> a
{1, 2, 3, 4, 7, 'h', 'e', 'l', 'o'}
>>> a.add("hello")
>>> a
{1, 2, 3, 4, 'hello', 7, 'h', 'e', 'l', 'o'}
```

**元素的删除**

集合删除单个元素有两种方法：

元素不在原集合中时：

set.discard\(x\)不会抛出异常

set.remove\(x\)会抛出KeyError错误

```py
>>> a={1,2,3,4}
>>> a.discard(1)
>>> a
{2, 3, 4}
>>> a.discard(1)
>>> a
{2, 3, 4}
>>> a.remove(1)
Traceback (most recent call last):
  File "<input>", line 1, in <module>
KeyError: 1
```

pop\(\)：由于集合是无序的，pop返回的结果不能确定，且当集合为空时调用pop会抛出KeyError错误，

clear\(\):清空集合

```py
>>> a={3,"a",2.1,1}
>>> a.pop()
>>> a.pop()
>>> a.clear()
>>> a
set()
>>> a.pop()
Traceback (most recent call last):
  File "<input>", line 1, in <module>
KeyError: 'pop from an empty set'
```

## 集合的**关系运算**

\|,\|=:合集

```py
a = {1,2,3}
b = {2,3,4,5}
print(a.union(b))
print(a|b)
```

&.&=:交集

```py
a = {1,2,3}
b = {2,3,4,5}
print(a.intersection(b))
print(a&b)
```

－,－=:差集

```py
a = {1,2,3}
b = {2,3,4,5}
print(a.difference(b))
print(a-b) 
```

^,^=:对称差集

```py
a = {1,2,3}
b = {2,3,4,5}
print(a.symmetric_difference(b))
print(a^b)
```

包含关系

in,not in：判断某元素是否在集合内  
＝＝,！＝:判断两个集合是否相等

两个集合之间一般有三种关系，相交、包含、不相交。在Python中分别用下面的方法判断：

* set.isdisjoint\(s\)：判断两个集合是不是不相交
* set.issuperset\(s\)：判断集合是不是包含其他集合，等同于a&gt;=b
* set.issubset\(s\)：判断集合是不是被其他集合包含，等同于a&lt;=b



