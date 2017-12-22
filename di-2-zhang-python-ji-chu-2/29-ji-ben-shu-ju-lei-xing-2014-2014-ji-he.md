## 本节重点

1.让学员了解什么是集合以及集合的作用

2.让学员掌握集合的定义和基本特征

3.让学员掌握集合的关系运算和常用操作

## 引子

现在有一个linux班一个python班，我们创建两个列表，把班里的学生表示出来：

l = \['张三','李四','老男孩'\]

p = \['张三','李四','alex'\]

现在要找出既在linux班上课也在python班上课的学生，应该怎么找？

```py
l= ['张三','李四','老男孩']
p = ['张三','李四','alex']
l_p = []
for i in l:
    if i in p:
        l_p.append(i)
print(l_p)
```

上面这种方法可以实现我们的需求，但是比较麻烦，而且当列表变得非常长，执行代码的效率也是问题。

接下来，我们要学习一种新的数据类型，能够非常轻松的帮我们完成这个任务。

## 认识集合

集合是一个数学概念：由一个或多个确定的元素所构成的整体叫做集合。

**集合中的元素有三个特征：**

1.确定性（元素必须可hash）

2.互异性（去重）

3.无序性（集合中的元素没有先后之分），如集合{3,4,5}和{3,5,4}算作同一个集合。

> 注意：集合存在的意义就在于**去重和关系运算**

## 用集合解决问题

```py
l= {'张三','李四','老男孩'}  #集合定义
p = {'张三','李四','alex'}
l_p = l&p    #集合求交集
print(l_p)
```

![](/assets/交集.png)

## 集合的定义

```py
l= {1,2,3,1}  #此处应说明集合“去重”的效果
#定义可变集合
>>> set_test=set('hello') #此处应说明集合的“无序性”
>>> set_test
{'l', 'o', 'e', 'h'}
#改为不可变集合frozenset
>>> f_set_test=frozenset(set_test)
>>> f_set_test
frozenset({'l', 'e', 'h', 'o'})
```

## 集合的**关系运算**

除了刚刚我们学过的交集之外，集合还可以做其他的关系运算。

继续以引子为例，现在已知两个集合分别是学习linux班的同学和学习python班的同学

&.&=:交集——既学习linux课程也学习python课程的同学

![](/assets/交集%282%29.png)

```py
l= {'张三','李四','老男孩'}
p = {'张三','李四','alex'}
print(l.intersection(p))
print(l&p)
```

\|,\|=:合集，也叫并集——linux班和python班的所有同学

> 这里同学们不可以单纯的认为python班的人数+linux班的人数就是结果，如果两班人数相加应该是6人。但学习Linux班的张三和李四还同时在python班学习，因此我们实际上总共只有四个学员。**求并集除了合并效果之外还有去重功能**

![](/assets/并集.png)

```py
l= {'张三','李四','老男孩'}
p = {'张三','李四','alex'}
print(l.union(p))
print(l|p)
```

－,－=:差集——只在linux而不python班的同学

![](/assets/差集.png)

```py
l= {'张三','李四','老男孩'}
p = {'张三','李四','alex'}
print(l.difference(p))
print(l-p)
```

^,^=:对称差集——只在linux班或只在python班的同学

![](/assets/对称差集.png)

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

## 集合的工厂函数

```py
class set(object):
    """
    set() -> new empty set object
    set(iterable) -> new set object

    Build an unordered collection of unique elements.
    """
    def add(self, *args, **kwargs): # real signature unknown
        """
        Add an element to a set.

        This has no effect if the element is already present.
        """
        pass

    def clear(self, *args, **kwargs): # real signature unknown
        """ Remove all elements from this set. """
        pass

    def copy(self, *args, **kwargs): # real signature unknown
        """ Return a shallow copy of a set. """
        pass

    def difference(self, *args, **kwargs): # real signature unknown
        """
        相当于s1-s2

        Return the difference of two or more sets as a new set.

        (i.e. all elements that are in this set but not the others.)
        """
        pass

    def difference_update(self, *args, **kwargs): # real signature unknown
        """ Remove all elements of another set from this set. """
        pass

    def discard(self, *args, **kwargs): # real signature unknown
        """
        与remove功能相同，删除元素不存在时不会抛出异常

        Remove an element from a set if it is a member.

        If the element is not a member, do nothing.
        """
        pass

    def intersection(self, *args, **kwargs): # real signature unknown
        """
        相当于s1&s2

        Return the intersection of two sets as a new set.

        (i.e. all elements that are in both sets.)
        """
        pass

    def intersection_update(self, *args, **kwargs): # real signature unknown
        """ Update a set with the intersection of itself and another. """
        pass

    def isdisjoint(self, *args, **kwargs): # real signature unknown
        """ Return True if two sets have a null intersection. """
        pass

    def issubset(self, *args, **kwargs): # real signature unknown
        """ 
        相当于s1<=s2

        Report whether another set contains this set. """
        pass

    def issuperset(self, *args, **kwargs): # real signature unknown
        """
        相当于s1>=s2

         Report whether this set contains another set. """
        pass

    def pop(self, *args, **kwargs): # real signature unknown
        """
        Remove and return an arbitrary set element.
        Raises KeyError if the set is empty.
        """
        pass

    def remove(self, *args, **kwargs): # real signature unknown
        """
        Remove an element from a set; it must be a member.

        If the element is not a member, raise a KeyError.
        """
        pass

    def symmetric_difference(self, *args, **kwargs): # real signature unknown
        """
        相当于s1^s2

        Return the symmetric difference of two sets as a new set.

        (i.e. all elements that are in exactly one of the sets.)
        """
        pass

    def symmetric_difference_update(self, *args, **kwargs): # real signature unknown
        """ Update a set with the symmetric difference of itself and another. """
        pass

    def union(self, *args, **kwargs): # real signature unknown
        """
        相当于s1|s2

        Return the union of sets as a new set.

        (i.e. all elements that are in either set.)
        """
        pass

    def update(self, *args, **kwargs): # real signature unknown
        """ Update a set with the union of itself and others. """
        pass

...略...
```



