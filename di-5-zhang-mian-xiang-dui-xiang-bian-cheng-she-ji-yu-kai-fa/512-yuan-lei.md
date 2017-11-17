### 本节重点

* 了解元类
* 了解元类的用途

> ### **本节时长需控制在45分钟内**

### 知识储备

exec：三个参数

参数一：字符串形式的命令

参数二：全局作用域

参数三：局部作用域

exec会在指定的局部作用域内执行字符串内的代码，除非明确地使用global关键字

```py
g={
    'x':1,
    'y':2,
    'teachers':{'egon','alex','yuanhao','wupeiqi'}
}
l={'birds':[1,2,3]}

# exec("""
# def func():
#     global x
#     x='egon'
# func()
# """,g,l)
# print(g)
# print(l)

exec("""
global x
x='egon'
""",g,l)
print(g)
print(l
```

### 引子

```py
class Foo:
    pass

f1=Foo() #f1是通过Foo类实例化的对象
```

python中一切皆是对象，类本身也是一个对象，当使用关键字class的时候，python解释器在加载class的时候就会创建一个对象\(这里的对象指的是类而非类的实例\)，因而我们可以将类当作一个对象去使用，同样满足第一类对象的概念，可以：

* 把类赋值给一个变量

* 把类作为函数参数进行传递

* 把类作为函数的返回值

* 在运行时动态地创建类 

上例可以看出f1是由Foo这个类产生的对象，而Foo本身也是对象，那它又是由哪个类产生的呢？

```py
#type函数可以查看类型，也可以用来查看对象的类，二者是一样的
print(type(f1)) # 输出：<class '__main__.Foo'>     表示，obj 对象由Foo类创建
print(type(Foo)) # 输出：<type 'type'>  
```

### 什么是元类

元类是类的类，是类的模板

元类是用来控制如何创建类的，正如类是创建对象的模板一样，而**元类的主要目的是为了控制类的创建行为**

元类的实例化的结果为我们用class定义的类，正如类的实例为对象\(f1**对象是Foo类的一个实例**，**Foo类是 type 类的一个实例**\)

type是python的一个内建元类，用来直接控制生成类，python中任何class定义的类其实都是type类实例化的对象

![](/assets/什么是元类.png)

### 创建类的两种方式

**方式一：使用class关键字**

```py
class Chinese(object):
    country='China'
    def __init__(self,name,age):
        self.name=name
        self.age=age
    def talk(self):
        print('%s is talking' %self.name)
```

**方式二（就是手动模拟class创建类的过程）：将创建类的步骤拆分开，手动去创建**

1、准备工作：

    创建类主要分为三部分

　　    1 类名

　　    2 类的父类

　　    3 类体

```py
#类名
class_name='Chinese'
#类的父类
class_bases=(object,)
#类体
class_body="""
country='China'
def __init__(self,name,age):
    self.name=name
    self.age=age
def talk(self):
    print('%s is talking' %self.name)
"""
```

2、先处理类体-&gt;名称空间：类体定义的名字都会存放于类的名称空间中（一个局部的名称空间），我们可以事先定义一个空字典，然后用exec去执行类体的代码（exec产生名称空间的过程与真正的class过程类似，只是后者会将\_\_开头的属性变形），生成类的局部名称空间，即填充字典

```py
class_dic={}
exec(class_body,globals(),class_dic)

print(class_dic)
#{'country': 'China', 'talk': <function talk at 0x101a560c8>, '__init__': <function __init__ at 0x101a56668>}
```

3、调用元类type（也可以自定义）来产生类Chinense

```py
Foo=type(class_name,class_bases,class_dic) #实例化type得到对象Foo，即我们用class定义的类Foo

print(Foo)
print(type(Foo))
print(isinstance(Foo,type))
'''
<class '__main__.Chinese'>
<class 'type'>
True
'''
```

我们看到，type 接收三个参数：

* 第 1 个参数是字符串 ‘Foo’，表示类名

