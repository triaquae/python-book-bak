### 七 \_\_setitem\_\_,\_\_getitem\_\_,\_\_delitem\_\_

```py
class Foo:
    def __init__(self,name):
        self.name=name

    def __getitem__(self, item):
        print(self.__dict__[item])

    def __setitem__(self, key, value):
        self.__dict__[key]=value
    def __delitem__(self, key):
        print('del obj[key]时,我执行')
        self.__dict__.pop(key)
    def __delattr__(self, item):
        print('del obj.key时,我执行')
        self.__dict__.pop(item)

f1=Foo('sb')
f1['age']=18
f1['age1']=19
del f1.age1
del f1['age']
f1['name']='alex'
print(f1.__dict__)
```

### 八 \_\_str\_\_,\_\_repr\_\_,\_\_format\_\_

改变对象的字符串显示\_\_str\_\_,\_\_repr\_\_  
自定制格式化字符串\_\_format\_\_

```py
#_*_coding:utf-8_*_
__author__ = 'Linhaifeng'
format_dict={
    'nat':'{obj.name}-{obj.addr}-{obj.type}',#学校名-学校地址-学校类型
    'tna':'{obj.type}:{obj.name}:{obj.addr}',#学校类型:学校名:学校地址
    'tan':'{obj.type}/{obj.addr}/{obj.name}',#学校类型/学校地址/学校名
}
class School:
    def __init__(self,name,addr,type):
        self.name=name
        self.addr=addr
        self.type=type

    def __repr__(self):
        return 'School(%s,%s)' %(self.name,self.addr)
    def __str__(self):
        return '(%s,%s)' %(self.name,self.addr)

    def __format__(self, format_spec):
        # if format_spec
        if not format_spec or format_spec not in format_dict:
            format_spec='nat'
        fmt=format_dict[format_spec]
        return fmt.format(obj=self)

s1=School('oldboy1','北京','私立')
print('from repr: ',repr(s1))
print('from str: ',str(s1))
print(s1)

'''
str函数或者print函数--->obj.__str__()
repr或者交互式解释器--->obj.__repr__()
如果__str__没有被定义,那么就会使用__repr__来代替输出
注意:这俩方法的返回值必须是字符串,否则抛出异常
'''
print(format(s1,'nat'))
print(format(s1,'tna'))
print(format(s1,'tan'))
print(format(s1,'asfdasdffd'))
```

**自定义format练习**

```py
date_dic={
    'ymd':'{0.year}:{0.month}:{0.day}',
    'dmy':'{0.day}/{0.month}/{0.year}',
    'mdy':'{0.month}-{0.day}-{0.year}',
}
class Date:
    def __init__(self,year,month,day):
        self.year=year
        self.month=month
        self.day=day

    def __format__(self, format_spec):
        if not format_spec or format_spec not in date_dic:
            format_spec='ymd'
        fmt=date_dic[format_spec]
        return fmt.format(self)

d1=Date(2016,12,29)
print(format(d1))
print('{:mdy}'.format(d1))
```

**issubclass和isinstance**

```py
#_*_coding:utf-8_*_
__author__ = 'Linhaifeng'

class A:
    pass

class B(A):
    pass

print(issubclass(B,A)) #B是A的子类,返回True

a1=A()
print(isinstance(a1,A)) #a1是A的实例
```

### 九 **slots**

**slots使用**

```py
'''
1.__slots__是什么:是一个类变量,变量值可以是列表,元祖,或者可迭代对象,也可以是一个字符串(意味着所有实例只有一个数据属性)
2.引子:使用点来访问属性本质就是在访问类或者对象的__dict__属性字典(类的字典是共享的,而每个实例的是独立的)
3.为何使用__slots__:字典会占用大量内存,如果你有一个属性很少的类,但是有很多实例,为了节省内存可以使用__slots__取代实例的__dict__
当你定义__slots__后,__slots__就会为实例使用一种更加紧凑的内部表示。实例通过一个很小的固定大小的数组来构建,而不是为每个实例定义一个
字典,这跟元组或列表很类似。在__slots__中列出的属性名在内部被映射到这个数组的指定小标上。使用__slots__一个不好的地方就是我们不能再给
实例添加新的属性了,只能使用在__slots__中定义的那些属性名。
4.注意事项:__slots__的很多特性都依赖于普通的基于字典的实现。另外,定义了__slots__后的类不再 支持一些普通类特性了,比如多继承。大多数情况下,你应该
只在那些经常被使用到 的用作数据结构的类上定义__slots__比如在程序中需要创建某个类的几百万个实例对象 。
关于__slots__的一个常见误区是它可以作为一个封装工具来防止用户给实例增加新的属性。尽管使用__slots__可以达到这样的目的,但是这个并不是它的初衷。           更多的是用来作为一个内存优化工具。

'''
class Foo:
    __slots__='x'


f1=Foo()
f1.x=1
f1.y=2#报错
print(f1.__slots__) #f1不再有__dict__

class Bar:
    __slots__=['x','y']

n=Bar()
n.x,n.y=1,2
n.z=3#报错
```

