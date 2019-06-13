上节课我们已经学会用if .. else 来猜年龄的游戏啦，但是只能猜一次就中的机率太小了，如果我想给玩家3次机会呢？就是程序启动后，玩家最多可以试3次，这个怎么弄呢？你总不会想着把代码复制3次吧。。。。

```py
age_of_oldboy = 48
guess = int(input(">>:"))
if guess > age_of_oldboy :
    print("猜的太大了，往小里试试...")
elif guess < age_of_oldboy :
    print("猜的太小了，往大里试试...")
else:
    print("恭喜你，猜对了...")
#第2次
guess = int(input(">>:"))
if guess > age_of_oldboy :
    print("猜的太大了，往小里试试...")
elif guess < age_of_oldboy :
    print("猜的太小了，往大里试试...")
else:
    print("恭喜你，猜对了...")
#第3次
guess = int(input(">>:"))
if guess > age_of_oldboy :
    print("猜的太大了，往小里试试...")
elif guess < age_of_oldboy :
    print("猜的太小了，往大里试试...")
else:
    print("恭喜你，猜对了...")
```

即使是小白的你，也觉得的太low了是不是，以后要修改功能还得修改3次，因此记住，写重复的代码是程序员最不耻的行为。

那么如何做到不用写重复代码又能让程序重复一段代码多次呢？ 循环语句就派上用场啦

#### **语法**

```
while  条件:
    执行代码...
```

简单吧,`while`就是当的意思，当山峰没有棱角的时候，当河水。。。，sorry ,`while`指 当其后面的条件 成立 ，就执行`while`下面的代码

写个让程序从0打印到100的程序 ，每循环一次，+1

```py
count = 0 
while count <= 100 : #只要count<=100就不断执行下面的代码
   print("loop ", count )
   count +=1  #每执行一次，就把count+1，要不然就变成死循环啦，因为count一直是0
```

输出

```
loop  0
loop  1
loop  2
loop  3
....
loop  98
loop  99
loop  100
```



如果我想实现打印1到100的偶数怎么办呢？

那就得先搞清，怎么判断一个数字是偶数，能被2整除的就是偶数对不对, 怎么判断能否被2整除？简单，除完2没有余数就是啦。记得我们学的取模算运算符么？

```
>>> 10%2
0
>>> 8%2  #无余数，是偶数
0
>>> 7%2  #有余数，是奇数
1
```

放到我们的循环程序里

```py
count = 0
while count <= 100 : #只要count<=100就不断执行下面的代码
    if count % 2 == 0: #是偶数
        print("loop ", count)
    count +=1 #每执行一次，就把count+1，要不然就变成死循环啦，因为count一直是0
```

输出

```
loop  0
loop  2
loop  4
loop  6
....
loop  96
loop  98
loop  100
```

#### 

#### **死循环**

**有一种循环叫死循环，一经触发，就运行个天荒地老、海枯石烂。**

while 是只要后边条件成立\(也就是条件结果为真\)就一直执行，怎么让条件一直成立呢？

```py
count = 0
while True: #True本身就是真呀
    print("你是风儿我是沙,缠缠绵绵到天涯...",count)
    count +=1
```



## 循环中止语句

如果在循环的过程中，因为某些原因，你不想继续循环了，怎么把它中止掉呢？这就用到break 或 continue 语句

* break用于完全结束一个循环，跳出循环体执行循环后面的语句

* continue和break有点类似，区别在于continue只是终止本次循环，接着还执行后面的循环，break则完全终止循环 

**例子:break**

```py
count = 0
while count <= 100 : #只要count<=100就不断执行下面的代码
    print("loop ", count)
    if count == 5:
        break
    count +=1 #每执行一次，就把count+1，要不然就变成死循环啦，因为count一直是0
print("-----out of while loop ------")
```

输出

```py
loop  0
loop  1
loop  2
loop  3
loop  4
loop  5
-----out of while loop ------

```

**例子：continue**

```py
count = 0
while count <= 100 : 
    count += 1
    if count > 5 and count < 95: #只要count在6-94之间，就不走下面的print语句，直接进入下一次loop
        continue 
    print("loop ", count)
print("-----out of while loop ------")
```

输出

```py
loop  1
loop  2
loop  3
loop  4
loop  5
loop  95
loop  96
loop  97
loop  98
loop  99
loop  100
loop  101
-----out of while loop ------
```

## while … else ..

与其它语言else 一般只与if 搭配不同，在Python 中还有个while …else 语句

while 后面的else 作用是指，**当while 循环正常执行完，中间没有被break 中止的话，就会执行else后面的语句**

```py
count = 0
while count <= 5 :
    count += 1
    print("Loop",count)
else:
    print("循环正常执行完啦")
print("-----out of while loop ------")
```

输出

```
Loop 1
Loop 2
Loop 3
Loop 4
Loop 5
Loop 6
循环正常执行完啦
-----out of while loop ------

```

如果执行过程中被break啦，就不会执行else的语句啦

```py
count = 0
while count <= 5 :
    count += 1
    if count == 3:break
    print("Loop",count)
else:
    print("循环正常执行完啦")
print("-----out of while loop ------")

```

输出

```
Loop 1
Loop 2
-----out of while loop ------

```



## 小节练习

**练习1：猜年龄游戏 \(10分钟\)**

要求：

1. 允许用户最多尝试3次，3次都没猜对的话，就直接退出，如果猜对了，打印恭喜信息并退出



**练习2：猜年龄游戏升级版 \(20分钟\)**

要求：

1. 允许用户最多尝试3次
2. 每尝试3次后，如果还没猜对，就问用户是否还想继续玩，如果回答Y或y, 就继续让其猜3次，以此往复，如果回答N或n，就退出程序
3. 如果猜对了，就直接退出



