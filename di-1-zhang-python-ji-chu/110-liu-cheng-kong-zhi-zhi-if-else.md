## 本节重点：

* 使学生理解和掌握基本流程控制if ... else 
* 掌握缩进的重要性
* 使学生掌握多条件语句if ..elif ...

> **本节时长需控制在30分钟之内**

## 流程控制

假如把写程序比做走路，那我们到现在为止，一直走的都是直路，还没遇到过分叉口，想象现实中，你遇到了分叉口，然后你决定往哪拐必然是有所动机的。你要判断那条岔路是你真正要走的路，如果我们想让程序也能处理这样的判断怎么办？ 很简单，只需要在程序里预设一些条件判断语句，满足哪个条件，就走哪条岔路。这个过程就叫流程控制。

#### if...else  语句

**单分支 \(3-5分钟\)**

```py
if 条件:
    满足条件后要执行的代码
```

![](/assets/if_else.png)

**双分支\(3分钟\)**

```
if 条件:
    满足条件执行代码
else:
    if条件不满足就走这段
```

```py
AgeOfOldboy = 48

if AgeOfOldboy > 50 :
    print("Too old, time to retire..")
else:
    print("还能折腾几年!")
```

**缩进\(5分钟\)**

> 这里必须要插入这个缩进的知识点

你会发现，上面的if代码里，每个条件的下一行都缩进了4个空格，这是为什么呢？这就是Python的一大特色，强制缩进，目的是为了让程序知道，每段代码依赖哪个条件，如果不通过缩进来区分，程序怎么会知道，当你的条件成立后，去执行哪些代码呢？

在其它的语言里，大多通过`{}`来确定代码块，比如C,C++,Java,Javascript都是这样，看一个JavaScript代码的例子

```js
var age = 56
if ( age < 50){
  console.log("还能折腾")
    console.log('可以执行多行代码')
}else{
   console.log('太老了')
}
```

在有`{}`来区分代码块的情况下，缩进的作用就只剩下让代码变的整洁了。

Python是门超级简洁的语言，发明者定是觉得用`{}`太丑了，所以索性直接不用它，那怎么能区分代码块呢？答案就是强制缩进。

Python的缩进有以下几个原则:

* 顶级代码必须顶行写，即如果一行代码本身不依赖于任何条件，那它必须不能进行任何缩进
* 同一级别的代码，缩进必须一致
* 官方建议缩进用4个空格，当然你也可以用2个，如果你想被人笑话的话。

**多分支\(15-20分钟\)**

回到流程控制上来，if...else ...可以有多个分支条件

```py
if 条件:
    满足条件执行代码
elif 条件:
    上面的条件不满足就走这个
elif 条件:
    上面的条件不满足就走这个
elif 条件:
    上面的条件不满足就走这个    
else:
    上面所有的条件不满足就走这段
```

写个猜年龄的游戏吧

```py
age_of_oldboy = 48

guess = int(input(">>:"))

if guess > age_of_oldboy :
    print("猜的太大了，往小里试试...")

elif guess < age_of_oldboy :
    print("猜的太小了，往大里试试...")

else:
    print("恭喜你，猜对了...")
```

上面的例子，根据你输入的值不同，会最多得到3种不同的结果

> 此时让学生自己也默写一遍这段代码

再来个匹配成绩的小程序吧，成绩有ABCDE5个等级，与分数的对应关系如下

```
A    90-100
B    80-89
C    60-79
D    40-59
E    0-39
```

要求用户输入0-100的数字后，你能正确打印他的对应成绩

```
score = int(input("输入分数:"))

if score > 100:
    print("我擦，最高分才100...")
elif score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 60:
    print("C")
elif score >= 40:
    print("D")
else:
    print("太笨了...E")
```

这里有个问题，就是当我输入95的时候 ，它打印的结果是A,但是95 明明也大于第二个条件`elif score >=80:`呀, 为什么不打印B呢？这是因为代码是从上到下依次判断，只要满足一个，就不会再往下走啦，这一点一定要清楚呀！

> 你有没有发现一个问题，我上在的程序都只能执行一次，猜年龄只能一次好无聊呀，能不能多让我试几次呢，说不定就猜中了呢，毕竟老男孩老师的年龄很快就成为常量啦。。。哈哈哈， 必然可以，继续往下学吧！加油！