* 第 2 个参数是元组 \(object, \)，表示所有的父类

* 第 3 个参数是字典，这里是一个空字典，表示没有定义属性和方法

补充：若Foo类有继承，即class Foo\(Bar\):.... 则等同于type\('Foo',\(Bar,\),{}\)



**一个类没有声明自己的元类，默认他的元类就是type，除了使用元类type，用户也可以通过继承type来自定义元类（顺便我们也可以瞅一瞅元类如何控制类的行为，工作流程是什么）**

所有类实例化的流程都一样，与三个方法有关

1. 任何名字后加括号,都是在调用一个功能,触发一个函数的执行,得到一个返回值,类或对象加括号触发的是\_\_call\_\_的运行
2. \_\_new\_\_更像是其他语言中的构造函数,必须有返回值,返回值就实例化的对象
3. \_\_init\_\_只是初始化函数,必须没有返回值,仅仅只是初始化功能,并不能new创建对象

前提注意：

1. 在我们自定义的元类内，\_\_new\_\_方法在产生obj时用type.\_\_new\_\_\(cls,\*args,\*\*kwargs\),用object.\_\_new\_\_\(cls\)抛出异常：TypeError: object.\_\_new\_\_\(Mymeta\) is not safe, use type.\_\_new\_\_\(\)
2. 在我们自定义的类内，\_\_new\_\_方法在产生obj时用object.\_\_new\_\_\(self\)

### 元类控制类的实例化过程

```py
#元类控制类的实例化过程：
    1 类()，调用元类.__call__()
    2 在1的方法中调用：
        类.__new__() #返回类的对象obj
        类.__init__(obj,...) #为对象进行初始化
```

不指定元类的情况

```py
#不指定元类的情况：没有指定元类，则默认用type作为元类，Foo()则触发type.__call__()
#然后在call内
#先调用Foo.__new__()产生空对象obj
#再调用Foo.__init__(obj,...)为空对象obj进行初始化

class Foo:
    x=1
    y=2
    def __init__(self,name,age,sex): #将__new__产生的空对象传给self
        self.name=name
        self.age=age
        self.sex=sex

    def __new__(cls, *args, **kwargs): #该方法的返回值即Foo('egon',18,'male')的返回值
        '''
        在此处可以处理cls的属性
        args与kwargs为调用Foo括号内传的值
        '''

        # return 123 #则f为123
        return object.__new__(cls) #f为对象<__main__.Foo object at 0x10fc6e668>

f=Foo('egon',18,'male')
print(f)
print(f.__dict__)

<__main__.Foo object at 0x108b246a0>
{'name': 'egon', 'age': 18, 'sex': 'male'}
```

指定元类为Mymeta的情况

```py
#指定元类为Mymeta的情况：Foo()则触发Mymeta.__call__()，我们需要在我们自定义的元类内实现__call__
#然后在call内
#先调用Foo.__new__()产生空对象obj
#再调用Foo.__init__(obj,...)为空对象obj进行初始化

class Mymeta(type):

    def __call__(self, *args, **kwargs):
        '''
        self为类Foo,即Foo只是元类的一个实例
        args与kwargs为调用Foo括号内传入的参数
        此时
        args=('egon', 18, 'male')
        kwargs={}
        '''
        #先产生Foo的空对象
        obj_of_Foo=self.__new__(self,*args,**kwargs) #Foo.__new__(Foo,'egon', 18, 'male')
        #再对空对象进行初始化
        self.__init__(obj_of_Foo,*args,**kwargs) #Foo.__init__(obj_of_Foo,'egon', 18, 'male')
        #最后返回初始化后的Foo的对象,作为调用Foo的返回值赋值给f
        return obj_of_Foo
class Foo(metaclass=Mymeta):
    x=1
    y=2
    def __init__(self,name,age,sex): #将__new__产生的空对象传给self
        self.name=name
        self.age=age
        self.sex=sex

    def __new__(cls, *args, **kwargs): #该方法的返回值即Foo('egon',18,'male')的返回值
        '''
        在此处可以处理cls的属性
        args与kwargs为调用Foo括号内传的值
        '''
        # return 123 #则f为123
        return object.__new__(cls) #f为对象<__main__.Foo object at 0x10fc6e668>

f=Foo('egon',18,'male')
print(f)
print(f.__dict__)

<__main__.Foo object at 0x10750a630>
{'name': 'egon', 'age': 18, 'sex': 'male'}
```

