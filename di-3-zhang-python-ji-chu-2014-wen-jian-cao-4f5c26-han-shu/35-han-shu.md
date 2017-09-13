## 本节重点：

* 使学生掌握函数的作用、语法
* 掌握作用域、全局变量与局部变量知识

> **本节时长需控制在  分钟内**



## 引子

现在老板让你写一个监控程序，24小时全年无休的监控你们公司网站服务器的系统状况，当cpu＼memory＼disk等指标的使用量超过阀值时即发邮件报警，你掏空了所有的知识量，写出了以下代码

```
while True：
    if cpu利用率 > 90%:
        #发送邮件提醒
        连接邮箱服务器
        发送邮件
        关闭连接
     
    if 硬盘使用空间 > 90%:
        #发送邮件提醒
        连接邮箱服务器
        发送邮件
        关闭连接
     
    if 内存占用 > 80%:
        #发送邮件提醒
        连接邮箱服务器
        发送邮件
        关闭连接
```

上面的代码实现了功能，但即使是邻居老王也看出了端倪，老王亲切的摸了下你家儿子的脸蛋，说，你这个重复代码太多了，每次报警都要重写一段发邮件的代码，太low了，这样干存在2个问题：

1. 代码重复过多，一个劲的copy and paste不符合高端程序员的气质
2. 如果日后需要修改发邮件的这段代码，比如加入群发功能，那你就需要在所有用到这段代码的地方都修改一遍

你觉得老王说的对，你也不想写重复代码，但又不知道怎么搞，老王好像看出了你的心思，此时他抱起你儿子，笑着说，其实很简单，**只需要把重复的代码提取出来，放在一个公共的地方，起个名字，以后谁想用这段代码，就通过这个名字调用就行了**，如下

```
def 发送邮件(内容)
    #发送邮件提醒
    连接邮箱服务器
    发送邮件
    关闭连接
     
while True：
     
    if cpu利用率 > 90%:
        发送邮件('CPU报警')
     
    if 硬盘使用空间 > 90%:
        发送邮件('硬盘报警')
     
    if 内存占用 > 80%:
        发送邮件('内存报警')

```

你看着老王写的代码，气势恢宏、磅礴大气，代码里透露着一股内敛的傲气，心想，老王这个人真是不一般，突然对他的背景更感兴趣了，问老王，这些花式玩法你都是怎么知道的？ 老王亲了一口你儿子，捋了捋不存在的胡子，淡淡的讲，“老夫，年少时，师从京西沙河淫魔银角大王 ”， 你一听“银角大王”这几个字，不由的娇躯一震，心想，真nb,怪不得代码写的这么6, 这“银角大王”当年在江湖上可是数得着的响当当的名字，只可惜后期纵欲过度，卒于公元2017年， 真是可惜了，只留下其哥哥孤守当年兄弟俩一起打下来的江山。 此时你看着的老王离开的身影，感觉你儿子跟他越来越像了。。。

## 基本定义

#### 函数是什么?

函数一词来源于数学，但编程中的「函数」概念，与数学中的函数是有很大不同的，具体区别，我们后面会讲，编程中的函数在英文中也有很多不同的叫法。在BASIC中叫做subroutine\(子过程或子程序\)，在Pascal中叫做procedure\(过程\)和function，在C中只有function，在Java里面叫做method。

**定义: 函数是指将一组语句的集合通过一个名字\(函数名\)封装起来，要想执行这个函数，只需调用其函数名即可**

**特性:**

1. 减少重复代码
2. 使程序变的可扩展
3. 使程序变得易维护

#### 语法定义

```py
def sayhi():#函数名
    print("Hello, I'm nobody!")
 
sayhi() #调用函数
```

可以带参数

```py
#下面这段代码
a,b = 5,8
c = a**b
print(c)
 
 
#改成用函数写
def calc(x,y):
    res = x**y
    return res #返回函数执行结果
 
c = calc(a,b) ＃结果赋值给c变量
print(c)
```

参数可以让你的函数更灵活，不只能做死的动作，还可以根据调用时传参的不同来决定函数内部的执行流程



## 函数参数

**形参变量**

只有在被调用时才分配内存单元，在调用结束时，即刻释放所分配的内存单元。因此，形参只在函数内部有效。函数调用结束返回主调用函数后则不能再使用该形参变量

**实参**

可以是常量、变量、表达式、函数等，无论实参是何种类型的量，在进行函数调用时，它们都必须有确定的值，以便把这些值传送给形参。因此应预先用赋值，输入等办法使参数获得确定值

![](/assets/chapter3-func-argv.png)

#### **默认参数**

看如下代码

