### 练习题

#### 文件处理相关

1. 编码问题
  - 请说明python2 与python3中的默认编码是什么？

      ```python
      # 答案
      py2默认ASCII码，py3默认的utf8
      ```

  - 为什么会出现中文乱码？你能列举出现乱码的情况有哪几种？

    ```python
    # 答案
    #coding:utf-8 #.py文件是什么编码就需要告诉python用什么编码去读取这个.py文件。
    sys.stdout.encoding，默认就是locale的编码，print会用sys.stdout.encoding去encode()成字节流，交给terminal显示。所以locale需要与terminal一致，才能正确print打印出中文。
    sys.setdefaultencoding(‘utf8’)，用于指定str.encode() str.decode()的默认编码，默认是ascii。
    以下几种(local 为软件运行时的语言环境):
      终端为UTF-8，locale为zh_CN.GBK
      终端为UTF-8，locale为zh_CN.UTF-8
      终端为GBK，locale为zh_CN.GBK
      终端为GBK，locale为zh_CN.UTF-8
    ```

- 如何进行编码转换？

    ```python
    # 答案
    字符串在python内部中是采用unicode的编码方式，所以其他语言先decode转换成unicode编码，再encode转换成utf8编码。
    ```

- `#-*-coding:utf-8-*-` 的作用是什么？

    ```
    # 答案
    编码声明
    ```

5. 解释py2 bytes vs py3 bytes的区别

    ```python
    # 答案
      Python 2 将 strings 处理为原生的 bytes 类型，而不是 unicode(python2 str == bytes)，

      Python 3 所有的 strings 均是 unicode 类型(python3 中需要通过 unicode )
      string -> encode  -> bytes

      bytes -> decode  -> string
    ```

2. 文件处理
  1. r和rb的区别是什么？

    ```python
    # 答案
      r 读模式
      rb 二进制读
    ```

  2. 解释一下以下三个参数的分别作用

    ```python
    # 答案
    open(f_name,'r',encoding="utf-8")
    ```

    ```python
     f_name   文件名
       r      模式
    encoding  编码方式
    ```

#### 函数基础：

1. 写函数，计算传入数字参数的和。（动态传参）

  ```python
  # 答案
  def func_sum(x, y):
      return x + y

      或
      lambda x , y : x +y
  ```

2. 写函数，用户传入修改的文件名，与要修改的内容，执行函数，完成整个文件的批量修改操作

  ```python
  # 答案
   # 修改列表中字符串首字母大写

   def file_daxie(file):
      a=[]
      for i in file:
          b=i.capitalize()
          a.append(b)
   print(a)

  ```

3. 写函数，检查用户传入的对象（字符串、列表、元组）的每一个元素是否含有空内容。

  ```python
  # 答案
  def file_k(file):
      n=0
      for i in file:
          if i==‘ ‘:
              n+=1
      print(‘有%s个空‘%n)
  ```

4. 写函数，检查传入字典的每一个value的长度,如果大于2，那么仅保留前两个长度的内容，并将新内容返回给调用者。

  ```python
  dic = {"k1": "v1v1", "k2": [11,22,33,44]}
  PS:字典中的value只能是字符串或列表
  ```   

  ```python
      #答案
        def func(i):  # i为所传字典
        
            for k, v in i.items():
                if len(v) > 2:
                    dic[k]= v[:2]
                else:
                    continue
            return i
        
        print(func(dic))
        
        {'k1': 'v1', 'k2': [11, 22]}
  ```

5. 解释闭包的概念

  ```python
  # 答案
     闭包(closure)是函数式编程的重要的语法结构。函数式编程是一种编程范式 (而面向过程编程和面向对象编程也都是编程范式)。
     在面向过程编程中，我们见到过函数(function)；在面向对象编程中，我们见过对象(object)。函数和对象的根本目的是以某种逻辑方式组织代码，并提高代码的可重复使用性(reusability)。
     闭包也是一种组织代码的结构，它同样提高了代码的可重复使用性。
  ```


#### 函数进阶：

1. 写函数，返回一个扑克牌列表，里面有52项，每一项是一个元组  
  1. 例如：\[\(‘红心’，2\),\(‘草花’，2\), …\(‘黑桃A’\)\]

  ```python
  # 答案
    def cards():
        num = []
        for i in range(2,11):
            num.append(i)
        num.extend(['J','Q','K','A'])
        type = ['红心','草花','方块','黑桃']
        result = []
        for i in num:
            for j in type:
                result.append((j,i))
        return result
    print(cards())
  ```

  2. 写函数，传入n个数，返回字典{‘max’:最大值,’min’:最小值}

  ```python
  例如:min_max(2,5,7,8,4)
  返回:{‘max’:8,’min’:2}
  ```
  ```python
  # 答案
    def max_min(*args):
        the_max = args[0]
        the_min = args[0]
        for i in args:
            if i > the_max:
                the_max = i
            if i < the_min:
                the_min = i
        return {'max': the_max, 'min': the_min}
    
    print(max_min(2, 4, 6, 48, -16, 999, 486, ))
  ```