应用举例：基于元类实现单例模式

```py
#单例模式,比如数据库对象,实例化时参数都一样,就没必要重复产生对象,浪费内存
class Mysql:
    __instance=None
    def __init__(self,host='127.0.0.1',port='3306'):
        self.host=host
        self.port=port

    @classmethod
    def singleton(cls,*args,**kwargs):
        if not cls.__instance:
            cls.__instance=cls(*args,**kwargs)
        return cls.__instance


obj1=Mysql()
obj2=Mysql()
print(obj1 is obj2) #False

obj3=Mysql.singleton()
obj4=Mysql.singleton()
print(obj3 is obj4) #True

#应用：定制元类实现单例模式
class Mymeta(type):
    def __init__(self,name,bases,dic): #定义类Mysql时就触发
        self.__instance=None
        super().__init__(name,bases,dic)

    def __call__(self, *args, **kwargs): #Mysql(...)时触发

        if not self.__instance:
            self.__instance=object.__new__(self) #产生对象
            self.__init__(self.__instance,*args,**kwargs) #初始化对象
            #上述两步可以合成下面一步
            # self.__instance=super().__call__(*args,**kwargs)

        return self.__instance
class Mysql(metaclass=Mymeta):
    def __init__(self,host='127.0.0.1',port='3306'):
        self.host=host
        self.port=port


obj1=Mysql()
obj2=Mysql()

print(obj1 is obj2)
```

### 元类控制类本身的产生过程

```py
元类Mymeta控制类本身的产生过程：
类=Mymeta()，调用type.__call__()
在1的方法中调用：
        Mymeta.__new__() #返回Mymeta的对象Foo
        Mymeta.__init__(Foo,...) #为对象Foo进行初始化


#提示：
回忆一下默认元类type的处理方式
    Foo=type(类名,父类,字典)
我们自定义的元类也是一样的道理
    Foo=Mymeta(类名,父类,字典)
    即
    Foo=Mymeta(('Foo', (<class 'object'>,), {'__module__': '__main__', '__qualname__': 'Foo'}))


#分析：
Mymeta(...)，括号内自动传固定的值：类名，类继承的父类，类字典
Type.__call__()
    Mymeta.__new__()
    Mymeta.__init__()
```

指定元类只控制类的创建

```py
class Mymeta(type):
    def __init__(self,class_name,class_bases,class_dic):
        '''
        可以在此控制类Foo的属性
        self=<class '__main__.Foo'>
        class_name='Foo'
        class_bases=(<class 'object'>,)
        class_dic={..., 'x': 1, 'y': 2}
        '''


    def __new__(cls, *args, **kwargs):
        '''
        cls为Mymeta
        将调用Mymeta的参数传给type.__call__,然后转交给Mymeta.__new__
        args与kwargs即Mymeta括号内的参数
        args=('Foo', (<class 'object'>,), {..., 'x': 1, 'y': 2})
        kwargs={}
        '''
        obj_of_Mymeta=type.__new__(cls,*args,**kwargs)
        return obj_of_Mymeta #Mymeta的对象即Foo

class Foo(object,metaclass=Mymeta): #Foo=Mymeta(类名,Foo的父类,Foo的字典)
    x=1
    y=2


print(Foo.__dict__)
{...,'x': 1, 'y': 2,...}
```

定制元类，控制类的创建