**刨根问底**

```py
class Foo:
    __slots__=['name','age']

f1=Foo()
f1.name='alex'
f1.age=18
print(f1.__slots__)

f2=Foo()
f2.name='egon'
f2.age=19
print(f2.__slots__)

print(Foo.__dict__)
#f1与f2都没有属性字典__dict__了,统一归__slots__管,节省内存
```

### 十 \_\_next\_\_和\_\_iter\_\_实现迭代器协议

**简单示范**

```py
#_*_coding:utf-8_*_
__author__ = 'Linhaifeng'
class Foo:
    def __init__(self,x):
        self.x=x

    def __iter__(self):
        return self

    def __next__(self):
        n=self.x
        self.x+=1
        return self.x

f=Foo(3)
for i in f:
    print(i)
```

```py
class Foo:
    def __init__(self,start,stop):
        self.num=start
        self.stop=stop
    def __iter__(self):
        return self
    def __next__(self):
        if self.num >= self.stop:
            raise StopIteration
        n=self.num
        self.num+=1
        return n

f=Foo(1,5)
from collections import Iterable,Iterator
print(isinstance(f,Iterator))

for i in Foo(1,5):
    print(i)
```

**练习：简单模拟range，加上步长**

```py
class Range:
    def __init__(self,n,stop,step):
        self.n=n
        self.stop=stop
        self.step=step

    def __next__(self):
        if self.n >= self.stop:
            raise StopIteration
        x=self.n
        self.n+=self.step
        return x

    def __iter__(self):
        return self

for i in Range(1,7,3): #
    print(i)
```

**斐波那契数列**

```py
class Fib:
    def __init__(self):
        self._a=0
        self._b=1

    def __iter__(self):
        return self

    def __next__(self):
        self._a,self._b=self._b,self._a + self._b
        return self._a

f1=Fib()

print(f1.__next__())
print(next(f1))
print(next(f1))

for i in f1:
    if i > 100:
        break
    print('%s ' %i,end='')
```

### 十一 \_\_doc\_\_

**它类的描述信息**

```py
class Foo:
    '我是描述信息'
    pass

print(Foo.__doc__)
```

**该属性无法被继承**

```py
class Foo:
    '我是描述信息'
    pass

class Bar(Foo):
    pass
print(Bar.__doc__) #该属性无法继承给子类
```

### 十二 \_\_module\_\_和\_\_class\_\_

\_\_module\_\_ 表示当前操作的对象在那个模块

\_\_class\_\_ 表示当前操作的对象的类是什么  

**lib/aa.py**

```py
#!/usr/bin/env python
# -*- coding:utf-8 -*-

class C:

    def __init__(self):
        self.name = ‘SB'
```

**index.py**

```
from lib.aa import C

obj = C()
print obj.__module__  # 输出 lib.aa，即：输出模块
print obj.__class__      # 输出 lib.aa.C，即：输出类
```

### 十三  \_\_del\_\_

析构方法，当对象在内存中被释放时，自动触发执行。

注：如果产生的对象仅仅只是python程序级别的（用户级），那么无需定义\_\_del\_\_,如果产生的对象的同时还会向操作系统发起系统调用，即一个对象有用户级与内核级两种资源，比如（打开一个文件，创建一个数据库链接），则必须在清除对象的同时回收系统资源，这就用到了\_\_del\_\_。 
 
**简单示范**

```py
class Foo:

    def __del__(self):
        print('执行我啦')

f1=Foo()
del f1
print('------->')

#输出结果
执行我啦
------->
```

**挖坑埋了你**

```py
class Foo:

    def __del__(self):
        print('执行我啦')

f1=Foo()
# del f1
print('------->')

#输出结果
------->
执行我啦


#为何啊？？？
```

