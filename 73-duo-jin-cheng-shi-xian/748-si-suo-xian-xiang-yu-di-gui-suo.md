## 本节重点

* 了解死锁现象与解决方法

> **本节时长需控制在15分钟内**

### 一 死锁现象

所谓死锁： 是指两个或两个以上的进程或线程在执行过程中，因争夺资源而造成的一种互相等待的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程称为死锁进程，如下就是死锁

```
from threading import Thread,Lock
import time
mutexA=Lock()
mutexB=Lock()

class MyThread(Thread):
    def run(self):
        self.func1()
        self.func2()
    def func1(self):
        mutexA.acquire()
        print('\033[41m%s 拿到A锁\033[0m' %self.name)

        mutexB.acquire()
        print('\033[42m%s 拿到B锁\033[0m' %self.name)
        mutexB.release()

        mutexA.release()

    def func2(self):
        mutexB.acquire()
        print('\033[43m%s 拿到B锁\033[0m' %self.name)
        time.sleep(2)

        mutexA.acquire()
        print('\033[44m%s 拿到A锁\033[0m' %self.name)
        mutexA.release()

        mutexB.release()

if __name__ == '__main__':
    for i in range(10):
        t=MyThread()
        t.start()
```

执行效果

```
Thread-1 拿到A锁
Thread-1 拿到B锁
Thread-1 拿到B锁
Thread-2 拿到A锁 #出现死锁，整个程序阻塞住
```

### 二 递归锁

解决方法，递归锁，在Python中为了支持在同一线程中多次请求同一资源，python提供了可重入锁RLock。

这个RLock内部维护着一个Lock和一个counter变量，counter记录了acquire的次数，从而使得资源可以被多次require。直到一个线程所有的acquire都被release，其他的线程才能获得资源。上面的例子如果使用RLock代替Lock，则不会发生死锁，二者的区别是：递归锁可以连续acquire多次，而互斥锁只能acquire一次

```
from threading import Thread,RLock
import time

mutexA=mutexB=RLock() #一个线程拿到锁，counter加1,该线程内又碰到加锁的情况，则counter继续加1，这期间所有其他线程都只能等待，等待该线程释放所有锁，即counter递减到0为止

class MyThread(Thread):
    def run(self):
        self.func1()
        self.func2()
    def func1(self):
        mutexA.acquire()
        print('\033[41m%s 拿到A锁\033[0m' %self.name)

        mutexB.acquire()
        print('\033[42m%s 拿到B锁\033[0m' %self.name)
        mutexB.release()

        mutexA.release()

    def func2(self):
        mutexB.acquire()
        print('\033[43m%s 拿到B锁\033[0m' %self.name)
        time.sleep(2)

        mutexA.acquire()
        print('\033[44m%s 拿到A锁\033[0m' %self.name)
        mutexA.release()

        mutexB.release()

if __name__ == '__main__':
    for i in range(10):
        t=MyThread()
        t.start()
```