3. 写函数，专门计算图形的面积

* 其中嵌套函数，计算圆的面积，正方形的面积和长方形的面积
* 调用函数area\(‘圆形’,圆半径\) 返回圆的面积
* 调用函数area\(‘正方形’,边长\) 返回正方形的面积
* 调用函数area\(‘长方形’,长，宽\) 返回长方形的面积

```python
def area():
def 计算长方形面积():
    pass

def 计算正方形面积():
    pass

def 计算圆形面积():
    pass
```

  ```python
  # 答案
  import math
  print('''
  请按照如下格式输出：
      调用函数area(‘圆形’,圆半径) 返回圆的面积
      调用函数area(‘正方形’,边长) 返回正方形的面积
      调用函数area(‘长方形’,长，宽) 返回长方形的面积''')
  def area(name,*args):
      def areas_rectangle(x,y):
          return ("长方形的面积为：",x*y)

      def area_square(x):
          return ("正方形的面积为：",x**2)

      def area_round(r):
          return ("圆形的面积为：",math.pi*r*r)
      if name =='圆形':
          return area_round(*args)
      elif name =='正方形':
          return area_square(*args)
      elif name =='长方形':
          return areas_rectangle(*args)


  print(area('长方形', 3, 4))
  print(area('圆形', 3))
  print(area('正方形', 3))
  ```

4. 写函数，传入一个参数n，返回n的阶乘

  ```python
  例如:cal(7)
  计算7*6*5*4*3*2*1
  ```

  ```python
  # 答案
  def cal(n):
      res= 1
      for i in range(n,0,-1):
          # print(i)
          res = res*i
          print(res)
      return res

  print(cal(7))
  ```

5. 编写装饰器，为多个函数加上认证的功能（用户的账号密码来源于文件），要求登录成功一次，后续的函数都无需再输入用户名和密码

```python
# 答案
def login(func):
    def wrapper(*args,**kwargs):
        username = input("account:").strip()
        password = input("password:").strip()
        with open('userinfo.txt','r',encoding='utf-8') as f:
            userinfo = f.read().strip(',')
            userinfo = eval(userinfo)
            print(userinfo)
            if username in userinfo['name'] and password in userinfo['password']:
                print("success")
            else:
                print("pass")

    return wrapper

@login
def name():
    print("hello")

name()
```

#### 生成器和迭代器

1. 生成器和迭代器的区别？

  ```python
  # 答案
   对于list、string、tuple、dict等这些容器对象,使用for循环遍历是很方便的。
  在后台for语句对容器对象调用iter()函数。iter()是python内置函数。
  iter()函数会返回一个定义了 next()方法的迭代器对象，它在容器中逐个访问容器内的
  元素。next()也是python内置函数。在没有后续元素时，next()会抛出
  一个StopIteration异常，通知for语句循环结束。
  迭代器是用来帮助我们记录每次迭代访问到的位置，当我们对迭代器使用next()函数的
  时候，迭代器会向我们返回它所记录位置的下一个位置的数据。实际上，在使用next()函数
  的时候，调用的就是迭代器对象的_next_方法（Python3中是对象的_next_方法，
  Python2中是对象的next()方法）。所以，我们要想构造一个迭代器，
  就要实现它的_next_方法。但这还不够，python要求迭代器本身也是可迭代的，
  所以我们还要为迭代器实现_iter_方法，而_iter_方法要返回一个迭代器，
  迭代器自身正是一个迭代器，所以迭代器的_iter_方法返回自身self即可。
  ```

2. 生成器有几种方式获取value？

  ```python
  # 答案
  两种方式获取：
      for  循环
      next 获取
  ```

3. 通过生成器写一个日志调用方法， 支持以下功能

* 根据指令向屏幕输出日志
* 根据指令向文件输出日志
* 根据指令同时向文件&屏幕输出日志
* 以上日志格式如下

```
2017-10-19 22:07:38 [1] test log db backup 3
2017-10-19 22:07:40 [2] user alex login success
#注意：其中[1],[2]是指自日志方法第几次调用，每调用一次输出一条日志
```

* 代码结构如下

```python
def logger(filename,channel='file'):
"""
日志方法
:param filename: log filename
:param channel: 输出的目的地，屏幕(terminal)，文件(file)，屏幕+文件(both)
:return:
"""
...your code...

#调用
log_obj = logger(filename="web.log",channel='both')
log_obj.__next__()
log_obj.send('user alex login success')
```

#### 内置函数

