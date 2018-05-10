## 本节重点

1.让学员理解字典数据类型出现的意义

2.让学员掌握字典的定义和特性

3.学员能熟练掌握字典常用操作，并了解其他工厂方法

## 引子

之前我们已经学过了字典和元组，我们可以把全班同学的名字保存在列表中，并能够对这些名字进行增删改查了。现在我们又有了一个新的需求，我们不仅要保存每个同学的姓名，还想要保存他的年龄、身高等等。应该如何保存呢？

这里可以引导学生像组合列表这里思考：\[\[name,age,high\],\[\],……,\[\]\]

但是这样就有一个问题，如果我们想修改某一个同学的信息，需要遍历整个列表，这种方式非常麻烦。

当然我们也可以用index寻找这个学员的信息，但是前提是我们必须知道这个学员的姓名年龄和身高，这样我们使用这个列表的成本就太高了。。。

这个时候就需要有新的数据类型来支撑我们的需求。

## 字典的定义与特性

字典是Python语言中唯一的映射类型。

**定义：**｛key1:value1,key2:value2｝

```
1、键与值用冒号“：”分开；
2、项与项用逗号“，”分开；
```

**特性：**

```
1.key-value结构
2.key必须可hash、且必须为不可变数据类型、必须唯一
3.可存放任意多个值、可修改、可以不唯一
4.无序
```

## 字典的创建与常见操作

**字典的创建**

```py
person = {"name": "alex", 'age': 20}
#或
person = dict(name='seven', age=20)
#或
person = dict({"name": "egon", 'age': 20})
#或

person = dict((['name','苑昊'],['文周',18]))
{}.fromkeys(seq,100) #不指定100默认为None
#注意
>>> dic={}.fromkeys(['k1','k2'],[])
>>> dic
{'k1': [], 'k2': []}
>>> dic['k1'].append(1)
>>> dic
{'k1': [1], 'k2': [1]}
```

**字典的常见操作**

```py
键、值、键值对
　　　　1、dic.keys() 返回一个包含字典所有KEY的列表；
　　　　2、dic.values() 返回一个包含字典所有value的列表；
　　　　3、dic.items() 返回一个包含所有（键，值）元祖的列表；
　　　　4、dic.iteritems()、dic.iterkeys()、dic.itervalues() 与它们对应的非迭代方法一样，不同的是它们返回一个迭代子，而不是一个列表；
新增
　　　　1、dic['new_key'] = 'new_value'；
　　　　2、dic.setdefault(key, None) ,如果字典中不存在Key键，由 dic[key] = default 为它赋值；_
删除
　　　　1、dic.pop(key[,default]) 和get方法相似。如果字典中存在key，删除并返回key对应的vuale；如果key不存在，且没有给出default的值，则引发keyerror异常；
　　　　2、dic.clear() 删除字典中的所有项或元素；    
修改
　　　　1、dic['key'] = 'new_value',如果key在字典中存在，'new_value'将会替代原来的value值；
　　　　2、dic.update(dic2) 将字典dic2的键值对添加到字典dic中
查看
　　　　1、dic['key']，返回字典中key对应的值，若key不存在字典中，则报错；
　　　　2、dict.get(key, default = None) 返回字典中key对应的值，若key不存在字典中，则返回default的值（default默认为None）
循环
　　　　1、for k in dic.keys()
　　　　2、for k,v in dic.items()
　　　　3、for k in dic
长度
　　　　1、len(dic)
```

## 字典的工厂函数

```py
class dict(object):
    """
    dict() -> new empty dictionary
    dict(mapping) -> new dictionary initialized from a mapping object's
        (key, value) pairs
    dict(iterable) -> new dictionary initialized as if via:
        d = {}
        for k, v in iterable:
            d[k] = v
    dict(**kwargs) -> new dictionary initialized with the name=value pairs
        in the keyword argument list.  For example:  dict(one=1, two=2)
    """
    def clear(self): # real signature unknown; restored from __doc__
        """ D.clear() -> None.  Remove all items from D. """
        pass

    def copy(self): # real signature unknown; restored from __doc__
        """ D.copy() -> a shallow copy of D """
        pass

    @staticmethod # known case
    def fromkeys(*args, **kwargs): # real signature unknown
        """ Returns a new dict with keys from iterable and values equal to value. """
        pass

    def get(self, k, d=None): # real signature unknown; restored from __doc__
        """ D.get(k[,d]) -> D[k] if k in D, else d.  d defaults to None. """
        pass

    def items(self): # real signature unknown; restored from __doc__
        """ D.items() -> a set-like object providing a view on D's items """
        pass

    def keys(self): # real signature unknown; restored from __doc__
        """ D.keys() -> a set-like object providing a view on D's keys """
        pass

    def pop(self, k, d=None): # real signature unknown; restored from __doc__
        """
        D.pop(k[,d]) -> v, remove specified key and return the corresponding value.
        If key is not found, d is returned if given, otherwise KeyError is raised
        """
        pass

    def popitem(self): # real signature unknown; restored from __doc__
        """
        D.popitem() -> (k, v), remove and return some (key, value) pair as a
        2-tuple; but raise KeyError if D is empty.
        """
        pass

    def setdefault(self, k, d=None): # real signature unknown; restored from __doc__
        """ D.setdefault(k[,d]) -> D.get(k,d), also set D[k]=d if k not in D """
        pass

    def update(self, E=None, **F): # known special case of dict.update
        """
        D.update([E, ]**F) -> None.  Update D from dict/iterable E and F.
        If E is present and has a .keys() method, then does:  for k in E: D[k] = E[k]
        If E is present and lacks a .keys() method, then does:  for k, v in E: D[k] = v
        In either case, this is followed by: for k in F:  D[k] = F[k]
        """
        pass

    def values(self): # real signature unknown; restored from __doc__
        """ D.values() -> an object providing a view on D's values """
        pass

....略....
```



