## 本节重点

* 掌握multiprocessing模块开启进程的两种方式

> **本节时长需控制在15分钟内**

### 一 multiprocessing模块介绍

python中的多线程无法利用多核优势，如果想要充分地使用多核CPU的资源（os.cpu\\_count\\(\\)查看），在python中大部分情况需要使用多进程。

Python提供了multiprocessing。 multiprocessing模块用来开启子进程，并在子进程中执行我们定制的任务（比如函数），该模块与多线程模块threading的编程接口类似。multiprocessing模块的功能众多：支持子进程、通信和共享数据、执行不同形式的同步，&gt;提供了Process、Queue、Pipe、Lock等组件。

需要再次强调的一点是：与线程不同，进程没有任何共享状态，进程修改的数据，改动仅限于该进程内。

### 二 Process类的介绍

**创建进程的类**：

```
Process([group [, target [, name [, args [, kwargs]]]]])，由该类实例化得到的对象，可用来开启一个子进程

强调：
1. 需要使用关键字的方式来指定参数
2. args指定的为传给target函数的位置参数，是一个元组形式，必须有逗号
```

** 参数介绍：**

```
group参数未使用，值始终为None

target表示调用对象，即子进程要执行的任务

args表示调用对象的位置参数元组，args=(1,2,'egon',)

kwargs表示调用对象的字典,kwargs={'name':'egon','age':18}

name为子进程的名称
```

**方法介绍：**

```
p.start()：启动进程，并调用该子进程中的p.run() 
p.run():进程启动时运行的方法，正是它去调用target指定的函数，我们自定义类的类中一定要实现该方法  

p.terminate():强制终止进程p，不会进行任何清理操作，如果p创建了子进程，该子进程就成了僵尸进程，使用该方法需要特别小心这种情况。如果p还保存了一个锁那么也将不会被释放，进而导致死锁
p.is_alive():如果p仍然运行，返回True

p.join([timeout]):主线程等待p终止（强调：是主线程处于等的状态，而p是处于运行的状态）。timeout是可选的超时时间。
```

**属性介绍：**

```
p.daemon：默认值为False，如果设为True，代表p为后台运行的守护进程，当p的父进程终止时，p也随之终止，并且设定为True后，p不能创建自己的新进程，必须在p.start()之前设置

p.name:进程的名称

p.pid：进程的pid
```















