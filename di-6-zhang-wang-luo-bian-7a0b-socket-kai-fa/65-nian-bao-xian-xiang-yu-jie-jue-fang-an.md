## 本节重点：

* 使学生了解粘包原理
* 让学生掌握粘包解决方案

> **本节时长需控制在70-80分钟内**

### 简单远程执行命令程序开发\(30分钟\)

是时候用户socket干点正事呀，我们来写一个远程执行命令的程序，写一个socket client端在windows端发送指令，一个socket server在Linux端执行命令并返回结果给客户端

执行命令的话，肯定是用我们学过的subprocess模块啦，但**注意注意注意：**

```py
res = subprocess.Popen(cmd.decode('utf-8'),shell=True,stderr=subprocess.PIPE,stdout=subprocess.PIPE)
```

命令结果的编码是以当前所在的系统为准的，如果是windows，那么**res.stdout.read\(\)读出的就是GBK编码的**，在接收端需**要用GBK解码，且只能从管道里读一次结果**

_**ssh server**_

```py
import socket
import subprocess

ip_port = ('127.0.0.1', 8080)


tcp_socket_server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcp_socket_server.bind(ip_port)
tcp_socket_server.listen(5)

while True:
    conn, addr = tcp_socket_server.accept()
    print('客户端', addr)

    while True:
        cmd = conn.recv(1024)
        if len(cmd) == 0: break
        print("recv cmd",cmd)
        res = subprocess.Popen(cmd.decode('utf-8'), shell=True,
                               stdout=subprocess.PIPE,
                               stdin=subprocess.PIPE,
                               stderr=subprocess.PIPE)

        stderr = res.stderr.read()
        stdout = res.stdout.read()
        print("res length",len(stdout))
        conn.send(stderr)
        conn.send(stdout)
```

_**ssh client **_

```py
import socket
ip_port = ('127.0.0.1', 8080)

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
res = s.connect_ex(ip_port)

while True:
    msg = input('>>: ').strip()
    if len(msg) == 0: continue
    if msg == 'quit': break

    s.send(msg.encode('utf-8'))
    act_res = s.recv(1024)

    print(act_res.decode('utf-8'), end='')
```

尝试执行ls、pwd命令,你惊喜的发现，拿到了正确的结果！

but 莫开心太早，此时执行一个结果比较长的命令，比如top -bn 1， 你发现依然可以拿到结果，但如果再执行一条df -h的话，就发现，你拿到并不是df命令的结果，而是上一条top命令的部分结果。为啥捏？为啥捏？为啥捏？

是因为，top命令的结果比较长，但客户端只recv\(1024\), 可结果比1024长呀，那怎么办，只好在服务器端的IO缓冲区里把客户端还没收走的暂时存下来，等客户端下次再来收，所以当客户端第2次调用recv\(1024\)就会首先把上次没收完的数据先收下来，再收df命令的结果。

那怎么解决呢？ 有些同学说，直接把recv\(1024\)改大不就好了，改成5000\10000或whatever. 可我的亲，这么干的话，并不能解决实际问题，因为你不可能提前知道对方返回的结果数据大下，无论你改成多大，对方的结果都有可能比你设置的大，另外这个recv并不是真的可以随便改特别大的，有关部门建议的不要超过8192，再大反而会出现影响收发速度和不稳定的情况

同志们，这个现象叫做粘包，就是指两次结果粘到一起了。它的发生主要是因为socket缓冲区导致的，来看一下

![](/assets/6.5 buffer .png)

你的程序实际上无权直接操作网卡的，你操作网卡都是通过操作系统给用户程序暴露出来的接口，那每次你的程序要给远程发数据时，其实是先把数据从用户态copy到内核态，这样的操作是耗资源和时间的，频繁的在内核态和用户态之前交换数据势必会导致发送效率降低， 因此socket 为提高传输效率，发送方往往要收集到足够多的数据后才发送一次数据给对方。若连续几次需要send的数据都很少，通常TCP socket 会根据优化算法把这些数据合成一个TCP段后一次发送出去，这样接收方就收到了粘包数据。

**粘包问题只存在于TCP中，Not UDP**

