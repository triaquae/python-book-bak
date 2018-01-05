## 本节重点

* 掌握线程queue的三种用法

> **本节时长需控制在5分钟内**

### 一 线程queue

queue is especially useful in threaded programming when information must be exchanged safely between multiple threads.

有三种不同的用法

**class queue.Queue\(maxsize=0\) \#队列：先进先出**

```
import queue

q=queue.Queue()
q.put('first')
q.put('second')
q.put('third')

print(q.get())
print(q.get())
print(q.get())



'''
结果(先进先出):
first
second
third
'''
```

**class queue.LifoQueue\(maxsize=0\) \#堆栈：last in fisrt out **

```
import queue

q=queue.LifoQueue()
q.put('first')
q.put('second')
q.put('third')

print(q.get())
print(q.get())
print(q.get())



'''
结果(后进先出):
third
second
first
'''
```

**class queue.PriorityQueue\(maxsize=0\) \#优先级队列：存储数据时可设置优先级的队列**

```
import queue

q=queue.PriorityQueue()
#put进入一个元组,元组的第一个元素是优先级(通常是数字,也可以是非数字之间的比较),数字越小优先级越高
q.put((20,'a'))
q.put((10,'b'))
q.put((30,'c'))

print(q.get())
print(q.get())
print(q.get())



'''
结果(数字越小优先级越高,优先级高的优先出队):
(10, 'b')
(20, 'a')
(30, 'c')
'''
```







