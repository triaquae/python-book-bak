## 本节重点

* 掌握多路复用IO模型

> **本节时长需控制在15分钟内**

### 多路复用IO\(IO multiplexing\)

IO multiplexing这个词可能有点陌生，但是如果我说select/epoll，大概就都能明白了。有些地方也称这种IO方式为**事件驱动IO**

\(event driven IO\)。我们都知道，select/epoll的好处就在于单个process就可以同时处理多个网络连接的IO。它的基本原理就是select/epoll这个function会不断的轮询所负责的所有socket，当某个socket有数据到达了，就通知用户进程。它的流程如图：

![](/assets/chapter7/多路复用IO.png)

```
当用户进程调用了select，那么整个进程会被block，而同时，kernel会“监视”所有select负责的socket，
当任何一个socket中的数据准备好了，select就会返回。这个时候用户进程再调用read操作，将数据从kernel拷贝到用户进程。  
这个图和blocking IO的图其实并没有太大的不同，事实上还更差一些。因为这里需要使用两个系统调用\(select和recvfrom\)，
而blocking IO只调用了一个系统调用\(recvfrom\)。但是，用select的优势在于它可以同时处理多个connection。
```

**    强调：**

**    1. 如果处理的连接数不是很高的话，使用select/epoll的web server不一定比使用multi-threading + blocking IO的web server性能更好，可能延迟还更大。select/epoll的优势并不是对于单个连接能处理得更快，而是在于能处理更多的连接。**

**    2. 在多路复用模型中，对于每一个socket，一般都设置成为non-blocking，但是，如上图所示，整个用户的process其实是一直被block的。只不过process是被select这个函数block，而不是被socket IO给block。**

**结论: select的优势在于可以处理多个连接，不适用于单个连接**

select网络IO模型示例

```
#服务端
from socket import *
import select
server = socket(AF_INET, SOCK_STREAM)
server.bind(('127.0.0.1',8093))
server.listen(5)
server.setblocking(False)
print('starting...')

rlist=[server,]
wlist=[]
wdata={}

while True:
    rl,wl,xl=select.select(rlist,wlist,[],0.5)
    print(wl)
    for sock in rl:
        if sock == server:
            conn,addr=sock.accept()
            rlist.append(conn)
        else:
            try:
                data=sock.recv(1024)
                if not data:
                    sock.close()
                    rlist.remove(sock)
                    continue
                wlist.append(sock)
                wdata[sock]=data.upper()
            except Exception:
                sock.close()
                rlist.remove(sock)

    for sock in wl:
        sock.send(wdata[sock])
        wlist.remove(sock)
        wdata.pop(sock)


#客户端
from socket import *
c=socket(AF_INET,SOCK_STREAM)
c.connect(('127.0.0.1',8081))

while True:
    msg=input('>>: ')
    if not msg:continue
    c.send(msg.encode('utf-8'))
    data=c.recv(1024)
    print(data.decode('utf-8'))
```

**select监听fd变化的过程分析：**

```
用户进程创建socket对象，拷贝监听的fd到内核空间，每一个fd会对应一张系统文件表，内核空间的fd响应到数据后，
就会发送信号给用户进程数据已到；
用户进程再发送系统调用，比如（accept）将内核空间的数据copy到用户空间，同时作为接受数据端内核空间的数据清除，
这样重新监听时fd再有新的数据又可以响应到了（发送端因为基于TCP协议所以需要收到应答后才会清除）。
```

**该模型的优点：**

```
相比其他模型，使用select() 的事件驱动模型只用单线程（进程）执行，占用资源少，不消耗太多 CPU，同时能够为多客户端提供服务。
如果试图建立一个简单的事件驱动的服务器程序，这个模型有一定的参考价值。
```

**该模型的缺点：**

```
首先select()接口并不是实现“事件驱动”的最好选择。因为当需要探测的句柄值较大时，select()接口本身需要消耗大量时间去轮询各个句柄。
很多操作系统提供了更为高效的接口，如linux提供了epoll，BSD提供了kqueue，Solaris提供了/dev/poll，…。
如果需要实现更高效的服务器程序，类似epoll这样的接口更被推荐。遗憾的是不同的操作系统特供的epoll接口有很大差异，
所以使用类似于epoll的接口实现具有较好跨平台能力的服务器会比较困难。
其次，该模型将事件探测和事件响应夹杂在一起，一旦事件响应的执行体庞大，则对整个模型是灾难性的。
```



