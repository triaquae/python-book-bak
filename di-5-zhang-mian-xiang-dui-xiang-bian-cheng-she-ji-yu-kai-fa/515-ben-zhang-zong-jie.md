## 本章总结

### 练习题

1. 面向对象三大特性，各有什么用处，说说你的理解。  
2. 类的属性和对象的属性有什么区别?  
3. 面向过程编程与面向对象编程的区别与应用场景?  
4. 类和对象在内存中是如何保存的。  
5. 什么是绑定到对象的方法、绑定到类的方法、解除绑定的函数、如何定义，如何调用，给谁用？有什么特性  
6. 使用实例进行 获取、设置、删除 数据, 分别会触发类的什么私有方法

   ```py
    class A(object):
        pass

    a = A()

    a["key"] = "val"
    a = a["key"]
    del a["key"]
   ```

7. python中经典类和新式类的区别

8. 如下示例, 请用面向对象的形式优化以下代码
 
  ```python
      def exc1(host,port,db,charset,sql):
          conn=connect(host,port,db,charset)
          conn.execute(sql)
          return xxx
      def exc2(host,port,db,charset,proc_name)
          conn=connect(host,port,db,charset)
          conn.call_proc(sql)
          return xxx
      # 每次调用都需要重复传入一堆参数
      exc1('127.0.0.1',3306,'db1','utf8','select * from tb1;')
      exc2('127.0.0.1',3306,'db1','utf8','存储过程的名字')
  ```

9. 示例1, 现有如下代码， 会输出什么：

   ```python
     class People(object):
         __name = "luffy"
         __age = 18

     p1 = People()
     print(p1.__name, p1.__age)
   ```

10. 示例2, 现有如下代码， 会输出什么：

    ```py
    class People(object):

       def __init__(self):
           print("__init__")

       def __new__(cls, *args, **kwargs):
           print("__new__")
           return object.__new__(cls, *args, **kwargs)

    People()
    ```

11. 请简单解释Python中 staticmethod（静态方法）和 classmethod（类方法）, 并分别补充代码执行下列方法。

    ```py
    class A(object):

       def foo(self, x):
           print("executing foo(%s, %s)" % (self,x))

       @classmethod
       def class_foo(cls, x):
           print("executing class_foo(%s, %s)" % (cls,x))

       @staticmethod
       def static_foo(x):
           print("executing static_foo(%s)" % (x))

    a = A()
    ```

12. 请执行以下代码，解释错误原因，并修正错误。

    ```py
    class Dog(object):

       def __init__(self,name):
           self.name = name

       @property
       def eat(self):
           print(" %s is eating" %self.name)

    d = Dog("ChenRonghua")
    d.eat()
    ```

13. 下面这段代码的输出结果将是什么？请解释。

    ```py
    class Parent(object):
       x = 1

    class Child1(Parent):
       pass

    class Child2(Parent):
       pass

    print(Parent.x, Child1.x, Child2.x)
    Child1.x = 2
    print(Parent.x, Child1.x, Child2.x)
    Parent.x = 3
    print(Parent.x, Child1.x, Child2.x)

    # 1 1 1 继承自父类的类属性x，所以都一样，指向同一块内存地址
    # 1 2 1 更改Child1，Child1的x指向了新的内存地址
    # 3 2 3 更改Parent，Parent的x指向了新的内存地址
    ```

14. 多重继承的执行顺序，请解答以下输出结果是什么？并解释。

    ```py
    class A(object):
       def __init__(self):
           print('A')
           super(A, self).__init__()

    class B(object):
       def __init__(self):
           print('B')
           super(B, self).__init__()

    class C(A):
       def __init__(self):
           print('C')
           super(C, self).__init__()

    class D(A):
       def __init__(self):
           print('D')
           super(D, self).__init__()

    class E(B, C):
       def __init__(self):
           print('E')
           super(E, self).__init__()

    class F(C, B, D):
       def __init__(self):
           print('F')
           super(F, self).__init__()

    class G(D, B):
       def __init__(self):
           print('G')
           super(G, self).__init__()

    if __name__ == '__main__':
       g = G()
       f = F()

    # G
    # D
    # A
    # B
    #
    # F
    # C
    # B
    # D
    # A
    ```

15. 请编写一段符合多态特性的代码.

