## 本节重点：

* 让学生理解为编程语言是什么？为什么要编程？
* 让学生大体明白，编程语言是如何与计算机底层通信的
* 编程语言有哪些分类？
* 分别列举主流编程语言的特点

> **本节时长需控制在25-30分钟内**

## 什么是编程？为什么要编程？\(5分钟\) {#5}

编程 是个动词，编程==写代码，写代码为了什么? 为了让计算机干你想要干的事情，比如，马化腾想跟别人聊天，于是写了个聊天软件，这个软件就是一堆代码的集合，这些代码是什么？这些代码是计算机能理解的语言。

例子：你是公司老板，你有一个员工是中国人，你让他干活，就得说中文，还有一个员工是美国人，让他干活，就得说英文，你还有一条狗，让他听话，你就得汪汪汪。。。，那现在你有台电脑，让它干活，就得用它能理解的语言。

那计算能理解的语言是什么呢？ 之前，我们已经了解到，它只能理解2进制，0101010...，你总不能人肉输一堆二进制给计算机\(虽然最原始的计算机就是这么干的\)让它工作吧，这样开发速度太慢了。所以最好的办法就是人输入简单的指令，计算机能把指令转成二进制进行执行，举例如下:

假如 程序员想让计算机  播放一首 歌曲 ， 只需要输入指令 ，

```
open "老男孩.mp3"
play
```

计算机的CPU接收到这样的指令后，会把它转成一堆 只有cpu可以理解的指令，然后再将指令变成各种对应的如下类似二进制

```
[  op  |  rs |  rt | address/immediate]
   35     3     8           68           decimal
 100011 00011 01000 00000 00001 000100   binary
```

最终cpu 去调用你的硬盘上这首歌，通过音箱播放。

上面cpu那段指令太难理解了，如果让你天天写这样的代码，大家非得自杀不可。还好，伟大的计算机先驱们，开发了各种编程语言，让我们只需要通过写一些简单的规则，就能操作计算机工作啦。

## 有哪些编程语言？\(10分钟\)

编程语言总体分以为机器语言、汇编语言、高级语言，如下

**机器语言**

由于计算机内部只能接受二进制代码，因此，用二进制代码0和1描述的指令称为机器指令，全部机器指令的集合构成计算机的机器语言，用机器语言编程的程序称为目标程序。只有目标程序才能被计算机直接识别和执行。但是机器语言编写的程序无明显特征，难以记忆，不便阅读和书写，且依赖于具体机种，局限性很大，机器语言属于低级语言。

用机器语言编写程序，编程人员要首先熟记所用计算机的全部指令代码和代码的涵义。手编程序时，程序员得自己处理每条指令和每一数据的存储分配和输入输出，还得记住编程过程中每步所使用的工作单元处在何种状态。这是一件十分繁琐的工作。编写程序花费的时间往往是实际运行时间的几十倍或几百倍。而且，编出的程序全是些0和1的指令代码，直观性差，还容易出错。**除了计算机生产厂家的专业人员外，绝大多数的程序员已经不再去学习机器语言了。**

机器语言是微处理器理解和使用的，用于控制它的操作二进制代码。

尽管机器语言好像是很复杂的，然而它是有规律的。

存在着多至100000种机器语言的指令。这意味着不能把这些种类全部列出来。

以下是一些示例：

指令部份的示例

0000 代表 加载（LOAD）

0001 代表 存储（STORE）

...

暂存器部份的示例

0000 代表暂存器 A

0001 代表暂存器 B

...

存储器部份的示例

000000000000 代表地址为 0 的存储器

000000000001 代表地址为 1 的存储器

000000010000 代表地址为 16 的存储器

100000000000 代表地址为 2^11 的存储器

集成示例

0000,0000,000000010000 代表 LOAD A, 16

0000,0001,000000000001 代表 LOAD B, 1

0001,0001,000000010000 代表 STORE B, 16

0001,0001,000000000001 代表 STORE B, 1\[1\]

**汇编语言**

汇编语言的实质和机器语言是相同的，都是直接对硬件操作，只不过指令采用了英文缩写的标识符，更容易识别和记忆。它同样需要编程者将每一步具体的操作用命令的形式写出来。汇编程序的每一句指令只能对应实际操作过程中的一个很细微的动作。例如移动、自增，因此汇编源程序一般比较冗长、复杂、容易出错，而且使用汇编语言编程需要有更多的计算机专业知识，但汇编语言的优点也是显而易见的，用汇编语言所能完成的操作不是一般高级语言所能够实现的，而且源程序经汇编生成的可执行文件不仅比较小，而且执行速度很快。

汇编的hello world，打印一句hello world, 需要写十多行，也是醉了。

```
; hello.asm 
section .data            ; 数据段声明
        msg db "Hello, world!", 0xA     ; 要输出的字符串
        len equ $ - msg                 ; 字串长度
section .text            ; 代码段声明
global _start            ; 指定入口函数
_start:                  ; 在屏幕上显示一个字符串
        mov edx, len     ; 参数三：字符串长度
        mov ecx, msg     ; 参数二：要显示的字符串
        mov ebx, 1       ; 参数一：文件描述符(stdout) 
        mov eax, 4       ; 系统调用号(sys_write) 
        int 0x80         ; 调用内核功能
                         ; 退出程序
        mov ebx, 0       ; 参数一：退出代码
        mov eax, 1       ; 系统调用号(sys_exit) 
        int 0x80         ; 调用内核功能
```

**高级语言**

高级语言是大多数编程者的选择。和汇编语言相比，它不但将许多相关的机器指令合成为单条指令，并且去掉了与具体操作有关但与完成工作无关的细节，例如使用堆栈、寄存器等，这样就大大简化了程序中的指令。同时，由于省略了很多细节，编程者也就不需要有太多的专业知识。

