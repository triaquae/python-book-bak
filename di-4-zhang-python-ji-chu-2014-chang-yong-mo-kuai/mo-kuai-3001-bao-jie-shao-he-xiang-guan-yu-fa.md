## 本节重点：

* 使学员掌握模块概念、分类、几种导入方法
* 使学生掌握包的概念、不同包之间模块的相互导入、模块的查找路径
* 使学员掌握第3方模块的安装方法

> **本节时长需控制在?分钟内**



## 什么是模块？

在计算机程序的开发过程中，随着程序代码越写越多，在一个文件里代码就会越来越长，越来越不容易维护。

为了编写可维护的代码，我们把很多函数分组，分别放到不同的文件里，这样，每个文件包含的代码就相对较少，很多编程语言都采用这种组织代码的方式。在Python中，一个.py文件就称之为一个模块（Module）。

## 使用模块有什么好处？

1. 最大的好处是大大提高了代码的可维护性。其次，编写代码不必从零开始。当一个模块编写完毕，就可以被其他地方引用。我们在编写程序的时候，也经常引用其他模块，包括Python内置的模块和来自第三方的模块。
2. 使用模块还可以避免函数名和变量名冲突。每个模块有独立的命名空间，因此相同名字的函数和变量完全可以分别存在不同的模块中，所以，我们自己在编写模块时，不必考虑名字会与其他模块冲突

## 模块分类 

模块分为三种：

* 内置标准模块（又称标准库）执行help\('modules'\)查看所有python自带模块列表
* 第三方开源模块，可通过pip install 模块名 联网安装 
* 自定义模块

## 模块调用 

```py
import module

from module import xx

from module.xx.xx import xx as rename  

from module.xx.xx import *
```

> 注意：模块一旦被调用，即相当于执行了另外一个py文件里的代码

#### 自定义模块

这个最简单， 创建一个.py文件，就可以称之为模块，就可以在另外一个程序里导入

#### 模块查找路径

发现，自己写的模块只能在当前路径下的程序里才能导入，换一个目录再导入自己的模块就报错说找不到了， 这是为什么？

这与导入路径有关

```py
import sys

print(sys.path)
```

输出

```py
['', '/Library/Frameworks/Python.framework/Versions/3.6/lib/python36.zip', 
'/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6', 
'/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/lib-dynload', 
'/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages']
```

python解释器会按照列表顺序去依次到每个目录下去匹配你要导入的模块名，只要在一个目录下匹配到了该模块名，就立刻导入，不再继续往后找。

> 注意列表第一个元素为空，即代表当前目录，所以你自己定义的模块在当前目录会被优先导入。

## 开源模块安装、使用

https://pypi.python.org/pypi 是python的开源模块库，截止2017年9.30日 ，已经收录了**118170**个来自全世界python开发者贡献的模块,几乎涵盖了你想用python做的任何事情。 事实上每个python开发者，只要注册一个账号就可以往这个平台上传你自己的模块，这样全世界的开发者都可以容易的下载并使用你的模块。![](/assets/chapter4/pypi.png)那如何从这个平台上下载代码呢？

1.直接在上面这个页面上点download,下载后，解压并进入目录，执行以下命令完成安装

```
编译源码    python setup.py build
安装源码    python setup.py install
```

2. 直接通过pip安装

```
pip3 install paramiko #parmiko 是模块名
```

pip命令会自动下载模块包并完成安装。

软件一般会被自动安装你python安装目录的这个子目录里

```
/your_python_install_path/3.6/lib/python3.6/site-packages
```

pip命令默认会连接在国外的python官方服务器下载，速度比较慢，你还可以使用国内的豆瓣源，数据会定期同步国外官网，速度快好多

```py
sudo pip install -i http://pypi.douban.com/simple/ alex_sayhi --trusted-host pypi.douban.com   #alex_sayhi是模块名
```

#### 使用

下载后，直接导入使用就可以，跟自带的模块调用方法无差，演示一个连接linux执行命令的模块

```py
#coding:utf-8

import paramiko

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect('192.168.1.108', 22, 'alex', '123')

stdin, stdout, stderr = ssh.exec_command('df')
print(stdout.read())
ssh.close();

执行命令 - 通过用户名和密码连接服务器
```



## 包\(Package\)

当你的模块文件越来越多，就需要对模块文件进行划分，比如把负责跟数据库交互的都放一个文件夹，把与页面交互相关的放一个文件夹，

```bash
.
└── my_proj
    ├── crm #代码目录
    │   ├── admin.py
    │   ├── apps.py
    │   ├── models.py
    │   ├── tests.py
    │   └── views.py
    ├── manage.py
    └── my_proj #配置文件目录
        ├── settings.py
        ├── urls.py
        └── wsgi.py
```

像上面这样，**一个文件夹管理多个模块文件，这个文件夹就被称为包**

那不同包之间的模块互相导入呢？

**crm/views.py内容**

```py

def sayhi():
    print('hello world!')
```

**通过manage.py调用**

```py
from crm import views

views.sayhi()
```

**执行manage.py \(注意这里用python2\)**

```py
Alexs-MacBook-Pro:my_proj alex$ ls
crm		manage.py	my_proj
Alexs-MacBook-Pro:my_proj alex$ python manage.py 
Traceback (most recent call last):
  File "manage.py", line 6, in <module>
    from crm import views
ImportError: No module named crm
```

竟然说找不到模块，为什么呢？

**包就是文件夹，但该文件夹下必须存在 \_\_init\_\_.py 文件, 该文件的内容可以为空。\_\_int\_\_.py用于标识当前文件夹是一个包。**

在crm目录下创建一个空文件**\_\_int\_\_.py ，再执行一次就可以了**

```
Alexs-MacBook-Pro:my_proj alex$ touch crm/__init__.py #创建一个空文件
Alexs-MacBook-Pro:my_proj alex$ 
Alexs-MacBook-Pro:my_proj alex$ ls crm/
__init__.py	admin.py	models.py	views.py
__pycache__	apps.py		tests.py	views.pyc
Alexs-MacBook-Pro:my_proj alex$ python manage.py 
hello world!

```

> 注意，在python3里，即使目录下没\_\_int\_\_.py文件也能创建成功，猜应该是解释器优化所致，但创建包还是要记得加上这个文件 吧。