```py
def stu_register(name,age,country,course):
    print("----注册学生信息------")
    print("姓名:",name)
    print("age:",age)
    print("国籍:",country)
    print("课程:",course)
 
stu_register("王山炮",22,"CN","python_devops")
stu_register("张叫春",21,"CN","linux")
stu_register("刘老根",25,"CN","linux")
```

发现 country 这个参数 基本都 是"CN", 就像我们在网站上注册用户，像国籍这种信息，你不填写，默认就会是 中国， 这就是通过默认参数实现的，把country变成默认参数非常简单

```py
def stu_register(name,age,course,country="CN"):
```

这样，这个参数在调用时不指定，那默认就是CN，指定了的话，就用你指定的值。

> **另外，你可能注意到了，在把country变成默认参数后，我同时把它的位置移到了最后面，为什么呢？　　**



#### 关键参数

正常情况下，给函数传参数要按顺序，不想按顺序就可以用关键参数，只需指定参数名即可\(指定了参数名的参数就叫关键参数\)，_**但记住一个要求就是，关键参数必须放在位置参数\(以位置顺序确定对应关系的参数\)之后**_

```py
def stu_register(name, age, course='PY' ,country='CN'):
    print("----注册学生信息------")
    print("姓名:", name)
    print("age:", age)
    print("国籍:", country)
    print("课程:", course)
```

调用可以这样

```py
stu_register("王山炮",course='PY', age=22,country='JP' )
```

但绝不可以这样

```py
stu_register("王山炮",course='PY',22,country='JP' )
```

当然这样也不行

```py
stu_register("王山炮",22,age=25,country='JP' )
```

这样相当于给age赋值2次，会报错！



#### **非固定参数**

若你的函数在定义时不确定用户想传入多少个参数，就可以使用非固定参数

```py
def stu_register(name,age,*args): # *args 会把多传入的参数变成一个元组形式
    print(name,age,args)
 
stu_register("Alex",22)
#输出
#Alex 22 () #后面这个()就是args,只是因为没传值,所以为空
 
stu_register("Jack",32,"CN","Python")
#输出
# Jack 32 ('CN', 'Python')
```

还可以有一个\*\*kwargs

```py
def stu_register(name,age,*args,**kwargs): # *kwargs 会把多传入的参数变成一个dict形式
    print(name,age,args,kwargs)
 
stu_register("Alex",22)
#输出
#Alex 22 () {}#后面这个{}就是kwargs,只是因为没传值,所以为空
 
stu_register("Jack",32,"CN","Python",sex="Male",province="ShanDong")
#输出
# Jack 32 ('CN', 'Python') {'province': 'ShanDong', 'sex': 'Male'}
```



## 返回值

函数外部的代码要想获取函数的执行结果，就可以在函数里用return语句把结果返回

```py

def stu_register(name, age, course='PY' ,country='CN'):
    print("----注册学生信息------")
    print("姓名:", name)
    print("age:", age)
    print("国籍:", country)
    print("课程:", course)
    if age > 22:
        return False
    else:
        return True

registriation_status = stu_register("王山炮",22,course="PY全栈开发",country='JP')

if registriation_status:
    print("注册成功")

else:
    print("too old to be a student.")
```

**注意**

* 函数在执行过程中只要遇到return语句，就会停止执行并返回结果，so 也可以理解为 return 语句代表着函数的结束
* 如果未在函数中指定return,那这个函数的返回值为None 



## 全局与局部变量

```py
name = "Alex Li"
 
def change_name(name):
    print("before change:",name)
    name = "金角大王,一个有Tesla的男人"
    print("after change", name)
 
 
change_name(name)
 
print("在外面看看name改了么?",name)
```

输出

```py
before change: Alex Li
after change 金角大王,一个有Tesla的男人
在外面看看name改了么? Alex Li
```

不用传name 值到函数里，也可以在函数里调用外面的变量

```py
name = "Alex Li"


def change_name():
    name = "金角大王,一个有Tesla的男人"
    print("after change", name)


change_name()

print("在外面看看name改了么?", name)
```

**但就是不能改！**



* 在函数中定义的变量称为局部变量，在程序的一开始定义的变量称为全局变量。
* 全局变量作用域是整个程序，局部变量作用域是定义该变量的函数。
* 当全局变量与局部变量同名时，在定义局部变量的函数内，局部变量起作用；在其它地方全局变量起作用。



#### 如何在函数里修改全局变量？

```py

name = "Alex Li"

def change_name():
    global name
    name = "Alex 又名 金角大王,路飞学城讲师"
    print("after change", name)


change_name()

print("在外面看看name改了么?", name)
```

`global name`**的作用就是要在函数里声明全局变量name ，意味着最上面的` name = "Alex Li" `即使不写，程序最后面的print也可以打印name **



