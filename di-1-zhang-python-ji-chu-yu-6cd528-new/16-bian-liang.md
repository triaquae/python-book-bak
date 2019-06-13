## 什么是变量？

变量，是用于在内存中存放程序数据的容器，怎么理解呢？

计算机的最核心功能就是“计算”， 计算需要数据源，数据源要存在内存里，比如我要把小明的姓名、身高、年龄信息存下来，后面程序会调用，怎么存呢，直接设置一个“变量名=值”， 就可以

```py
name = "小明"
age = 22
height = 160 
```

后面程序想调用的时候，直接调 变量名 就可以

```py
name = "小明"
age = 22
height = 160 
print(name)
print(age)
```



## 变量的使用规则

程序是从上到下执行的，所以变量必须先定义，后调用， 否则会报错

![](https://book.apeland.cn/media/images/2019/02/21/image_r09G11t.png)

**变量名定义规则**

1. 变量名只能是 字母、数字或下划线的任意组合

2. 变量名的第一个字符不能是数字

3. 以下关键字不能声明为变量名\[‘and’, ‘as’, ‘assert’, ‘break’, ‘class’, ‘continue’, ‘def’, ‘del’, ‘elif’, ‘else’, ‘except’, ‘exec’, ‘finally’, ‘for’, ‘from’, ‘global’, ‘if’, ‘import’, ‘in’, ‘is’, ‘lambda’, ‘not’, ‘or’, ‘pass’, ‘print’, ‘raise’, ‘return’, ‘try’, ‘while’, ‘with’, ‘yield’\]

  


## **常用定义方式**

驼峰体

```
AgeOfOldboy = 56 
NumberOfStudents = 80
```

下划线

```
age_of_oldboy = 56 
number_of_students = 80
```

你觉得哪种更清晰，哪种就是官方推荐的，我想你肯定会先第2种

#### **定义变量不好的方式举例**

* 变量名为中文、拼音

* 变量名过长

* 变量名词不达意

  


## 变量的修改

自行看图不解释

![](https://book.apeland.cn/media/images/2019/02/21/image_W0IaPgB.png)

## 常量

常量即指不变的量，如pai 3.141592653…, 或在程序运行过程中不会改变的量

举例，假如老男孩老师的年龄会变，那这就是个变量，但在一些情况下，他的年龄不会变了，那就是常量。在Python中没有一个专门的语法代表常量，程序员约定俗成用变量名全部大写代表常量

```
AGE_OF_OLDBOY = 56
```



> 在c语言中有专门的常量定义语法，
> `const int count = 60;`
> 一旦定义为常量，更改即会报错

  




  


