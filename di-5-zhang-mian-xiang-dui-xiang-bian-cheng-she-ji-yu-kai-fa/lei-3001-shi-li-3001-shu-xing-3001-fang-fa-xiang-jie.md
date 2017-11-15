## 本节重点：

* 使学员了解面向对象语法使用

> **本节时长需控制在60分钟内**

### 类的语法

![](/assets\chapter5/class_define.png)

上面的代码其实有问题，属性名字和年龄都写死了，想传名字传不进去。

```py
class Person(object):

    def __init__(self, name, age):
        self.name = name
        self.age = age


p = Person("Alex", 22)
print(p.name, p.age)
```

为什么有\_\_init\_\_? 为什么有self? 此时的你一脸蒙逼，相信不画个图，你的智商是理解不了的！

画图之前， 你先注释掉这两句

```py
# p = Person("Alex", 22)
# print(p.name, p.age)

#加上句
print(Person)
```

```
#执行结果
<class '__main__.Person'>
```

这代表什么?代表 即使不实例化，这个Person类本身也是已经存在内存里的对不对， yes, cool，那实例化时，会产生什么化学反应呢？![](/assets\chapter5/class_实例化.png)

根据上图我们得知，**其实self,就是实例本身！你实例化时python解释器会自动把这个实例本身通过self参数传进去。**

你说好吧，假装懂了，但是这么干有什么好处呢？想了解self的好处，得给Person类加个功能

```py
class Person(object):

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def talk(self):
        print("Hello, my name is %s, I'm %s years old!" % (self.name, self.age))

p = Person("Alex", 22)
# print(p.name, p.age)
p.talk() #注意这里调用并未传递参数
```

执行输出

```
Hello, my name is Alex, I'm 22 years old!
```

**为何p.talk\(\)未传参数不报错，且为何talk方法定义要跟一个self参数？**

我们上面讲到self其实是实例本身， 那p.talk\(\) 其实相当于p.talk\(p\),你不需要自己把p实例传进去，解释器帮你干了，那为何要在talk定义时加self参数呢？

是因为，你的talk方法里有调用到实例的属性呀，这些属性又都是绑定在实例上的，你想调用实例属性，就必须要把实例传进去。

**构造方法**

`__init__(...)`被称为 构造方法或初始化方法，在例实例化过程中自动执行，目的是初始化实例的一些属性。每个实例通过\_\_init\_\_初始化的属性都是独有的

刚才定义的这个类体现了面向对象的第一个基本特性，**封装，其实就是使用构造方法将内容封装到某个具体对象中，然后通过对象直接或者self间接获取被封装的内容**

了解了基本定义，下面详解下类的方法和属性

### 类的方法

**构造方法**

刚才上面已经说了，主要作用是实例化时给实例一些初始化参数，或执行一些其它的初始化工作，总之，因为这个\_\_init\_\_只要一实例化，就会自动执行，so不管你在这个方法里写什么，它都会统统在实例化时执行一遍

**普通方法**

定义类的一些正常功能，比如人这个类， 可以说话、走路、吃饭等，每个方法其实想当于一个功能或动作

**析构方法\(解构方法\)**

实例在内存中被删除时，会自动执行这个方法，如你在内存里生成了一个人的实例，现在他被打死了，那这个人除了自己的实例要被删除外，可能它在实例外产生的一些痕迹也要清除掉，清除的动作就可以写在这个方法里

```py
class Person(object):

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def talk(self):
        print("Hello, my name is %s, I'm %s years old!" % (self.name, self.age))

    def __del__(self):
        print("running del method, this person must be died.")


p = Person("Alex", 22)
p.talk()

del p

print('--end program--')
```