```py
class Mymeta(type):
    def __init__(self):
        print('__init__')

    def __new__(cls, *args, **kwargs):
        # print('__new__')
        obj=type.__new__(cls,*args,**kwargs)
        return obj

    def __call__(self, *args, **kwargs):
        print('__call__')


Foo=Mymeta()
class Foo(metaclass=Mymeta):
    pass

print(Foo)
'''
基于上述表达,我们改写了__new__,返回obj,但是抛出异常:
TypeError: __init__() takes 1 positional argument but 4 were given

'''


#改写
class Mymeta(type):
    def __init__(self,name,bases,dic):
        print('__init__')

    def __new__(cls, *args, **kwargs):
        print('__new__')
        obj=type.__new__(cls,*args,**kwargs)
        return obj

    def __call__(self, *args, **kwargs):
        print('__call__')


# Foo=Mymeta()
class Foo(metaclass=Mymeta):
    pass

print(Foo)
```

应用：限制类内函数必须有文档注释

```py
class Mymeta(type):
    def __init__(self,name,bases,dic):
        for key,value in dic.items():
            if key.startswith('__'):
                continue
            if not callable(value):
                continue
            if not value.__doc__:
                raise TypeError('%s 必须有文档注释' %key)
        type.__init__(self,name,bases,dic)

    def __new__(cls, *args, **kwargs):
        # print('__new__')
        obj=type.__new__(cls,*args,**kwargs)
        return obj

    def __call__(self, *args, **kwargs):
        # print('__call__')
        pass

# Foo=Mymeta()
class Foo(metaclass=Mymeta):
    def f1(self):
        'from f1'
        pass

    def f2(self):
        pass

'''
抛出异常
TypeError: f2 必须有文档注释
'''
```

### 练习题

**练习一：在元类中控制把自定义类的数据属性都变成大写**

```py
class Mymetaclass(type):
    def __new__(cls,name,bases,attrs):
        update_attrs={}
        for k,v in attrs.items():
            if not callable(v) and not k.startswith('__'):
                update_attrs[k.upper()]=v
            else:
                update_attrs[k]=v
        return type.__new__(cls,name,bases,update_attrs)

class Chinese(metaclass=Mymetaclass):
    country='China'
    tag='Legend of the Dragon' #龙的传人
    def walk(self):
        print('%s is walking' %self.name)


print(Chinese.__dict__)
'''
{'__module__': '__main__',
 'COUNTRY': 'China', 
 'TAG': 'Legend of the Dragon',
 'walk': <function Chinese.walk at 0x0000000001E7B950>,
 '__dict__': <attribute '__dict__' of 'Chinese' objects>,                                         
 '__weakref__': <attribute '__weakref__' of 'Chinese' objects>,
 '__doc__': None}
'''
```

**练习二：在元类中控制自定义的类无需\_\_init\_\_方法**

要求：

　　1.元类帮其完成创建对象，以及初始化操作；

　　2.要求实例化时传参必须为关键字形式，否则抛出异常TypeError: must use keyword argument for key function；

　　3.key作为用户自定义类产生对象的属性，且所有属性变成大写

```py
class Mymetaclass(type):
    # def __new__(cls,name,bases,attrs):
    #     update_attrs={}
    #     for k,v in attrs.items():
    #         if not callable(v) and not k.startswith('__'):
    #             update_attrs[k.upper()]=v
    #         else:
    #             update_attrs[k]=v
    #     return type.__new__(cls,name,bases,update_attrs)

    def __call__(self, *args, **kwargs):
        if args:
            raise TypeError('must use keyword argument for key function')
        obj = object.__new__(self) #创建对象，self为类Foo

        for k,v in kwargs.items():
            obj.__dict__[k.upper()]=v
        return obj

class Chinese(metaclass=Mymetaclass):
    country='China'
    tag='Legend of the Dragon' #龙的传人
    def walk(self):
        print('%s is walking' %self.name)

p=Chinese(name='egon',age=18,sex='male')
print(p.__dict__)
```



