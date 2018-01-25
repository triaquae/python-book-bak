## 本节重点

* 了解元类
* 了解元类的用途

> **本节时长需控制在45分钟内**

### 一 知识储备

```python
exec：三个参数

参数一：字符串形式的命令

参数二：全局作用域（字典形式），如果不指定，默认为globals()

参数三：局部作用域（字典形式），如果不指定，默认为locals()
```

**exec的使用**

```py
#可以把exec命令的执行当成是一个函数的执行，会将执行期间产生的名字存放于局部名称空间中
g={
'x':1,
'y':2
}
l={}

exec('''
global x,z
x=100
z=200

m=300
''',g,l)

print(g) #{'x': 100, 'y': 2,'z':200,......}
print(l) #{'m': 300}
```

### 二 引子（类也是对象）

```py
class Foo:
      pass

f1=Foo() #f1是通过Foo类实例化的对象
```

python中一切皆是对象，类本身也是一个对象，当使用关键字class的时候，python解释器在加载class的时候就会创建一个对象\(这里的对象指的是类而非类的实例\)，因而我们可以将类当作一个对象去使用，同样满足第一类对象的概念，可以：

把类赋值给一个变量

把类作为函数参数进行传递

把类作为函数的返回值

在运行时动态地创建类

上例可以看出f1是由Foo这个类产生的对象，而Foo本身也是对象，那它又是由哪个类产生的呢？

```py
#type函数可以查看类型，也可以用来查看对象的类，二者是一样的
print(type(f1)) # 输出：<class '__main__.Foo'> 表示，obj 对象由Foo类创建
print(type(Foo)) # 输出：<type 'type'>
```

### 三 什么是元类？

元类是类的类，是类的模板

元类是用来控制如何创建类的，正如类是创建对象的模板一样，而元类的主要目的是为了控制类的创建行为

元类的实例化的结果为我们用class定义的类，正如类的实例为对象\(f1对象是Foo类的一个实例，Foo类是 type 类的一个实例\)

type是python的一个内建元类，用来直接控制生成类，python中任何class定义的类其实都是type类实例化的对象  
!\[image\_1c1p03hmh198t1skn1ulrps57h19.png-80.6kB\]\[1\]

### 四 创建类的两种方式

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

**方式二：就是手动模拟class创建类的过程）：将创建类的步骤拆分开，手动去创建**

```
#准备工作：

#创建类主要分为三部分

　　1 类名

　　2 类的父类

　　3 类体


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

步骤一（先处理类体-&gt;名称空间）：类体定义的名字都会存放于类的名称空间中（一个局部的名称空间），我们可以事先定义一个空字典，然后用exec去执行类体的代码（exec产生名称空间的过程与真正的class过程类似，只是后者会将\_\_开头的属性变形），生成类的局部名称空间，即填充字典

```
class_dic={}
exec(class_body,globals(),class_dic)


print(class_dic)
#{'country': 'China', 'talk': <function talk at 0x101a560c8>, '__init__': <function __init__ at 0x101a56668>}
```

步骤二：调用元类type（也可以自定义）来产生类Chinense

```
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

### 五 自定义元类控制类的行为

```
#一个类没有声明自己的元类，默认他的元类就是type，除了使用元类type，用户也可以通过继承type来自定义元类（顺便我们也可以瞅一瞅元类如何控制类的行为，工作流程是什么）
```

**egon5步带你学会元类**

