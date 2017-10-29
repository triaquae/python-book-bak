## 本节重点：

* 使学员了解面向对象概念、与面向过程的区别

> **本节时长需控制在30分钟内**

## 编程范式

编程是 程序 员 用特定的语法+数据结构+算法 组成的代码来告诉计算机如何执行任务的过程 。

一个程序是程序员为了得到一个任务结果而编写的一组指令的集合，正所谓条条大路通罗马，实现一个任务的方式有很多种不同的方式， 对这些不同的编程方式的特点进行归纳总结得出来的编程方式类别，即为编程范式。 不同的编程范式本质上代表对各种类型的任务采取的不同的解决问题的思路， 大多数语言只支持一种编程范式，当然也有些语言可以同时支持多种编程范式。 两种最重要的编程范式分别是面向过程编程和面向对象编程。

### 面向过程编程\(Procedural Programming\)

Procedural programming uses a list of instructions to tell the computer what to do step-by-step.

面向过程编程依赖 - 你猜到了- procedures，一个procedure包含一组要被进行计算的步骤， 面向过程又被称为top-down languages， 就是程序从上到下一步步执行，一步步从上到下，从头到尾的解决问题 。基本设计思路就是程序一开始是要着手解决一个大的问题，然后把一个大问题分解成很多个小问题或子过程，这些子过程再执行的过程再继续分解直到小问题足够简单到可以在一个小步骤范围内解决。

举个典型的面向过程的例子， 写一个数据远程备份程序， 分三步，本地数据打包，上传至云服务器，测试备份文件可用性。

```py
def cloud_upload(file):

        print("\nconnecting cloud storage center...")
        print("cloud storage connected.")
        print("upload file...xxx..to cloud...", file)
        print('close connection.....')


def data_backup(folder):
    print("找到要备份的目录...", folder)
    print("将备份文件打包，移至相应目录...")
    return '/tmp/backup20181103.zip'

def data_backup_test():

    print("\n从另外一台机器将备份文件从远程cloud center下载，看文件是否无损")


def main():
    zip_file = data_backup("c:\\users\\alex\欧美100G高清无码")

    cloud_upload(zip_file)

    data_backup_test()


if __name__ == '__main__':
    main()
```

这个变量，那这个子过程你也要修改，假如又有一个其它子程序依赖这个子过程 ， 那就会发生一连串的影响，随着程序越来越大， 这种编程方式的维护难度会越来越高。

```py
test = 1

def cloud_upload(file):

    if test == 1:
        print("\nconnecting cloud storage center...")
        print("cloud storage connected.")
        print("upload file...xxx..to cloud...", file)
        print('close connection.....')
        return True
    else:
        print("不备份")
        return False

def data_backup(folder):
    print("找到要备份的目录...", folder)
    print("将备份文件打包，移至相应目录...")
    return '/tmp/backup20181103.zip'

def data_backup_test(upload_res):
    if upload_res == 1:
        print("\n从另外一台机器将备份文件从远程cloud center下载，看文件是否无损")
    else:
        print("upload error,不备份")

def main():
    zip_file = data_backup("c:\\users\\alex\欧美100G高清无码")

    res = cloud_upload(zip_file)

    data_backup_test(res)


if __name__ == '__main__':
    main()
```

所以我们一般认为， 如果你只是写一些简单的脚本，去做一些一次性任务，用面向过程的方式是极好的，但如果你要处理的任务是复杂的，且需要不断迭代和维护 的， 那还是用面向对象最方便了。

### 面向对象编程\(Object Oriented Programing\)

直接解释，你必然会蒙逼，所以先讲个引子。

你现在是一家游戏公司的开发人员，现在需要你开发一款叫做&lt;人狗大战&gt;的游戏，你就思考呀，人狗作战，那至少需要2个角色，一个是人， 一个是狗，且人和狗都有不同的技能，比如人拿棍打狗， 狗可以咬人，怎么描述这种不同的角色和他们的功能呢？

你搜罗了自己掌握的所有技能，写出了下面的代码来描述这两个角色

```py
person = {
    'name':'Alex',
    'attack': 100, #杀伤力
    'life_value':1000
}


dog = {
    'name':'Peiqi',
    'attack': 200, #杀伤力
    'life_value':800
}
```

一个字典表示一个角色实体，但如果有多条狗和多个人一起打呢？那就得写多个字典

