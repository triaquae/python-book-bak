## 本节重点

* 了解IO模型
* 掌握network IO的两个阶段

> **本节时长需控制在15分钟内**

### IO模型介绍

[为了更好地了解IO模型，我们需要事先回顾下：同步、异步、阻塞、非阻塞](http://www.cnblogs.com/linhaifeng/articles/7430066.html#_label4)

同步（synchronous） IO和异步（asynchronous） IO，阻塞（blocking） IO和非阻塞（non-blocking）IO分别是什么，到底有什么区别？这个问题其实不同的人给出的答案都可能不同，比如wiki，就认为asynchronous IO和non-blocking IO是一个东西。这其实是因为不同的人的知识背景不同，并且在讨论这个问题的时候上下文\(context\)也不相同。所以，为了更好的回答这个问题，我先限定一下本文的上下文。

```
本文讨论的背景是Linux环境下的network IO。本文最重要的参考文献是Richard Stevens的“UNIX® Network Programming Volume 1, Third Edition: The Sockets Networking ”，6.2节“I/O Models ”，Stevens在这节中详细说明了各种IO的特点和区别，如果英文够好的话，推荐直接阅读。Stevens的文风是有名的深入浅出，所以不用担心看不懂。本文中的流程图也是截取自参考文献。

Stevens在文章中一共比较了五种IO Model：  
* blocking IO  
* nonblocking IO  
* IO multiplexing  
* signal driven IO  
* asynchronous IO  
由signal driven IO（信号驱动IO）在实际中并不常用，所以主要介绍其余四种IO Model。
```

再说一下IO发生时涉及的对象和步骤。对于一个network IO \\(这里我们以read举例\\)，它会涉及到两个系统对象，一个是调用这个IO的process \\(or thread\\)，另一个就是系统内核\\(kernel\\)。当一个read操作发生时，该操作会经历两个阶段：

```
1）等待数据准备 (Waiting for the data to be ready)
2）将数据从内核拷贝到进程中(Copying the data from the kernel to the process)
```

记住这两点很重要，因为这些IO模型的区别就是在两个阶段上各有不同的情况。