```
#！！！如果你拷贝不注明出处的话，以后老子都不写了！！！

#知识储备：
    #产生的新对象 = object.__new__(继承object类的子类)

#步骤一：如果说People=type(类名,类的父类们,类的名称空间)，那么我们定义元类如下，来控制类的创建
class Mymeta(type):  # 继承默认元类的一堆属性
    def __init__(self, class_name, class_bases, class_dic):
        if '__doc__' not in class_dic or not class_dic.get('__doc__').strip():
            raise TypeError('必须为类指定文档注释')

        if not class_name.istitle():
            raise TypeError('类名首字母必须大写')

        super(Mymeta, self).__init__(class_name, class_bases, class_dic)


class People(object, metaclass=Mymeta):
    country = 'China'

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def talk(self):
        print('%s is talking' % self.name)

#步骤二：如果我们想控制类实例化的行为，那么需要先储备知识__call__方法的使用
class People(object,metaclass=type):
    def __init__(self,name,age):
        self.name=name
        self.age=age

    def __call__(self, *args, **kwargs):
        print(self,args,kwargs)


# 调用类People，并不会出发__call__
obj=People('egon',18)

# 调用对象obj(1,2,3,a=1,b=2,c=3)，才会出发对象的绑定方法obj.__call__(1,2,3,a=1,b=2,c=3)
obj(1,2,3,a=1,b=2,c=3) #打印：<__main__.People object at 0x10076dd30> (1, 2, 3) {'a': 1, 'b': 2, 'c': 3}

#总结：如果说类People是元类type的实例，那么在元类type内肯定也有一个__call__，会在调用People('egon',18)时触发执行，然后返回一个初始化好了的对象obj

#步骤三：自定义元类，控制类的调用（即实例化）的过程
class Mymeta(type): #继承默认元类的一堆属性
    def __init__(self,class_name,class_bases,class_dic):
        if not class_name.istitle():
            raise TypeError('类名首字母必须大写')

        super(Mymeta,self).__init__(class_name,class_bases,class_dic)

    def __call__(self, *args, **kwargs):
        #self=People
        print(self,args,kwargs) #<class '__main__.People'> ('egon', 18) {}

        #1、实例化People，产生空对象obj
        obj=object.__new__(self)


        #2、调用People下的函数__init__，初始化obj
        self.__init__(obj,*args,**kwargs)


        #3、返回初始化好了的obj
        return obj

class People(object,metaclass=Mymeta):
    country='China'

    def __init__(self,name,age):
        self.name=name
        self.age=age

    def talk(self):
        print('%s is talking' %self.name)

obj=People('egon',18)
print(obj.__dict__) #{'name': 'egon', 'age': 18}

#步骤四：
class Mymeta(type): #继承默认元类的一堆属性
    def __init__(self,class_name,class_bases,class_dic):
        if not class_name.istitle():
            raise TypeError('类名首字母必须大写')

        super(Mymeta,self).__init__(class_name,class_bases,class_dic)

    def __call__(self, *args, **kwargs):
        #self=People
        print(self,args,kwargs) #<class '__main__.People'> ('egon', 18) {}

        #1、调用self，即People下的函数__new__，在该函数内完成：1、产生空对象obj 2、初始化 3、返回obj
        obj=self.__new__(self,*args,**kwargs)

        #2、一定记得返回obj，因为实例化People(...)取得就是__call__的返回值
        return obj

class People(object,metaclass=Mymeta):
    country='China'

    def __init__(self,name,age):
        self.name=name
        self.age=age

    def talk(self):
        print('%s is talking' %self.name)

    def __new__(cls, *args, **kwargs):
        obj=object.__new__(cls)
        cls.__init__(obj,*args,**kwargs)
        return obj

obj=People('egon',18)
print(obj.__dict__) #{'name': 'egon', 'age': 18}

#步骤五：基于元类实现单例模式,比如数据库对象,实例化时参数都一样,就没必要重复产生对象,浪费内存
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

### 六 练习题

**练习一：在元类中控制把自定义类的数据属性都变成大写**

```
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

**练习二：在元类中控制自定义的类无需init方法**

1.元类帮其完成创建对象，以及初始化操作；  
　　2.要求实例化时传参必须为关键字形式，否则抛出异常TypeError: must use keyword argument  
　　3.key作为用户自定义类产生对象的属性，且所有属性变成大写

```
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

[1]: [http://static.zybuluo.com/agocan/1rt5gasw99sxveikp3fxsoeg/image\_1c1p03hmh198t1skn1ulrps57h19.png](http://static.zybuluo.com/agocan/1rt5gasw99sxveikp3fxsoeg/image_1c1p03hmh198t1skn1ulrps57h19.png)