1. 用map来处理字符串列表,把列表中所有人都变成sb,比方alex\_sb

  ```python
  name=['alex','wupeiqi','yuanhao','nezha']
  ```

  ```python
  map()函数
  map()是 Python 内置的高阶函数，它接收一个函数 f 和一个 list，并通过把
  函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。

  　　注意：map()函数在不改变原有的lisy，而是返回一个新的list
   代码:
   name=['alex','wupeiqi','yuanhao','nezha']

  def sb(x):
      return x+'_sb'

  res = map(sb,name)
  print(list(res))
  ```

2. 用filter函数处理数字列表，将列表中所有的偶数筛选出来

  ```python
  num = [1,3,5,6,7,8]
  ```

  ```python
  num = [1,3,5,6,7,8]
  def func(x):
      if x%2 == 0:
          return True

  ret = filter(func,num)
  print(list(ret))
  ```

3. 如下，每个小字典的name对应股票名字，shares对应多少股，price对应股票的价格

  ```python
  portfolio = [
  {'name': 'IBM', 'shares': 100, 'price': 91.1},
  {'name': 'AAPL', 'shares': 50, 'price': 543.22},
  {'name': 'FB', 'shares': 200, 'price': 21.09},
  {'name': 'HPQ', 'shares': 35, 'price': 31.75},
  {'name': 'YHOO', 'shares': 45, 'price': 16.35},
  {'name': 'ACME', 'shares': 75, 'price': 115.65}
  ]
  ```

计算购买每支股票的总价

用filter过滤出，单价大于100的股票有哪些

  ```python
  f = filter(lambda d:d['price']>=100,portfolio)
  print(list(f))
  ```

1、请分别介绍文件操作中不同的打开方式之间的区别：

| 模式 | 含义 |
| :-- | :-- | :-- |
| r | 文本只读模式 |  
| rb | 二进制模式 这种方法是用来传输或存储，不给人看的 |  
| r+ | 读写模式，只要有r，那么文件必须存在 |  
| rb+ | 二进制读写模式 |  
| w | 只写模式，不能读，用w模式打开一个已经存在的文件，如果有内容会清空，重新写 |  
| wb | 以二进制方式打开，只能写文件，如果不存在，则创建 |  
| w+ | <span class="Apple-tab-span" style="white-space:pre"></span>读写模式，先读后写，只要有w，会清空原来的文件内容 |  
| wb+ | 二进制写读模式 |  
| a | <span class="Apple-tab-span" style="white-space:pre"></span>追加模式，也能写，在文件的末尾添加内容 |  
| ab | 二进制追加模式 |  
| a+ | 追加模式，如果文件不存在，则创建文件，如果存在，则在末尾追加 |  
| ab+ |  追读写二进制模式，从文件顶部读取文件，从文件底部添加内容，不存在则创建|  

2、有列表 li = ['alex', 'egon', 'smith', 'pizza', 'alen'], 请将以字母“a”开头的元素的首字母改为大写字母；

```python
# 答案
li = ['alex', 'egon', 'smith', 'pizza', 'alen']
li_new = []
for i in li:
    if i.startswith('a'):
        li_new.append(i.capitalize())
    else:
        li_new.append(i)
print(li_new)

for i in range(len(li)):
    if li[i][0] == 'a':
        li[i] = li[i].capitalize()
    else:
        continue
print(li)
```

3、有如下程序, 请给出两次调用`show_num`函数的执行结果，并说明为什么：

  ```python
  num = 20
  def show_num(x=num):
    print(x)
  show_num()
  num = 30
  show_num()
  ```

  ```python
  # 答案
  如果函数收到的是一个不可变对象（比如数字、字符或者元组）的引用，就不能直接修改原始对象，相当于通过“传值’来传递对象，此时如果想改变这些变量的值，可以将这些变量申明为全局变量。
  ```

4、有列表 li = ['alex', 'egon', 'smith', 'pizza', 'alen'], 请以列表中每个元素的第二个字母倒序排序；

  ```python
  # 答案
  print(sorted(li, key=lambda x: x[1], reverse=True))
  ```