16. 很多同学都是学会了面向对象的语法，却依然写不出面向对象的程序，原因是什么呢？原因就是因为你还没掌握一门面向对象设计利器，即领域建模，请解释下什么是领域建模，以及如何通过其设计面向对象的程序？[http://www.cnblogs.com/alex3714/articles/5188179.html](http://www.cnblogs.com/alex3714/articles/5188179.html) 此blog最后面有详解

17. 请写一个小游戏，人狗大站，2个角色，人和狗，游戏开始后，生成2个人，3条狗，互相混战，人被狗咬了会掉血，狗被人打了也掉血，狗和人的攻击力，具备的功能都不一样。注意，请按题14领域建模的方式来设计类。

18. 编写程序, 在元类中控制把自定义类的数据属性都变成大写.

19. 编写程序, 在元类中控制自定义的类无需**init**方法.  
20. 编写程序, 编写一个学生类, 要求有一个计数器的属性, 统计总共实例化了多少个学生.  
21. 编写程序, A 继承了 B, 俩个类都实现了 handle 方法, 在 A 中的 handle 方法中调用 B 的 handle 方法  
22. 编写程序, 如下有三点要求：  
      
    1. 自定义用户信息数据结构， 写入文件, 然后读取出内容, 利用json模块进行数据的序列化和反序列化

    ```py
    e.g
    {
        "egon":{"password":"123",'status':False,'timeout':0},
        "alex":{"password":"456",'status':False,'timeout':0},
    }
    ```

    1. 定义用户类，定义方法db，例如 执行obj.db可以拿到用户数据结构  
    2. 在该类中实现登录、退出方法, 登录成功将状态\(status\)修改为True, 退出将状态修改为False\(退出要判断是否处于登录状态\).密码输入错误三次将设置锁定时间\(下次登录如果和当前时间比较大于10秒即不允许登录\)  

23. 用面向对象的形式编写一个老师角色, 并实现以下功能, 获取老师列表, 创建老师、删除老师、创建成功之后通过 pickle 序列化保存到文件里，并在下一次重启程序时能  
    读取到创建的老师, 例如程序目录结构如下.

    ```py
    .
    |-- bin/
    |   |-- main.py         程序运行主体程序(可进行菜单选择等)
    |-- config/
    |   |-- settings.py     程序配置(例如: 配置存储创建老师的路径相关等)
    |-- db                  数据存储(持久化, 使得每次再重启程序时, 相关数据对应保留)
    |   |-- teachers/          存储所有老师的文件
    |   |-- ...                ...
    |-- src/                程序主体模块存放
    |   |-- __init__.py
    |   |-- teacher.py      例如: 实现老师相关功能的文件
    |   |-- group.py        例如: 实现班级相关的功能的文件
    |-- manage.py           程序启动文件
    |-- README.md           程序说明文件
    ```

24. 根据23 题, 再编写一个班级类, 实现以下功能, 创建班级, 删除班级, 获取班级列表、创建成功之后通过 pickle 序列化保存到文件里，并在下一次重启程序时能  
    读取到创建的班级.

25. 根据 23题, 编写课程类, 实现以下功能, 创建课程\(创建要求如上\), 删除课程, 获取课程列表

26. 根据23 题, 编写学校类, 实现以下功能, 创建学校, 删除学校, 获取学校列表

27. 通过23题, 它们雷同的功能, 是否可以通过继承的方式进行一些优化

    ```py
    伪代码
    class Behavior(object):

        def fetch(self, keyword):
            通过 keyword 参数 查询出对应的数据列表

    class School(Behavior):

        pass

    class Teacher(Behavior):

        pass

    s = School()
    t = Teacher()

    s.fetch("school")
    t.fetch("teacher")
    ```



## 本章作业

**题目**：选课系统开发，要求有四种角色:学校、学员、课程、讲师

**详细要求:**  

1. 创建北京、上海 2 所学校

2. 创建linux , python , go 3个课程 ， linux\py 在北京开， go 在上海开

3. 课程包含，周期，价格，通过学校创建课程

4. 通过学校创建班级， 班级关联课程、讲师

5. 创建学员时，选择学校，关联班级

6. 创建讲师角色时要关联学校

7. 提供两个角色接口

8. 为学员、讲师、管理员分别提供用户界面，并提供对应功能：
    1 学员视图， 可以注册， 交学费， 选择班级，
    2 讲师视图， 讲师可管理自己的班级， 上课时选择班级， 查看班级学员列表 ， 修改所管理的学员的成绩
    3 管理视图，创建讲师， 创建班级，创建课程
    
*注1：上面的操作产生的数据都通过pickle序列化保存到文件里
*注2：此作业必须画流程图，图中标注好不同类或对象之间的调用关系


