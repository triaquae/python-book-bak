## 本节重点

* 多态与多态性
* 鸭子类型

> **本节时长需控制在15分钟内**

### 多态

多态指的是一类事物有多种形态，比如

动物有多种形态：人，狗，猪

```py
import abc
class Animal(metaclass=abc.ABCMeta): #同一类事物:动物
    @abc.abstractmethod
    def talk(self):
        pass

class People(Animal): #动物的形态之一:人
    def talk(self):
        print('say hello')

class Dog(Animal): #动物的形态之二:狗
    def talk(self):
        print('say wangwang')

class Pig(Animal): #动物的形态之三:猪
    def talk(self):
        print('say aoao')
```

文件有多种形态：文本文件，可执行文件

```py
import abc
class File(metaclass=abc.ABCMeta): #同一类事物:文件
    @abc.abstractmethod
    def click(self):
        pass

class Text(File): #文件的形态之一:文本文件
    def click(self):
        print('open file')

class ExeFile(File): #文件的形态之二:可执行文件
    def click(self):
        print('execute file')
```

### 多态性

一 **什么是多态动态绑定（在继承的背景下使用时，有时也称为多态性）**

多态性是指在不考虑实例类型的情况下使用实例，多态性分为静态多态性和动态多态性

_静态多态性：如任何类型都可以用运算符+进行运算_

_动态多态性：如下_

```py
peo=People()
dog=Dog()
pig=Pig()

#peo、dog、pig都是动物,只要是动物肯定有talk方法
#于是我们可以不用考虑它们三者的具体是什么类型,而直接使用
peo.talk()
dog.talk()
pig.talk()

#更进一步,我们可以定义一个统一的接口来使用
def func(obj):
    obj.talk()
```

**二 为什么要用多态性（多态性的好处）**

其实大家从上面多态性的例子可以看出，我们并没有增加什么新的知识，也就是说python本身就是支持多态性的，这么做的好处是什么呢？

1.增加了程序的灵活性

_　　以不变应万变，不论对象千变万化，使用者都是同一种形式去调用，如func\(animal\)_

2.增加了程序额可扩展性

_　通过继承animal类创建了一个新的类，使用者无需更改自己的代码，还是用func\(animal\)去调用 　　_

```py
>>> class Cat(Animal): #属于动物的另外一种形态：猫
...     def talk(self):
...         print('say miao')
... 
>>> def func(animal): #对于使用者来说，自己的代码根本无需改动
...     animal.talk()
... 
>>> cat1=Cat() #实例出一只猫
>>> func(cat1) #甚至连调用方式也无需改变，就能调用猫的talk功能
say miao

'''
这样我们新增了一个形态Cat，由Cat类产生的实例cat1，使用者可以在完全不需要修改自己代码的情况下。使用和人、狗、猪一样的方式调用cat1的talk方法，即func(cat1)
'''
```

### 鸭子类型

逗比时刻：

Python崇尚鸭子类型，即‘如果看起来像、叫声像而且走起路来像鸭子，那么它就是鸭子’

python程序员通常根据这种行为来编写程序。例如，如果想编写现有对象的自定义版本，可以继承该对象

也可以创建一个外观和行为像，但与它无任何关系的全新对象，后者通常用于保存程序组件的松耦合度。

例1：利用标准库中定义的各种‘与文件类似’的对象，尽管这些对象的工作方式像文件，但他们没有继承内置文件对象的方法

```py
#二者都像鸭子,二者看起来都像文件,因而就可以当文件一样去用
class TxtFile:
    def read(self):
        pass

    def write(self):
        pass

class DiskFile:
    def read(self):
        pass
    def write(self):
        pass
```

例2：序列类型有多种形态：字符串，列表，元组，但他们直接没有直接的继承关系

```py
#str,list,tuple都是序列类型
s=str('hello')
l=list([1,2,3])
t=tuple((4,5,6))

#我们可以在不考虑三者类型的前提下使用s,l,t
s.__len__()
l.__len__()
t.__len__()

len(s)
len(l)
len(t)
```