5、有名为`poetry.txt`的文件，其内容如下，请删除第三行；

  ```
  昔人已乘黄鹤去，此地空余黄鹤楼。
  黄鹤一去不复返，白云千载空悠悠。
  晴川历历汉阳树，芳草萋萋鹦鹉洲。
  日暮乡关何处是？烟波江上使人愁。
  ```

  ```python
  # 答案
  方法一：
  import os
  p = 'poetry.txt'
  file = open(p,'r',encoding='utf-8')
  print(file)
  pnew = '%s.new'%p
  filenew = open(pnew,'w',encoding='utf-8')
  str1 = '晴川历历汉阳树，芳草萋萋鹦鹉洲。'
  for i in file:
      if str1 in i:
          i = ''
          filenew.write(i)
      else:
          filenew.write(i)
  file.close()
  filenew.close()
  os.replace(pnew,p)

  方法二：逐行读取文件
  import os
  f1=open('poetry.txt', 'r',encoding='utf-8')

  str='晴川历历汉阳树，芳草萋萋鹦鹉洲。'
  with open('poetry1.txt', 'w', encoding='utf-8') as f2:
      ff1='poetry.txt'
      ff2='poetry1.txt'
      for line in f1:
          if str in line:
              line=''
              f2.write(line)

          else:
              f2.write(line)
  f1.close()
  f2.close()
  os.replace(ff2,ff1)
  ```

6、有名为`username.txt`的文件，其内容格式如下，写一个程序，判断该文件中是否存在"alex", 如果没有，则将字符串"alex"添加到该文件末尾，否则提示用户该用户已存在；

  ```
  pizza
  alex
  egon
  ```

  ```python
  # 答案
  with open('username.txt','r+',encoding='utf-8') as f:
    str1 = 'alexx'
    i = f.read()
    print(i)
    if str1 in i:
        print("the user already exist in")
    else:
        f.write('\nalexx')
  ```

7、有名为user_info.txt的文件，其内容格式如下，写一个程序，删除id为100003的行；

  ```
  pizza,100001
  alex, 100002
  egon, 100003
  ```

  ```python
  # 答案
  import os
  a = 'user_info.txt'
  b = 'user_info1.txt'
  with open(a,'r',encoding='utf-8') as f:
      with open(b, 'w', encoding='utf-8') as f2:
          for i in f:
              if '100003' in i:
                  pass
              else:
                  f2.write(i)
  os.replace(b,a)
  ```

8、有名为user_info.txt的文件，其内容格式如下，写一个程序，将id为100002的用户名修改为`alex li`；

  ```
  pizza,100001
  alex, 100002
  egon, 100003
  ```

  ```python
  # 答案
  file = 'user_info.txt'
  old_str = '100002'
  new_str = 'alex, 100002'
  file_data=''
  with open(file,'r',encoding='utf-8') as f1:

      for line in f1:
          if old_str in line:
              line =new_str
          file_data +=line

          with open(file,'w',encoding='utf-8') as f1:
              f1.write(file_data)

  ```

9、写一个计算每个程序执行时间的装饰器；

  ```python
  # 答案
  import time
  def timer(func):
      def wrapper(*args,**kwargs):
          start_time = time.time()
          func(*args)
          stop_time = time.time()
          print(stop_time-start_time)
      return wrapper

  @timer
  def sayhi():
      print("hello word")

  sayhi()
  ```

10、lambda是什么？请说说你曾在什么场景下使用lambda？

```python
# 答案
lambda函数就是可以接受任意多个参数(包括可选参数)并且返回单个表达式值得函数
    好处：
        1.lambda函数比较轻便，即用即扔，适合完成只在一处使用的简单功能
        2.匿名函数，一般用来给filter，map这样的函数式编程服务
        3.作为回调函数，传递给某些应用，比如消息处理
```

11、题目：写一个摇骰子游戏，要求用户压大小，赔率一赔一。

要求：三个骰子，摇大小，每次打印摇骰子数。

```python
import random

def roll_dice(numbers=3, points=None):
    """
     定义骰子，循环三次
    :param numbers:
    :param points:
    :return:
    """

    print('----- 摇骰子 -----')
    if points is None:
        points = []
    while numbers > 0:
        point = random.randrange(1, 7)
        points.append(point)
        numbers -= 1
    return points

def roll_result(total):
    """
    定义大小，三个大或者一个小两个大。三个小或者两个小一个大
    :param total:
    :return:
    """

    is_big = 11 <= total <= 18
    is_small = 3 <= total <= 10
    if is_big:
        return "big"
    elif is_small:
        return "small"

def start_game():
    your_money = 1000
    while your_money > 0:
        print('----- 游戏开始 -----')
        choices = ["大", "小"]
        your_choice = input("请下注， 大 or 小")
        your_bet = input("下注金额：")
        if your_choice in choices:
            points = roll_dice()
            total = sum(points)
            you_win = your_choice == roll_result(total)
            if you_win:
                your_money = your_money + int(your_bet)
                print("骰子点数", points)
                print("恭喜， 你赢了%s元， 你现在的本金%s 元" % (your_bet, your_money + int(your_bet)))
            else:
                your_money = your_money - int(your_bet)
                print("骰子点数", points)
                print("很遗憾， 你输了%s元， 你现在的本金%s 元" % (your_bet, your_money - int(your_bet)))
        else:
            print('格式有误，请重新输入')
    else:
        print("game over")

start_game()

```

