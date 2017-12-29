## 本节重点

* 掌握队列的使用

> **本节时长需控制在5分钟内**

### 队列介绍

进程彼此之间互相隔离，要实现进程间通信（IPC），multiprocessing模块支持两种形式：队列和管道，这两种方式都是使用消息传递的

**创建队列的类（底层就是以管道和锁定的方式实现）**：

```
Queue([maxsize]):创建共享的进程队列，Queue是多进程安全的队列，可以使用Queue实现多进程之间的数据传递。 
```

**参数介绍：**

```
maxsize是队列中允许最大项数，省略则无大小限制。
但需要明确：
    1、队列内存放的是消息而非大数据
    2、队列占用的是内存空间，因而maxsize即便是无大小限制也受限于内存大小
```

**主要方法介绍：**

```
q.put方法用以插入数据到队列中。
q.get方法可以从队列读取并且删除一个元素。
```

**队列的使用**

```
from multiprocessing import Process,Queue

q=Queue(3)

#put ,get ,put_nowait,get_nowait,full,empty
q.put(1)
q.put(2)
q.put(3)
print(q.full()) #满了
# q.put(4) #再放就阻塞住了

print(q.get())
print(q.get())
print(q.get())
print(q.empty()) #空了
# print(q.get()) #再取就阻塞住了
```





