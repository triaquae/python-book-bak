## 本节重点

* 掌握在一个进程下开启多个子进程与在一个进程下开启多个线程的区别

> **本节时长需控制在15分钟内**

### 一 **谁的开启速度快？**

**1、在主进程下开启线程**

```
from threading import Thread

def work():
    print('hello')

if __name__ == '__main__':
    t=Thread(target=work)
    t.start()
    print('主线程/主进程')
```

执行结果如下，几乎是t.start \(\)的同时就将线程开启了，然后先打印出了hello，证明线程的创建开销极小

```
hello
主线程/主进程
```

**2、在主进程下开启子进程**

```
from multiprocessing import Process

def work():
    print('hello')

if __name__ == '__main__':
    #在主进程下开启子进程
    p=Process(target=work)
    p.start()
    print('主线程/主进程')
```

执行结果如下，p.start \(\)将开启进程的信号发给操作系统后，操作系统要申请内存空间，让好拷贝父进程地址空间到子进程，开销远大于线程

```
主线程/主进程
hello
```

### 二 瞅一瞅pid？

**1、在主进程下开启多个线程,每个线程都跟主进程的pid一样**

```
from threading import Thread
import os

def work():
    print('hello',os.getpid())

if __name__ == '__main__':
    t1=Thread(target=work)
    t2=Thread(target=work)
    t1.start()
    t2.start()
    print('主线程/主进程pid',os.getpid())
```

执行结果

```
hello 7939
hello 7939
主线程/主进程 7939
```

**2、开多个进程,每个进程都有不同的pid**

```
from multiprocessing import Process
import os

def work():
    print('hello',os.getpid())

if __name__ == '__main__':
    p1=Process(target=work)
    p2=Process(target=work)
    p1.start()
    p2.start()
    print('主线程/主进程',os.getpid())
```

执行结果

```
主线程/主进程 7951
hello 7952
hello 7953
```

### 三 同一进程内的线程共享该进程的数据？

**1、进程之间地址空间是隔离的**

```
from multiprocessing import Process
import os

def work():
    global n
    n=0

if __name__ == '__main__':
    n=100
    p=Process(target=work)
    p.start()
    p.join()
    print('主',n)
```

执行结果如下，毫无疑问子进程p已经将自己的全局的n改成了0,但改的仅仅是它自己的,查看父进程的n仍然为100

```
主 100
```

**2、同一进程内开启的多个线程是共享该进程地址空间的**

```
from threading import Thread
import os

def work():
    global n
    n=0

if __name__ == '__main__':
    n=100
    t=Thread(target=work)
    t.start()
    t.join()
    print('主',n)
```

执行结果如下， 查看结果为0,因为同一进程内的线程之间共享进程内的数据

```
主 0  
```



