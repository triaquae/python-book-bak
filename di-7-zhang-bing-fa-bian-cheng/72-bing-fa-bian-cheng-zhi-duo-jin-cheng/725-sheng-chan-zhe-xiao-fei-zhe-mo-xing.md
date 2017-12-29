## 本节重点

* 了解互斥锁的概念

> **本节时长需控制在15分钟内**

### 一 互斥锁

进程之间数据不共享,但是共享同一套文件系统,所以访问同一个文件,或同一个打印终端,是没有问题的,而共享带来的是竞争，竞争带来的结果就是错乱，如下

```
#并发运行,效率高,但竞争同一打印终端,带来了打印错乱
from multiprocessing import Process
import os,time
def work():
    print('%s is running' %os.getpid())
    time.sleep(2)
    print('%s is done' %os.getpid())

if __name__ == '__main__':
    for i in range(3):
        p=Process(target=work)
        p.start()
```

如何控制，就是加锁处理。而互斥锁的意思就是互相排斥，如果把多个进程比喻为多个人，互斥锁的工作原理就是多个人都要去争抢同一个资源：卫生间，一个人抢到卫生间后上一把锁，其他人都要等着，等到这个完成任务后释放锁，其他人才有可能有一个抢到......所以互斥锁的原理，就是把并发改成穿行，降低了效率，但保证了数据安全不错乱

```
#由并发变成了串行,牺牲了运行效率,但避免了竞争
from multiprocessing import Process,Lock
import os,time
def work(lock):
    lock.acquire() #加锁
    print('%s is running' %os.getpid())
    time.sleep(2)
    print('%s is done' %os.getpid())
    lock.release() #释放锁
if __name__ == '__main__':
    lock=Lock()
    for i in range(3):
        p=Process(target=work,args=(lock,))
        p.start()
```

### 二 模拟抢票练习

多个进程共享同一文件，我们可以把文件当数据库，用多个进程模拟多个人执行抢票任务

```
#文件db.txt的内容为：{"count":1}
#注意一定要用双引号，不然json无法识别
from multiprocessing import Process
import time,json

def search(name):
    dic=json.load(open('db.txt'))
    time.sleep(1)
    print('\033[43m%s 查到剩余票数%s\033[0m' %(name,dic['count']))

def get(name):
    dic=json.load(open('db.txt'))
    time.sleep(1) #模拟读数据的网络延迟
    if dic['count'] >0:
        dic['count']-=1
        time.sleep(1) #模拟写数据的网络延迟
        json.dump(dic,open('db.txt','w'))
        print('\033[46m%s 购票成功\033[0m' %name)

def task(name):
    search(name)
    get(name)

if __name__ == '__main__':
    for i in range(10): #模拟并发10个客户端抢票
        name='<路人%s>' %i
        p=Process(target=task,args=(name,))
        p.start()
```

并发运行，效率高，但竞争写同一文件，数据写入错乱,只有一张票，卖成功给了10个人

```
<路人0> 查到剩余票数1
<路人1> 查到剩余票数1
<路人2> 查到剩余票数1
<路人3> 查到剩余票数1
<路人4> 查到剩余票数1
<路人5> 查到剩余票数1
<路人6> 查到剩余票数1
<路人7> 查到剩余票数1
<路人8> 查到剩余票数1
<路人9> 查到剩余票数1
<路人0> 购票成功
<路人4> 购票成功
<路人1> 购票成功
<路人5> 购票成功
<路人3> 购票成功
<路人7> 购票成功
<路人2> 购票成功
<路人6> 购票成功
<路人8> 购票成功
<路人9> 购票成功
```

加锁处理：购票行为由并发变成了串行，牺牲了运行效率，但保证了数据安全

