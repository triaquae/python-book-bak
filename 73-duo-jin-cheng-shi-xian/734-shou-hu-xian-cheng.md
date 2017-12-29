## 本节重点

* 了解守护线程的概念
* 了解守护线程与守护进程的区别

> **本节时长需控制在15分钟内**

### 一 守护线程

无论是进程还是线程，都遵循：守护xxx会等待主xxx运行完毕后被销毁

需要强调的是：运行完毕并非终止运行

```
1、对主进程来说，运行完毕指的是主进程代码运行完毕

2、对主线程来说，运行完毕指的是主线程所在的进程内所有非守护线程统统运行完毕，主线程才算运行完毕
```

详细解释：

```
1、主进程在其代码结束后就已经算运行完毕了（守护进程在此时就被回收）,然后主进程会一直等非守护的子进程都运行完毕后回收子进程的资源(否则会产生僵尸进程)，才会结束，

2、主线程在其他非守护线程运行完毕后才算运行完毕（守护线程在此时就被回收）。因为主线程的结束意味着进程的结束，进程整体的资源都将被回收，而进程必须保证非守护线程都运行完毕后才能结束。
```

验证

```
from threading import Thread
import time
def sayhi(name):
    time.sleep(2)
    print('%s say hello' %name)

if __name__ == '__main__':
    t=Thread(target=sayhi,args=('egon',))
    t.setDaemon(True) #必须在t.start()之前设置
    t.start()

    print('主线程')
    print(t.is_alive())
```

执行结果

```
主线程
True
```

### 二 练习

思考下述代码的执行结果有可能是哪些情况？为什么？

```
from threading import Thread
import time

def foo():
    print(123)
    time.sleep(1)
    print("end123")

def bar():
    print(456)
    time.sleep(3)
    print("end456")

if __name__ == '__main__':
    t1=Thread(target=foo)
    t2=Thread(target=bar)

    t1.daemon=True
    t1.start()
    t2.start()
    print("main-------")
```