还是看上图，发送端可以是一K一K地发送数据，而接收端的应用程序可以两K两K地提走数据，当然也有可能一次提走3K或6K数据，或者一次只提走几个字节的数据，也就是说，应用程序所看到的数据是一个整体，或说是一个流（stream），一条消息有多少字节对应用程序是不可见的，因此TCP协议是面向流的协议，这也是容易出现粘包问题的原因。而UDP是面向消息的协议，每个UDP段都是一条消息，应用程序必须以消息为单位提取数据，不能一次提取任意字节的数据，这一点和TCP是很不同的。怎样定义消息呢？可以认为对方一次性write/send的数据为一个消息，需要明白的是当对方send一条信息的时候，无论底层怎样分段分片，TCP协议层会把构成整条消息的数据段排序完成后才呈现在内核缓冲区。

例如基于tcp的套接字客户端往服务端上传文件，发送时文件内容是按照一段一段的字节流发送的，在接收方看了，根本不知道该文件的字节流从何处开始，在何处结束

所谓粘包问题主要还是因为接收方不知道消息之间的界限，不知道一次性提取多少字节的数据所造成的。

**总结**

1. TCP（transport control protocol，传输控制协议）是面向连接的，面向流的，提供高可靠性服务。收发两端（客户端和服务器端）都要有一一成对的socket，因此，发送端为了将多个发往接收端的包，更有效的发到对方，使用了优化方法（Nagle算法），将多次间隔较小且数据量小的数据，合并成一个大的数据块，然后进行封包。这样，接收端，就难于分辨出来了，必须提供科学的拆包机制。 即面向流的通信是无消息保护边界的。
2. UDP（user datagram protocol，用户数据报协议）是无连接的，面向消息的，提供高效率服务。不会使用块的合并优化算法，, 由于UDP支持的是一对多的模式，所以接收端的skbuff\(套接字缓冲区）采用了链式结构来记录每一个到达的UDP包，在每个UDP包中就有了消息头（消息来源地址，端口等信息），这样，对于接收端来说，就容易进行区分处理了。 
   **即面向消息的通信是有消息保护边界的。**
3. **tcp是基于数据流的，于是收发的消息不能为空，这就需要在客户端和服务端都添加空消息的处理机制，防止程序卡住，而udp是基于数据报的，即便是你输入的是空内容（直接回车），那也不是空消息，udp协议会帮你封装上消息头，实验略**

#### 基于UDP的命令执行程序\(10分钟\)

上面说了，udp不存在粘包问题，我们看一下实例

udp server

```py
import socket
import subprocess

ip_port = ('127.0.0.1', 9003)
bufsize = 1024

udp_server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
udp_server.bind(ip_port)

while True:
    # 收消息
    cmd, addr = udp_server.recvfrom(bufsize)
    print('用户命令----->', cmd,addr)

    # 逻辑处理
    res = subprocess.Popen(cmd.decode('utf-8'), shell=True, stderr=subprocess.PIPE, stdin=subprocess.PIPE,
                           stdout=subprocess.PIPE)
    stderr = res.stderr.read()
    stdout = res.stdout.read()

    # 发消息
    udp_server.sendto(stdout + stderr, addr)

udp_server.close()
```

udp client

```py
from socket import *

import time

ip_port = ('127.0.0.1', 9003)
bufsize = 1024

udp_client = socket(AF_INET, SOCK_DGRAM)

while True:
    msg = input('>>: ').strip()
    if len(msg) == 0:
        continue

    udp_client.sendto(msg.encode('utf-8'), ip_port)
    data, addr = udp_client.recvfrom(bufsize)
    print(data.decode('utf-8'), end='')
```

### 

### 粘包的解决办法\(35分钟\)

问题的根源在于，接收端不知道发送端将要传送的字节流的长度，所以解决粘包的方法就是围绕，如何让发送端在发送数据前，把自己将要发送的字节流总大小让接收端知晓，然后接收端来一个死循环接收完所有数据

#### 普通青年版

服务器端

```py
import socket,subprocess
ip_port=('127.0.0.1',8080)
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

s.bind(ip_port)
s.listen(5)

while True:
    conn,addr=s.accept()
    print('客户端',addr)
    while True:
        msg=conn.recv(1024)
        if not msg:break
        res=subprocess.Popen(msg.decode('utf-8'),shell=True,\
                            stdin=subprocess.PIPE,\
                         stderr=subprocess.PIPE,\
                         stdout=subprocess.PIPE)
        err=res.stderr.read()
        if err:
            ret=err
        else:
            ret=res.stdout.read()
        data_length=len(ret)
        conn.send(str(data_length).encode('utf-8'))
        data=conn.recv(1024).decode('utf-8')
        if data == 'recv_ready':
            conn.sendall(ret)
    conn.close()
```

客户端

```
import socket,time
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
res=s.connect_ex(('127.0.0.1',8080))

while True:
    msg=input('>>: ').strip()
    if len(msg) == 0:continue
    if msg == 'quit':break

    s.send(msg.encode('utf-8'))
    length=int(s.recv(1024).decode('utf-8'))
    s.send('recv_ready'.encode('utf-8'))
    send_size=0
    recv_size=0
    data=b''
    while recv_size < length:
        data+=s.recv(1024)
        recv_size+=len(data) #为什么不直接写1024？


    print(data.decode('utf-8'))
```

> 为何low？
>
> 程序的运行速度远快于网络传输速度，所以在发送一段字节前，先用send去发送该字节流长度，这种方式会放大网络延迟带来的性能损耗

刚才上面 在发送消息之前需先发送消息长度给对端，还必须要等对端返回一个ready收消息的确认，不等到对端确认就直接发消息的话，还是会产生粘包问题\(承载消息长度的那条消息和消息本身粘在一起\)。 有没有优化的好办法么？

#### 文艺青年版一

思考一个问题，为什么不能在发送了消息长度\(称为消息头head吧\)给对端后，立刻发消息内容\(称为body吧\)，是因为怕head 和body 粘在一起，所以通过等对端返回确认来把两条消息中断开。

可不可以直接发head + body,但又能让对端区分出哪个是head，哪个是body呢？我靠、我靠，感觉智商要涨了。

想到了，把head设置成定长的呀，这样对端只要收消息时，先固定收定长的数据，head里写好，后面还有多少是属于这条消息的数据，然后直接写个循环收下来不就完了嘛！唉呀妈呀，我真机智。

可是、可是如何制作定长的消息头呢？假设你有2条消息要发送，第一条消息长度是 3000个字节，第2条消息是200字节。如果消息头只包含消息长度的话，那两个消息的消息头分别是

```
len(msg1) = 4000 = 4字节
len(msg2) = 200 = 3字节
```

你的服务端如何完整的收到这个消息头呢？是recv\(3\)还是recv\(4\)服务器端怎么知道？用尽我所有知识，我只能想到拼接字符串的办法了，打比方就是设置消息头固定100字节长，不够的拿空字符串去拼接。

server

```py
import socket,json
import subprocess

ip_port = ('127.0.0.1', 8080)

tcp_socket_server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcp_socket_server.setsockopt(socket.SOL_SOCKET,socket.SO_REUSEADDR,1) #一行代码搞定，写在bind之前
tcp_socket_server.bind(ip_port)
tcp_socket_server.listen(5)

def pack_msg_header(header,size):
    bytes_header = bytes(json.dumps(header),encoding="utf-8")
    fill_up_size = size -  len(bytes_header)
    print("need to fill up ",fill_up_size)

    header['fill'] = header['fill'].zfill(fill_up_size)
    print("new header",header)
    bytes_new_header = bytes(bytes(json.dumps(header),encoding="utf-8"))
    return bytes_new_header

while True:
    conn, addr = tcp_socket_server.accept()
    print('客户端', addr)

    while True:
        cmd = conn.recv(1024)
        if len(cmd) == 0: break
        print("recv cmd",cmd)
        res = subprocess.Popen(cmd.decode('utf-8'), shell=True,
                               stdout=subprocess.PIPE,
                               stdin=subprocess.PIPE,
                               stderr=subprocess.PIPE)

        stderr = res.stderr.read()
        stdout = res.stdout.read()
        print("res length",len(stdout))

        msg_header = {
            'length':len(stdout + stderr),
            'fill':''
        }
        packed_header = pack_msg_header(msg_header,100)
        print("packed header size",packed_header,len(packed_header))
        conn.send(packed_header)
        conn.send(stdout + stderr)
```

client

```py
import socket
import json

ip_port = ('127.0.0.1', 8080)

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
res = s.connect_ex(ip_port)

while True:
    msg = input('>>: ').strip()
    if len(msg) == 0: continue
    if msg == 'quit': break

    s.send(msg.encode('utf-8'))
    response_msg_header = s.recv(100).decode("utf-8")

    response_msg_header_data = json.loads(response_msg_header)
    msg_size = response_msg_header_data['length']

    res = s.recv(msg_size)
    print("received res size ",len(res))
    print(res.decode('utf-8'), end='')
```

#### 文艺青年版二

为字节流加上自定义固定长度报头也可以借助于第三方模块struct，用法为

```
import json,struct
#假设通过客户端上传1T:1073741824000的文件a.txt

#为避免粘包,必须自定制报头
header={'file_size':1073741824000,'file_name':'/a/b/c/d/e/a.txt','md5':'8f6fbf8347faa4924a76856701edb0f3'} #1T数据,文件路径和md5值

#为了该报头能传送,需要序列化并且转为bytes
head_bytes=bytes(json.dumps(header),encoding='utf-8') #序列化并转成bytes,用于传输

#为了让客户端知道报头的长度,用struck将报头长度这个数字转成固定长度:4个字节
head_len_bytes=struct.pack('i',len(head_bytes)) #这4个字节里只包含了一个数字,该数字是报头的长度

#客户端开始发送
conn.send(head_len_bytes) #先发报头的长度,4个bytes
conn.send(head_bytes) #再发报头的字节格式
conn.sendall(文件内容) #然后发真实内容的字节格式

#服务端开始接收
head_len_bytes=s.recv(4) #先收报头4个bytes,得到报头长度的字节格式
x=struct.unpack('i',head_len_bytes)[0] #提取报头的长度

head_bytes=s.recv(x) #按照报头长度x,收取报头的bytes格式
header=json.loads(json.dumps(header)) #提取报头

#最后根据报头的内容提取真实的数据,比如
real_data_len=s.recv(header['file_size'])
s.recv(real_data_len)
```

使用struct模块实现方式如下

server

```
import socket,struct,json
import subprocess
phone=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
phone.setsockopt(socket.SOL_SOCKET,socket.SO_REUSEADDR,1) #就是它，在bind前加

phone.bind(('127.0.0.1',8080))

phone.listen(5)

while True:
    conn,addr=phone.accept()
    while True:
        cmd=conn.recv(1024)
        if not cmd:break
        print('cmd: %s' %cmd)

        res=subprocess.Popen(cmd.decode('utf-8'),
                             shell=True,
                             stdout=subprocess.PIPE,
                             stderr=subprocess.PIPE)
        err=res.stderr.read()
        print(err)
        if err:
            back_msg=err
        else:
            back_msg=res.stdout.read()

        headers={'data_size':len(back_msg)}
        head_json=json.dumps(headers)
        head_json_bytes=bytes(head_json,encoding='utf-8')

        conn.send(struct.pack('i',len(head_json_bytes))) #先发报头的长度
        conn.send(head_json_bytes) #再发报头
        conn.sendall(back_msg) #在发真实的内容

    conn.close()
```

client

```
from socket import *
import struct,json

ip_port=('127.0.0.1',8080)
client=socket(AF_INET,SOCK_STREAM)
client.connect(ip_port)

while True:
    cmd=input('>>: ')
    if not cmd:continue
    client.send(bytes(cmd,encoding='utf-8'))

    head=client.recv(4) #先收4个bytes，这里4个bytes里包含了报头的长度
    head_json_len=struct.unpack('i',head)[0] #解出报头的长度
    head_json=json.loads(client.recv(head_json_len).decode('utf-8')) #拿到报头
    data_len=head_json['data_size'] #取出报头内包含的信息

    #开始收数据
    recv_size=0
    recv_data=b''
    while recv_size < data_len:
        recv_data+=client.recv(1024)
        recv_size+=len(recv_data)

    print(recv_data.decode('utf-8'))
    #print(recv_data.decode('gbk')) #windows默认gbk编码
```