```py
person = {
    'name':'Alex',
    'attack': 100, #杀伤力
    'life_value':1000
}
person2 = {
    'name':'Black Girl',
    'attack': 100, #杀伤力
    'life_value':600
}


dog = {
    'name':'Peiqi',
    'attack': 200, #杀伤力
    'life_value':800
}
```

这样是有问题的，因为如果你字典里的值不小心定义错了，把attack写成了了atteck的话，那整个程序就有问题了。so 你很快想出了改进方案，把字典放进函数

```py
def person(name,attack,life_value):
    data = {
        'name':name,
        'attack':attack,
        'life_value':life_value,
    }
    return data


def dog(name, attack, life_value):
    data = {
        'name': name,
        'attack': attack,
        'life_value': life_value,
    }
    return data


alex = person("Alex",100,1000)
rain = person("Black girl",80,700)

d = dog("PeiQi",200,800)
```

好，现在角色定义好了，还差每个角色的功能，人打狗，狗咬人的功能要定义出来

```py
....

def attack(p,d):
    """人打狗功能"""

    d['life_value'] -= p['attack'] #被打了，要掉血
    print("人[%s] 打了 狗[%s]。。。,[%s]的生命值还有[%s]" % (p['name'], d['name'],d['name'],d['life_value']))

def bite(d,p):
    """狗咬人功能"""
    p['life_value'] -= d['attack']
    print("狗[%s] 咬了 人[%s]。。。,[%s]的生命值还有[%s]" % (d['name'], p['name'],p['name'],p['life_value']))

alex = person("Alex",100,1000)
black_girl = person("Black girl",80,700)

d = dog("PeiQi",200,800)

attack(alex,d)
bite(d,black_girl)
```

现在，就可以开心的玩耍啦。。。

但玩着玩着， 你不小心调用错了，

```py
bite(alex,black_girl) #你调用咬人功能时，把alex当狗传进去了，结果就变成了如下
```

> 人\[Alex\] 打了 狗\[PeiQi\]。。。,\[PeiQi\]的生命值还有\[700\]
>
> 狗\[PeiQi\] 咬了 人\[Black girl\]。。。,\[Black girl\]的生命值还有\[500\]
>
> 狗\[Alex\] 咬了 人\[Black girl\]。。。,\[Black girl\]的生命值还有\[400\]

你让我咬black\_girl一口我不介意，但以狗的身份，我是反对的，所以这明显是个bug,bite\(\)功能是狗专属的，不应该允许人调用，这可怎么办呢？

哈，想了一会，你又搞定了。

```py
def person(name,attack_val,life_value):

    def attack( d):
        """人打狗功能"""

        d['life_value'] -= attack_val  # 被打了，要掉血
        print("人[%s] 打了 狗[%s]。。。,[%s]的生命值还有[%s]" % (name, d['name'], d['name'], d['life_value']))

    data = {
        'name':name,
        'attack_val':attack_val,
        'life_value':life_value,
        'attack':attack
    }
    return data


def dog(name, attack_val, life_value):

    def bite(p):
        """狗咬人功能"""
        p['life_value'] -= attack_val
        print("狗[%s] 咬了 人[%s]。。。,[%s]的生命值还有[%s]" % (name, p['name'], p['name'], p['life_value']))

    data = {
        'name': name,
        'attack_val': attack_val,
        'life_value': life_value,
        'bite':bite
    }
    return data



alex = person("Alex",100,1000)
black_girl = person("Black girl",80,700)

d = dog("PeiQi",200,800)

alex['attack'](d)
d['bite'](black_girl)
```

你是如此的机智，这样就实现了限制人只能用人自己的功能啦。

但，我的哥，不要高兴太早，刚才你只是阻止了两个完全 不同的角色 之间的功能混用， 但有没有可能 ，同一个种角色，但有些属性是不同的呢？ 比如 ，现在游戏升级了，不仅可以打狗，还可以生孩子，但男人不能生呀，只能女的生，怎么办呢？你想了想说，简单呀， 在person函数里包一个子函数叫`get_birth(),`

```py
def get_birth(person_data):
    if person_data['sex'] == 'female':
        print("%s生孩子 啦..."% person_data['name'] )
    else:
        print("你是男的生个毛线.")
```

没错， 这虽然解决了只能女人生孩子的问题，但其实随着游戏功能越来越多，你会发出男女之间的区别也越来越多 ，但又同时有很多共性，如果 在每个区别处都 单独做判断，那得累死。