```
#把文件db.txt的内容重置为：{"count":1}
from multiprocessing import Process,Lock
import time,json

def search(name):
    dic=json.load(open('db.txt'))
    time.sleep(1)
    print('\033[43m%s 查到剩余票数%s\033[0m' %(name,dic['count']))

def get(name):
    dic=json.load(open('db.txt'))
    time.sleep(1) #模拟读数据的网络延迟
    if dic['count'] >0:
        dic['count']-=1
        time.sleep(1) #模拟写数据的网络延迟
        json.dump(dic,open('db.txt','w'))
        print('\033[46m%s 购票成功\033[0m' %name)

def task(name,lock):
    search(name)
    with lock: #相当于lock.acquire(),执行完自代码块自动执行lock.release()
        get(name)

if __name__ == '__main__':
    lock=Lock()
    for i in range(10): #模拟并发10个客户端抢票
        name='<路人%s>' %i
        p=Process(target=task,args=(name,lock))
        p.start()
```

执行结果

```
<路人0> 查到剩余票数1
<路人1> 查到剩余票数1
<路人2> 查到剩余票数1
<路人3> 查到剩余票数1
<路人4> 查到剩余票数1
<路人5> 查到剩余票数1
<路人6> 查到剩余票数1
<路人7> 查到剩余票数1
<路人8> 查到剩余票数1
<路人9> 查到剩余票数1
<路人0> 购票成功
```

### 三 互斥锁与join

使用join可以将并发变成串行，互斥锁的原理也是将并发变成穿行，那我们直接使用join就可以了啊，为何还要互斥锁，说到这里我赶紧试了一下

```
#把文件db.txt的内容重置为：{"count":1}
from multiprocessing import Process,Lock
import time,json

def search(name):
    dic=json.load(open('db.txt'))
    print('\033[43m%s 查到剩余票数%s\033[0m' %(name,dic['count']))

def get(name):
    dic=json.load(open('db.txt'))
    time.sleep(1) #模拟读数据的网络延迟
    if dic['count'] >0:
        dic['count']-=1
        time.sleep(1) #模拟写数据的网络延迟
        json.dump(dic,open('db.txt','w'))
        print('\033[46m%s 购票成功\033[0m' %name)

def task(name,):
    search(name)
    get(name)

if __name__ == '__main__':
    for i in range(10):
        name='<路人%s>' %i
        p=Process(target=task,args=(name,))
        p.start()
        p.join()
```

执行结果

```
<路人0> 查到剩余票数1
<路人0> 购票成功
<路人1> 查到剩余票数0
<路人2> 查到剩余票数0
<路人3> 查到剩余票数0
<路人4> 查到剩余票数0
<路人5> 查到剩余票数0
<路人6> 查到剩余票数0
<路人7> 查到剩余票数0
<路人8> 查到剩余票数0
<路人9> 查到剩余票数0 
```

发现使用join将并发改成穿行，确实能保证数据安全，但问题是连查票操作也变成只能一个一个人去查了，很明显大家查票时应该是并发地去查询而无需考虑数据准确与否，此时join与互斥锁的区别就显而易见了，join是将一个任务整体串行，而互斥锁的好处则是可以将一个任务中的某一段代码串行，比如只让task函数中的get任务串行

```
def task(name,):
    search(name) # 并发执行
    
    lock.acquire()
    get(name) #串行执行
    lock.release()
```

### 四 总结

加锁可以保证多个进程修改同一块数据时，同一时间只能有一个任务可以进行修改，即串行地修改，没错，速度是慢了，但牺牲了速度却保证了数据安全。

虽然可以用文件共享数据实现进程间通信，但问题是：

1、效率低（共享数据基于文件，而文件是硬盘上的数据）

2、需要自己加锁处理



因此我们最好找寻一种解决方案能够兼顾：

1、效率高（多个进程共享一块内存的数据）

2、帮我们处理好锁问题。

这就是mutiprocessing模块为我们提供的基于消息的IPC通信机制：队列和管道。

队列和管道都是将数据存放于内存中，而队列又是基于（管道+锁）实现的，可以让我们从复杂的锁问题中解脱出来，因而队列才是进程间通信的最佳选择。

我们应该尽量避免使用共享数据，尽可能使用消息传递和队列，避免处理复杂的同步和锁问题，而且在进程数目增多时，往往可以获得更好的可获展性。







