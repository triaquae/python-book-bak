## 本节重点

* 掌握什么是线程
* 掌握线程与进程的区别

> **本节时长需控制在30分钟内**

### 一 什么是线程

在传统操作系统中，每个进程有一个地址空间，而且默认就有一个控制线程

线程顾名思义，就是一条流水线工作的过程（流水线的工作需要电源，电源就相当于cpu），而一条流水线必须属于一个车间，一个车间的工作过程是一个进程，车间负责把资源整合到一起，是一个资源单位，而一个车间内至少有一条流水线。

**所以，进程只是用来把资源集中到一起（进程只是一个资源单位，或者说资源集合），而线程才是cpu上的执行单位。**



多线程（即多个控制线程）的概念是，在一个进程中存在多个线程，多个线程共享该进程的地址空间，相当于一个车间内有多条流水线，都共用一个车间的资源。例如，北京地铁与上海地铁是不同的进程，而北京地铁里的13号线是一个线程，北京地铁所有的线路共享北京地铁所有的资源，比如所有的乘客可以被所有线路拉。

### 二 线程与进程的区别

1. Threads share the address space of the process that created it; processes have their own address space.
2. Threads have direct access to the data segment of its process; processes have their own copy of the data segment of the parent process.
3. Threads can directly communicate with other threads of its process; processes must use interprocess communication to communicate with sibling processes.
4. New threads are easily created; new processes require duplication of the parent process.
5. Threads can exercise considerable control over threads of the same process; processes can only exercise control over child processes.
6. Changes to the main thread \(cancellation, priority change, etc.\) may affect the behavior of the other threads of the process; changes to the parent process does not affect child processes.

总结上述区别，无非两个关键点，这也是我们在特定的场景下需要使用多线程的原因：

1. 同一个进程内的多个线程共享该进程内的地址资源
2. 创建线程的开销要远小于创建进程的开销（创建一个进程，就是创建一个车间，涉及到申请空间，而且在该空间内建至少一条流水线，但创建线程，就只是在一个车间内造一条流水线，无需申请空间，所以创建开销小）

### 三 多线程应用举例

开启一个字处理软件进程，该进程肯定需要办不止一件事情，比如监听键盘输入，处理文字，定时自动将文字保存到硬盘，这三个任务操作的都是同一块数据，因而不能用多进程。只能在一个进程里并发地开启三个线程,如果是单线程，那就只能是，键盘输入时，不能处理文字和自动保存，自动保存时又不能输入和处理文字。

![](/assets/chapter7/多线程应用举例.png)