你想了想说， 那就直接写2个角色吧， 反正 这么多区别， 我的哥， 不能写两个角色呀，因为他们还有很多共性 ， 写两个不同的角色，就代表 相同的功能 也要重写了，是不是我的哥？ 。。。 没话说了吧？哈哈， 就是要逼你到绝路上。

**上面的问题通过面向对象编程可轻松解决！**

#### 什么是面向对象编程？

OOP\(Object Oriented Programing）编程是利用“类”和“对象”来创建各种模型来实现对真实世界的描述。

上面的描述你必定是懵逼的，用白话解释面向对象与面向过程的区别就是：

**面向过程 = 个人视角**

```
我要去做大保健，我只需考虑，我有没有钱，去哪家店，怎么去，做什么价位的就可以，你的每一步都要通过程序定义出来，写死了，在这个程序里，你只被设定了去做大保健的功能，你说中途我想去个ktv,那可能会导致整个程序的逻辑都得更改。 用面向过程的方式写代码，那你care的就是整个事情的执行过程
```

**面向对象 = 上帝视角**

```
如果你是上帝，你现在要创世纪，把这么多人、动物、山河造出来，上帝光靠自己干，一个一个的造人，多累呀，让你干这个活，你肯定是先造模子，一个男人模子，一个女人模子，剩下的就一个个复制就行啦。这个模子的作用是什么？模子定义了人这个物种所具备的所有特征\(或者说，我们把具备这些特征的个体归为人类\)。

这个世界上所有的东西都是你定义的，你需要用最高效的方式去造世界，最高效的方式就是，先把世界按物种、样貌、有无生命等各种维度分类，然后给每类东西建模型，再让其在不脱离你基本横型定义的框架下，自我繁衍（世界要多姿多彩，所以即使是同一物种，也要有些不一样）
```

#### 为什么要用面向对象？

1. 使程序更加容易扩展和易更改，使开发效率变的更高
2. 基于面向对象的程序可以使它人更加容易理解你的代码逻辑，从而使团队开发变得更从容。



## 面向对象介绍

学习面向对象过程中会遇到一些名词，我们先解释下

### 名词解释

**类：**一个类即是对一类拥有相同属性的对象的抽象、蓝图、原型、模板。在类中定义了这些对象的都具备的属性（variables\(data\)）、共同的方法

**属性：**人类包含很多特征，把这些特征用程序来描述的话，叫做属性，比如年龄、身高、性别、姓名等都叫做属性，一个类中，可以有多个属性

**方法：**人类不止有身高、年龄、性别这些属性，还能做好多事情，比如说话、走路、吃饭等，相比较于属性是名词，说话、走路是动词，这些动词用程序来描述就叫做方法。

**实例\(对象\)：**一个对象即是一个类的实例化后实例，一个类必须经过实例化后方可在程序中调用，一个类可以实例化多个对象，每个对象亦可以有不同的属性，就像人类是指所有人，每个人是指具体的对象，人与人之前有共性，亦有不同

**实例化：**把一个类转变为一个对象的过程就叫实例化

### 面向对象3大特性

> 注意，此处只需知道这几个名词，后面会专门再对着代码学习这几大特性

**Encapsulation 封装**

在类中对数据的赋值、内部调用对外部用户是透明的，这使类变成了一个胶囊或容器，里面包含着类的数据和方法

**Inheritance 继承**

一个类可以派生出子类，在这个父类里定义的属性、方法自动被子类继承

**Polymorphism 多态**

多态是面向对象的重要特性,简单点说:“一个接口，多种实现”，指一个基类中派生出了不同的子类，且每个子类在继承了同样的方法名的同时又对父类的方法做了不同的实现，这就是同一种事物表现出的多种形态。

编程其实就是一个将具体世界进行抽象化的过程，多态就是抽象化的一种体现，把一系列具体事物的共同点抽象出来, 再通过这个抽象的事物, 与不同的具体事物进行对话。

对不同类的对象发出相同的消息将会有不同的行为。比如，你的老板让所有员工在九点钟开始工作, 他只要在九点钟的时候说：“开始工作”即可，而不需要对销售人员说：“开始销售工作”，对技术人员说：“开始技术工作”, 因为“员工”是一个抽象的事物, 只要是员工就可以开始工作，他知道这一点就行了。至于每个员工，当然会各司其职，做各自的工作。

多态允许将子类的对象当作父类的对象使用，某父类型的引用指向其子类型的对象,调用的方法是该子类型的方法。这里引用和调用方法的代码编译前就已经决定了,而引用所指向的对象可以在运行期间动态绑定



