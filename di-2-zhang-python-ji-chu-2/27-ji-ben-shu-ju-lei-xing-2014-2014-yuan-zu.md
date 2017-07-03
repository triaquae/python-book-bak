## 本节重点

1.让学员理解元组数据类型出现的意义

2.让学员掌握元组的定义和特性

3.学员能熟练掌握元组常用操作，并了解其他工厂方法

## 引子

介绍完列表，我们再介绍一种和列表非常相似的数据类型。叫做元组。

## 元组的定义和特性

_定义：与列表类似，只不过［］改成（）_

_特性：  _

_　　1.可存放多个值  
　　2.不可变  
　　3._按照从左到右的顺序定义元组元素，下标从0开始顺序访问，有序

> 解释为什么要有不可变数据类型元祖出现？

## 元组的创建与常用操作

创建

```py
ages = (11, 22, 33, 44, 55)
#或
ages = tuple((11, 22, 33, 44, 55))
```

常用操作

```py
#索引
>>> ages = (11, 22, 33, 44, 55)
>>> ages[0]
11
>>> ages[3]
44
>>> ages[-1]
55

#切片:同list　　

#循环
>>> for age in ages:
	print(age)

	
11
22
33
44
55

#长度
>>> len(ages)
5

#包含
>>> 11 in ages
True
>>> 66 in ages
False
>>> 11 not in ages
False
```

## 元组的特性详解

**1.可存放多个值**

如果元组中只有一个值

```py
t = (1,)
t = (1)   #<==>t = 1
```

元组中不仅可以存放数字、字符串，还可以存放更加复杂的数据类型

**2.不可变**

元组本身不可变，如果元组中还包含其他可变元素，这些可变元素可以改变

## 元组的工厂函数

```py
class tuple(object):
    """
    tuple() -> empty tuple
    tuple(iterable) -> tuple initialized from iterable's items

    If the argument is a tuple, the return value is the same object.
    """
    def count(self, value): # real signature unknown; restored from __doc__
        """ T.count(value) -> integer -- return number of occurrences of value """
        return 0

    def index(self, value, start=None, stop=None): # real signature unknown; restored from __doc__
        """
        T.index(value, [start, [stop]]) -> integer -- return first index of value.
        Raises ValueError if the value is not present.
        """
        return 0

    def __add__(self, *args, **kwargs): # real signature unknown
        """ Return self+value. """
        pass

    def __contains__(self, *args, **kwargs): # real signature unknown
        """ Return key in self. """
        pass

    def __eq__(self, *args, **kwargs): # real signature unknown
        """ Return self==value. """
        pass

    def __getattribute__(self, *args, **kwargs): # real signature unknown
        """ Return getattr(self, name). """
        pass

    def __getitem__(self, *args, **kwargs): # real signature unknown
        """ Return self[key]. """
        pass

    def __getnewargs__(self, *args, **kwargs): # real signature unknown
        pass

    def __ge__(self, *args, **kwargs): # real signature unknown
        """ Return self>=value. """
        pass

    def __gt__(self, *args, **kwargs): # real signature unknown
        """ Return self>value. """
        pass

    def __hash__(self, *args, **kwargs): # real signature unknown
        """ Return hash(self). """
        pass

    def __init__(self, seq=()): # known special case of tuple.__init__
        """
        tuple() -> empty tuple
        tuple(iterable) -> tuple initialized from iterable's items

        If the argument is a tuple, the return value is the same object.
        # (copied from class doc)
        """
        pass

    def __iter__(self, *args, **kwargs): # real signature unknown
        """ Implement iter(self). """
        pass

    def __len__(self, *args, **kwargs): # real signature unknown
        """ Return len(self). """
        pass

    def __le__(self, *args, **kwargs): # real signature unknown
        """ Return self<=value. """
        pass

    def __lt__(self, *args, **kwargs): # real signature unknown
        """ Return self<value. """
        pass

    def __mul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value.n """
        pass

    @staticmethod # known case of __new__
    def __new__(*args, **kwargs): # real signature unknown
        """ Create and return a new object.  See help(type) for accurate signature. """
        pass

    def __ne__(self, *args, **kwargs): # real signature unknown
        """ Return self!=value. """
        pass

    def __repr__(self, *args, **kwargs): # real signature unknown
        """ Return repr(self). """
        pass

    def __rmul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value. """
        pass
```



