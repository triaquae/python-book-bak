## 本章总节

### 练习题

#### 文件处理相关

1. 编码问题  
   1. 请说明python2 与python3中的默认编码是什么？  
   2. 为什么会出现中文乱码？你能列举出现乱码的情况有哪几种？  
   3. 如何进行编码转换？  
   4. `#-*-coding:utf-8-*-` 的作用是什么？

   5. 解释py2 bytes vs py3 bytes的区别

2. 文件处理  
   1. r和rb的区别是什么？  
   2. 解释一下以下三个参数的分别作用

   ```python
    open(f_name,'r',encoding="utf-8")
   ```

#### 函数基础：

1. 写函数，计算传入数字参数的和。（动态传参）
2. 写函数，用户传入修改的文件名，与要修改的内容，执行函数，完成整个文件的批量修改操作
3. 写函数，检查用户传入的对象（字符串、列表、元组）的每一个元素是否含有空内容。
4. 写函数，检查传入字典的每一个value的长度,如果大于2，那么仅保留前两个长度的内容，并将新内容返回给调用者。

   ```
   dic = {"k1": "v1v1", "k2": [11,22,33,44]}
   PS:字典中的value只能是字符串或列表
   ```

5. 解释闭包的概念

#### 函数进阶：

1. 写函数，返回一个扑克牌列表，里面有52项，每一项是一个元组
   1. 例如：\[\(‘红心’，2\),\(‘草花’，2\), …\(‘黑桃A’\)\]
2. 写函数，传入n个数，返回字典{‘max’:最大值,’min’:最小值}

   ```python
   例如:min_max(2,5,7,8,4)
   返回:{‘max’:8,’min’:2}
   ```

3. 写函数，专门计算图形的面积

   * 其中嵌套函数，计算圆的面积，正方形的面积和长方形的面积
   * 调用函数area\(‘圆形’,圆半径\)  返回圆的面积
   * 调用函数area\(‘正方形’,边长\)  返回正方形的面积
   * 调用函数area\(‘长方形’,长，宽\)  返回长方形的面积

   ```python
   def area():
       def 计算长方形面积():
           pass

       def 计算正方形面积():
           pass

       def 计算圆形面积():
           pass
   ```

4. 写函数，传入一个参数n，返回n的阶乘

   ```python
   例如:cal(7)
   计算7*6*5*4*3*2*1
   ```

5. 编写装饰器，为多个函数加上认证的功能（用户的账号密码来源于文件），要求登录成功一次，后续的函数都无需再输入用户名和密码

#### 生成器和迭代器

1. 生成器和迭代器的区别？
2. 生成器有几种方式获取value？
3. 通过生成器写一个日志调用方法， 支持以下功能

   * 根据指令向屏幕输出日志
   * 根据指令向文件输出日志
   * 根据指令同时向文件&屏幕输出日志
   * 以上日志格式如下

     ```
     2017-10-19 22:07:38 [1] test log db backup 3
     2017-10-19 22:07:40 [2]    user alex login success 
     #注意：其中[1],[2]是指自日志方法第几次调用，每调用一次输出一条日志
     ```

   * 代码结构如下

     ```
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

2. 用filter函数处理数字列表，将列表中所有的偶数筛选出来

   ```python
   num = [1,3,5,6,7,8]
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
   
1、请分别介绍文件操作中不同的打开方式之间的区别：

| 模式   | 含义   |
| ---- | ---- |
| r    |      |
| rb   |      |
| r+   |      |
| rb+  |      |
| w    |      |
| wb   |      |
| w+   |      |
| wb+  |      |
| a    |      |
| ab   |      |
| a+   |      |
| ab+  |      |

2、有列表 li = ['alex', 'egon', 'smith', 'pizza', 'alen'], 请将以字母“a”开头的元素的首字母改为大写字母；

3、有如下程序, 请给出两次调用`show_num`函数的执行结果，并说明为什么：

   ```
   num = 20
   
   def show_num(x=num):
       print(x)
      
   show_num()
   
   num = 30
   
   show_num()
   ```

4、有列表 li = ['alex', 'egon', 'smith', 'pizza', 'alen'], 请以列表中每个元素的第二个字母倒序排序；

5、有名为`poetry.txt`的文件，其内容如下，请删除第三行；
   
   ```
   昔人已乘黄鹤去，此地空余黄鹤楼。
   
   黄鹤一去不复返，白云千载空悠悠。
   
   晴川历历汉阳树，芳草萋萋鹦鹉洲。
   
   日暮乡关何处是？烟波江上使人愁。
   ```
   
6、有名为`username.txt`的文件，其内容格式如下，写一个程序，判断该文件中是否存在"alex", 如果没有，则将字符串"alex"添加到该文件末尾，否则提示用户该用户已存在；
   
   ```
   pizza
   alex
   egon
   ```

7、有名为user_info.txt的文件，其内容格式如下，写一个程序，删除id为100003的行；

   ```
   pizza,100001
   alex, 100002
   egon, 100003
   ```

8、有名为user_info.txt的文件，其内容格式如下，写一个程序，将id为100002的用户名修改为`alex li`；

   ```
   pizza,100001
   alex, 100002
   egon, 100003
   ```

9、写一个计算每个程序执行时间的装饰器；

10、lambda是什么？请说说你曾在什么场景下使用lambda？

11、题目：写一个摇骰子游戏，要求用户压大小，赔率一赔一。

要求：三个骰子，摇大小，每次打印摇骰子数。



### 作业

现要求你写一个简单的员工信息增删改查程序，需求如下：

![](/assets/chapter3/staff_table.png)

当然此表你在文件存储时可以这样表示

```
1,Alex Li,22,13651054608,IT,2013-04-01
2,Jack Wang,28,13451024608,HR,2015-01-07
3,Rain Wang,21,13451054608,IT,2017-04-01
4,Mack Qiao,44,15653354208,Sales,2016-02-01
5,Rachel Chen,23,13351024606,IT,2013-03-16
6,Eric Liu,19,18531054602,Marketing,2012-12-01
7,Chao Zhang,21,13235324334,Administration,2011-08-08
8,Kevin Chen,22,13151054603,Sales,2013-04-01
9,Shit Wen,20,13351024602,IT,2017-07-03
10,Shanshan Du,26,13698424612,Operation,2017-07-02
```

1.可进行模糊查询，语法至少支持下面3种查询语法:

```py
find name,age from staff_table where age > 22

find * from staff_table where dept = "IT"

find * from staff_table where enroll_date like "2013"
```

2.可创建新员工纪录，以phone做唯一键\(即不允许表里有手机号重复的情况\)，staff\_id需自增

```py
语法: add staff_table Alex Li,25,134435344,IT,2015-10-29
```

3.可删除指定员工信息纪录，输入员工id，即可删除

```py
语法: del from staff_table where  id=3
```

4.可修改员工信息，语法如下:

```py
UPDATE staff_table SET dept="Market" WHERE  dept = "IT" 把所有dept=IT的纪录的dept改成Market
UPDATE staff_table SET age=25 WHERE  name = "Alex Li"  把name=Alex Li的纪录的年龄改成25
```

5.以上每条语名执行完毕后，要显示这条语句影响了多少条纪录。 比如查询语句 就显示 查询出了多少条、修改语句就显示修改了多少条等。

** 注意：以上需求，要充分使用函数，请尽你的最大限度来减少重复代码！**

