## 本节重点

* 掌握进程池与线程池的用法
* 掌回调函数

> **本节时长需控制在30分钟内**

### 一 进程池与线程池

在刚开始学多进程或多线程时，我们迫不及待地基于多进程或多线程实现并发的套接字通信，然而这种实现方式的致命缺陷是：服务的开启的进程数或线程数都会随着并发的客户端数目地增多而增多，这会对服务端主机带来巨大的压力，甚至于不堪重负而瘫痪，于是我们必须对服务端开启的进程数或线程数加以控制，让机器在一个自己可以承受的范围内运行，这就是进程池或线程池的用途，例如进程池，就是用来存放进程的池子，本质还是基于多进程，只不过是对开启进程的数目加上了限制

**介绍**

```
官网：https://docs.python.org/dev/library/concurrent.futures.html

concurrent.futures模块提供了高度封装的异步调用接口
ThreadPoolExecutor：线程池，提供异步调用
ProcessPoolExecutor: 进程池，提供异步调用
Both implement the same interface, which is defined by the abstract Executor class.
```

**基本方法**

```
1、submit(fn, *args, **kwargs)
异步提交任务

2、map(func, *iterables, timeout=None, chunksize=1) 
取代for循环submit的操作

3、shutdown(wait=True) 
相当于进程池的pool.close()+pool.join()操作
wait=True，等待池内所有任务执行完毕回收完资源后才继续
wait=False，立即返回，并不会等待池内的任务执行完毕
但不管wait参数为何值，整个程序都会等到所有任务执行完毕
submit和map必须在shutdown之前

4、result(timeout=None)
取得结果

5、add_done_callback(fn)
回调函数
```

### 二 进程池

**介绍**

```
The ProcessPoolExecutor class is an Executor subclass that uses a pool of processes to execute calls asynchronously. ProcessPoolExecutor uses the multiprocessing module, which allows it to side-step the Global Interpreter Lock but also means that only picklable objects can be executed and returned.

class concurrent.futures.ProcessPoolExecutor(max_workers=None, mp_context=None)
An Executor subclass that executes calls asynchronously using a pool of at most max_workers processes. If max_workers is None or not given, it will default to the number of processors on the machine. If max_workers is lower or equal to 0, then a ValueError will be raised.
```

**用法**

```
from concurrent.futures import ThreadPoolExecutor,ProcessPoolExecutor

import os,time,random
def task(n):
    print('%s is runing' %os.getpid())
    time.sleep(random.randint(1,3))
    return n**2

if __name__ == '__main__':

    executor=ProcessPoolExecutor(max_workers=3)

    futures=[]
    for i in range(11):
        future=executor.submit(task,i)
        futures.append(future)
    executor.shutdown(True)
    print('+++>')
    for future in futures:
        print(future.result())
```

### 三 线程池

**介绍**

```
ThreadPoolExecutor is an Executor subclass that uses a pool of threads to execute calls asynchronously.
class concurrent.futures.ThreadPoolExecutor(max_workers=None, thread_name_prefix='')
An Executor subclass that uses a pool of at most max_workers threads to execute calls asynchronously.

Changed in version 3.5: If max_workers is None or not given, it will default to the number of processors on the machine, multiplied by 5, assuming that ThreadPoolExecutor is often used to overlap I/O instead of CPU work and the number of workers should be higher than the number of workers for ProcessPoolExecutor.

New in version 3.6: The thread_name_prefix argument was added to allow users to control the threading.Thread names for worker threads created by the pool for easier debugging.
```

**用法**

```
把ProcessPoolExecutor换成ThreadPoolExecutor，其余用法全部相同
```

### 四 map方法

```
from concurrent.futures import ThreadPoolExecutor,ProcessPoolExecutor

import os,time,random
def task(n):
    print('%s is runing' %os.getpid())
    time.sleep(random.randint(1,3))
    return n**2

if __name__ == '__main__':

    executor=ThreadPoolExecutor(max_workers=3)

    # for i in range(11):
    #     future=executor.submit(task,i)

    executor.map(task,range(1,12)) #map取代了for+submit
```

### 五 回调函数

可以为进程池或线程池内的每个进程或线程绑定一个函数，该函数在进程或线程的任务执行完毕后自动触发，并接收任务的返回值当作参数，该函数称为回调函数

```
from concurrent.futures import ThreadPoolExecutor,ProcessPoolExecutor
from multiprocessing import Pool
import requests
import json
import os

def get_page(url):
    print('<进程%s> get %s' %(os.getpid(),url))
    respone=requests.get(url)
    if respone.status_code == 200:
        return {'url':url,'text':respone.text}

def parse_page(res):
    res=res.result()
    print('<进程%s> parse %s' %(os.getpid(),res['url']))
    parse_res='url:<%s> size:[%s]\n' %(res['url'],len(res['text']))
    with open('db.txt','a') as f:
        f.write(parse_res)


if __name__ == '__main__':
    urls=[
        'https://www.baidu.com',
        'https://www.python.org',
        'https://www.openstack.org',
        'https://help.github.com/',
        'http://www.sina.com.cn/'
    ]

    p=ProcessPoolExecutor(3)
    for url in urls:
        p.submit(get_page,url).add_done_callback(parse_page) #parse_page拿到的是一个future对象obj，需要用obj.result()拿到结果
```



