## 本节重点

* 掌握类属性与实例属性
* 掌握绑定方法

> **本节时长需控制在20分钟内**

### 属性查找

类有两种属性：数据属性和函数属性

1、类的数据属性是所有对象共享的

```py
#类的数据属性是所有对象共享的,id都一样
print(id(OldboyStudent.school))

print(id(s1.school)) #4377347328
print(id(s2.school)) #4377347328
print(id(s3.school)) #4377347328
```

2、类的函数数据是绑定给对象用的，称为绑定到对象的方法

```py
#类的函数属性是绑定给对象使用的,obj.method称为绑定方法,内存地址都不一样

print(OldboyStudent.learn) #<function OldboyStudent.learn at 0x1021329d8>
print(s1.learn) #<bound method OldboyStudent.learn of <__main__.OldboyStudent object at 0x1021466d8>>
print(s2.learn) #<bound method OldboyStudent.learn of <__main__.OldboyStudent object at 0x102146710>>
print(s3.learn) #<bound method OldboyStudent.learn of <__main__.OldboyStudent object at 0x102146748>>

#ps:id是python的实现机制,并不能真实反映内存地址,如果有内存地址,还是以内存地址为准
```

在obj.name会先从obj自己的名称空间里找name，找不到则去类中找，类也找不到就找父类...最后都找不到就抛出异常

### 绑定方法

定义类并实例化出三个对象

```py
class OldboyStudent:
    school='oldboy'
    def __init__(self,name,age,sex):
        self.name=name
        self.age=age
        self.sex=sex
    def learn(self):
        print('%s is learning' %self.name) #新增self.name

    def eat(self):
        print('%s is eating' %self.name)

    def sleep(self):
        print('%s is sleeping' %self.name)


s1=OldboyStudent('李坦克','男',18)
s2=OldboyStudent('王大炮','女',38)
s3=OldboyStudent('牛榴弹','男',78)
```

类中定义的函数（没有被任何装饰器装饰的）是类的函数属性，类可以使用，但必须遵循函数的参数规则，有几个参数需要传几个参数

```py
OldboyStudent.learn(s1) #李坦克 is learning
OldboyStudent.learn(s2) #王大炮 is learning
OldboyStudent.learn(s3) #牛榴弹 is learning
```

类中定义的函数（没有被任何装饰器装饰的）,其实主要是给对象使用的，而且是绑定到对象的，虽然所有对象指向的都是相同的功能，但是绑定到不同的对象就是不同的绑定方法

强调：绑定到对象的方法的特殊之处在于，绑定给谁就由谁来调用，谁来调用，就会将‘谁’本身当做第一个参数传给方法，即自动传值（方法\_\_init\_\_也是一样的道理）

```py
s1.learn() #等同于OldboyStudent.learn(s1)
s2.learn() #等同于OldboyStudent.learn(s2)
s3.learn() #等同于OldboyStudent.learn(s3)
```

**注意：绑定到对象的方法的这种自动传值的特征，决定了在类中定义的函数都要默认写一个参数self，self可以是任意名字，但是约定俗成地写出self。**

### 类即类型

python中一切皆为对象，且python3中类与类型是一个概念，类型就是类

```py
#类型dict就是类dict
>>> list
<class 'list'>

#实例化的到3个对象l1,l2,l3
>>> l1=list()
>>> l2=list()
>>> l3=list()

#三个对象都有绑定方法append,是相同的功能,但内存地址不同
>>> l1.append
<built-in method append of list object at 0x10b482b48>
>>> l2.append
<built-in method append of list object at 0x10b482b88>
>>> l3.append
<built-in method append of list object at 0x10b482bc8>

#操作绑定方法l1.append(3),就是在往l1添加3,绝对不会将3添加到l2或l3
>>> l1.append(3)
>>> l1
[3]
>>> l2
[]
>>> l3
[]
#调用类list.append(l3,111)等同于l3.append(111)
>>> list.append(l3,111) #l3.append(111)
>>> l3
[111]
```

## 小节练习

**练习1：编写一个学生类，产生一堆学生对象， \(5分钟\)**

要求：

1. 有一个计数器（属性），统计总共实例了多少个对象

**练习2：模仿王者荣耀定义两个英雄类， \(10分钟\)**

要求：

1. 英雄需要有昵称、攻击力、生命值等属性；
2. 实例化出两个英雄对象；
3. 英雄之间可以互殴，被殴打的一方掉血，血量小于0则判定为死亡。