高级语言主要是相对于汇编语言而言，它并不是特指某一种具体的语言，而是包括了很多编程语言，像最简单的编程语言PASCAL语言也属于高级语言。

**高级语言所编制的程序不能直接被计算机识别，必须经过转换才能被执行**，按转换方式可将它们分为两类：

**编译类**：编译是指在应用源程序执行之前，就将程序源代码“翻译”成目标代码（机器语言），因此其目标程序可以脱离其语言环境独立执行\(编译后生成的可执行文件，是cpu可以理解的2进制的机器码组成的\)，使用比较方便、效率较高。但应用程序一旦需要修改，必须先修改源代码，再重新编译生成新的目标文件（\* .obj，也就是OBJ文件）才能执行，只有目标文件而没有源代码，修改很不方便。

> 用翻译官举例子

![](/assets/编译VS解释.png)

**编译后程序运行时不需要重新翻译，直接使用编译的结果就行了。程序执行效率高，依赖编译器，跨平台性差些**。如C、C++、Delphi等

**解释类**：执行方式类似于我们日常生活中的“同声翻译”，应用程序源代码一边由相应语言的解释器“翻译”成目标代码（机器语言），一边执行，因此效率比较低，而且不能生成可独立执行的可执行文件，应用程序不能脱离其解释器\(想运行，必须先装上解释器，就像跟老外说话，必须有翻译在场\)，但这种方式比较灵活，可以动态地调整、修改应用程序。如Python、Java、PHP、Ruby等语言。

#### 总结

**机器语言**

优点是最底层，速度最快，缺点是最复杂，开发效率最低

**汇编语言**

优点是比较底层，速度最快，缺点是复杂，开发效率最低

**高级语言**

编译型语言执行速度快，不依赖语言环境运行，跨平台差

解释型跨平台好，一份代码，到处使用，缺点是执行速度慢，依赖解释器运行

## 主流编程语言介绍\(10分钟\)

世界上的编程语言有600多种，但真正大家主流在使用的最多二三十种，不同的语言有自己的特点和擅长领域，随着计算机的不断发展，新语言在不断诞生，也同时有很多老旧的语言慢慢无人用了。有个权威的语言排名网站，可以看到主流的编程语言是哪些

\*2017年5月数据\([https://www.tiobe.com/tiobe-index/](https://www.tiobe.com/tiobe-index/) \)![](/assets/prgoram_rank.png)

长期语言排名

![](/assets/long_history_program_ranking.png)

下面介绍下几个主流的编程语言：\(5分钟快速介绍\)

**C语言: **

C语言是一种计算机程序设计语言，它既具有高级语言的特点，又具有汇编语言的特点。它由美国贝尔研究所的D.M.Ritchie于1972年推出，1978年后，C语言已先后被移植到大、中、小及微型机上，它可以作为工作系统设计语言，编写系统应用程序，也可以作为应用程序设计语言，编写不依赖计算机硬件的应用程序。它的应用范围广泛，具备很强的数据处理能力，不仅仅是在软件开发上，而且各类科研都需要用到C语言，适于编写系统软件，三维，二维图形和动画，具体应用比如单片机以及嵌入式系统开发。

**C++：**

C++是C语言的继承的扩展，它既可以进行C语言的过程化程序设计，又可以进行以抽象数据类型为特点的基于对象的程序设计，还可以进行以继承和多态为特点的面向对象的程序设计。C++擅长面向对象程序设计的同时，还可以进行基于过程的程序设计，因而C++就适应的问题规模而论，大小由之。

C++不仅拥有计算机高效运行的实用性特征，同时还致力于提高大规模程序的编程质量与程序设计语言的问题描述能力。

**JAVA:**

Java是一种可以撰写跨平台应用软件的面向对象的程序设计语言，是由Sun Microsystems公司于1995年5月推出的Java程序设计语言和Java平台（即JavaSE, JavaEE, JavaME）的总称。Java 技术具有卓越的通用性、高效性、平台移植性和安全性，广泛应用于个人PC、数据中心、游戏控制台、科学超级计算机、移动电话和互联网，同时拥有全球最大的开发者专业社群。在全球云计算和移动互联网的产业环境下，Java更具备了显著优势和广阔前景。

**PHP:**

PHP（外文名:PHP: Hypertext Preprocessor，中文名：“超文本预处理器”）是一种通用开源脚本语言。语法吸收了C语言、Java和Perl的特点，利于学习，使用广泛，主要适用于Web开发领域

**Ruby:**

Ruby 是开源的，在Web 上免费提供，但需要一个许可证。\[4\]

Ruby 是一种通用的、解释的编程语言。

Ruby 是一种真正的面向对象编程语言。

Ruby 是一种类似于 Python 和 Perl 的服务器端脚本语言。

Ruby 可以用来编写通用网关接口（CGI）脚本。

Ruby 可以被嵌入到超文本标记语言（HTML）。

Ruby 语法简单，这使得新的开发人员能够快速轻松地学习 Ruby

**GO:**

Go 是一个开源的编程语言，它能让构造简单、可靠且高效的软件变得容易。

Go是从2007年末由Robert Griesemer, Rob Pike, Ken Thompson主持开发，后来还加入了Ian Lance Taylor, Russ Cox等人，并最终于2009年11月开源，在2012年早些时候发布了Go 1稳定版本。现在Go的开发已经是完全开放的，并且拥有一个活跃的社区。

由其擅长并发编程

**Python:**

Python是一门优秀的综合语言， Python的宗旨是简明、优雅、强大，在人工智能、云计算、金融分析、大数据开发、WEB开发、自动化运维、测试等方向应用广泛，已是全球第4大最流行的语言。