典型的应用场景：

创建数据库类，用该类实例化出数据库链接对象，对象本身是存放于用户空间内存中，而链接则是由操作系统管理的，存放于内核空间内存中

当程序结束时，python只会回收自己的内存空间，即用户态内存，而操作系统的资源则没有被回收，这就需要我们定制\_\_del\_\_，在对象被删除前向操作系统发起关闭数据库链接的系统调用，回收资源

这与文件处理是一个道理：

```py
f=open('a.txt') #做了两件事，在用户空间拿到一个f变量，在操作系统内核空间打开一个文件
del f #只回收用户空间的f，操作系统的文件还处于打开状态

#所以我们应该在del f之前保证f.close()执行,即便是没有del，程序执行完毕也会自动del清理资源，于是文件操作的正确用法应该是
f=open('a.txt')
读写...
f.close()
很多情况下大家都容易忽略f.close,这就用到了with上下文管理
```

### 十四 \_\_enter\_\_和\_\_exit\_\_

我们知道在操作文件对象的时候可以这么写

```py
with open('a.txt') as f:
　　'代码块'
```

上述叫做上下文管理协议，即with语句，为了让一个对象兼容with语句，必须在这个对象的类中声明\_\_enter\_\_和\_\_exit\_\_方法  

**上下文管理协议**

```py
class Open:
    def __init__(self,name):
        self.name=name

    def __enter__(self):
        print('出现with语句,对象的__enter__被触发,有返回值则赋值给as声明的变量')
        # return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        print('with中代码块执行完毕时执行我啊')


with Open('a.txt') as f:
    print('=====>执行代码块')
    # print(f,f.name)
```

\_\_exit\_\_\(\)中的三个参数分别代表异常类型，异常值和追溯信息,with语句中代码块出现异常，则with后的代码都无法执行

```py
class Open:
    def __init__(self,name):
        self.name=name

    def __enter__(self):
        print('出现with语句,对象的__enter__被触发,有返回值则赋值给as声明的变量')

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('with中代码块执行完毕时执行我啊')
        print(exc_type)
        print(exc_val)
        print(exc_tb)



with Open('a.txt') as f:
    print('=====>执行代码块')
    raise AttributeError('***着火啦,救火啊***')
print('0'*100) #------------------------------->不会执行
```

如果\_\_exit\(\)返回值为True,那么异常会被清空，就好像啥都没发生一样，with后的语句正常执行

```py
class Open:
    def __init__(self,name):
        self.name=name

    def __enter__(self):
        print('出现with语句,对象的__enter__被触发,有返回值则赋值给as声明的变量')

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('with中代码块执行完毕时执行我啊')
        print(exc_type)
        print(exc_val)
        print(exc_tb)
        return True



with Open('a.txt') as f:
    print('=====>执行代码块')
    raise AttributeError('***着火啦,救火啊***')
print('0'*100) #------------------------------->会执行
```

**练习：模拟Open**

```py
class Open:
    def __init__(self,filepath,mode='r',encoding='utf-8'):
        self.filepath=filepath
        self.mode=mode
        self.encoding=encoding

    def __enter__(self):
        # print('enter')
        self.f=open(self.filepath,mode=self.mode,encoding=self.encoding)
        return self.f

    def __exit__(self, exc_type, exc_val, exc_tb):
        # print('exit')
        self.f.close()
        return True
    def __getattr__(self, item):
        return getattr(self.f,item)

with Open('a.txt','w') as f:
    print(f)
    f.write('aaaaaa')
    f.wasdf #抛出异常，交给__exit__处理
```

用途或者说好处：

1. 使用with语句的目的就是把代码块放入with中执行，with结束后，自动完成清理工作，无须手动干预

2. 在需要管理一些资源比如文件，网络连接和锁的编程环境中，可以在\_\_exit\_\_中定制自动释放资源的机制，你无须再去关系这个问题，这将大有用处

### 十五 \_\_call\_\_

对象后面加括号，触发执行。

注：构造方法的执行是由创建对象触发的，即：对象 = 类名\(\) ；而对于 \_\_call\_\_ 方法的执行是由对象后加括号触发的，即：对象\(\) 或者 类\(\)\(\)

```py
class Foo:

    def __init__(self):
        pass

    def __call__(self, *args, **kwargs):

        print('__call__')


obj = Foo() # 执行 __init__
obj()       # 执行 __call__
```



