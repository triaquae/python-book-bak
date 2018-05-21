## 练习答案

1、请用代码实现：利用下划线将列表的每一个元素拼接成字符串，li＝\['alex', 'eric', 'rain'\]

```
  该题目主要是考的字符串的拼接,join方法,
      s = ""
      li = ['alex', 'eric', 'rain']
      s = "_".join(li)
```

2、查找列表中元素，移除每个元素的空格，并查找以a或A开头并且以c结尾的所有元素。

li = \["alec", " aric", "Alex", "Tony", "rain"\]

tu = \("alec", " aric", "Alex", "Tony", "rain"\)

dic = {'k1': "alex", 'k2': ' aric', "k3": "Alex", "k4": "Tony"}

```
  li = ["alec", " aric", "Alex", "Tony", "rain"]

  for i in li:
      i = i.strip()
      if i.startswith("a") or i.startswith("A")  and i.endswith("c"):
          print(i)
```

3、写代码，有如下列表，按照要求实现每一个功能

li=\['alex', 'eric', 'rain'\]

* 计算列表长度并输出
* 列表中追加元素“seven”，并输出添加后的列表
* 请在列表的第1个位置插入元素“Tony”，并输出添加后的列表
* 请修改列表第2个位置的元素为“Kelly”，并输出修改后的列表
* 请删除列表中的元素“eric”，并输出修改后的列表
* 请删除列表中的第2个元素，并输出删除的元素的值和删除元素后的列表
* 请删除列表中的第3个元素，并输出删除元素后的列表
* 请删除列表中的第2至4个元素，并输出删除元素后的列表
* 请将列表所有的元素反转，并输出反转后的列表
* 请使用for、len、range输出列表的索引
* 请使用enumrate输出列表元素和序号（序号从100开始）
* 请使用for循环输出列表的所有元素

```python
li=['alex', 'eric', 'rain']
# 计算列表长度并输出
print(len(li))

# 列表中追加元素“seven”，并输出添加后的列表
li.append("seven")
print(li)

# 请在列表的第1个位置插入元素“Tony”，并输出添加后的列表
li.insert(0, "Tony")
print(li)

# 请修改列表第2个位置的元素为“Kelly”，并输出修改后的列表
li[1] = "Kelly"
print(li)

# 请删除列表中的元素“eric”，并输出修改后的列表
li.remove("eric")  # 指定的是元素
print(li)

# 请删除列表中的第2个元素，并输出删除的元素的值和删除元素后的列表
li_pop = li.pop(1)  # 指定的是下标位置
print(li_pop, li)

# 请删除列表中的第3个元素，并输出删除元素后的列表
del li[2]  # 指定的是下标位置
print(li)

# 请删除列表中的第2至4个元素，并输出删除元素后的列表

# 请将列表所有的元素反转，并输出反转后的列表

# 请使用for、len、range输出列表的索引
for i in range(len(li)):
    print(i)

# 请使用enumrate输出列表元素和序号（序号从100开始）
for index, val in enumerate(li, 100):
    print(index)

# 请使用for循环输出列表的所有元素
for i in li:
    print(i)
```

4、写代码，有如下列表，请按照功能要求实现每一个功能

li = \["hello", 'seven', \["mon", \["h", "kelly"\], 'all'\], 123, 446\]

* 请根据索引输出“Kelly”  
* 请使用索引找到'all'元素并将其修改为“ALL”，如：li\[0\]\[1\]\[9\]...

```
# 请根据索引输出“Kelly”
li[2][1][1]
# 请使用索引找到'all'元素并将其修改为“ALL”，如：li[0][1][9]...
li[2][2].upper()
li[2][2] = "ALL"
```

5、写代码，有如下元组，请按照功能要求实现每一个功能

tu＝\('alex', 'eric', 'rain'\)

* 计算元组长度并输出
* 获取元组的第2个元素，并输出
* 获取元组的第1-2个元素，并输出
* 请使用for输出元组的元素
* 请使用for、len、range输出元组的索引
* 请使用enumrate输出元祖元素和序号（序号从10开始）

```pthon
# 计算元组长度并输出
print(len(t))
# 获取元组的第2个元素，并输出
print(t[1])
# 获取元组的第1-2个元素，并输出
print(t[1:2])
# 请使用for输出元组的元素
for i in t:
    print(i)
# 请使用for、len、range输出元组的索引
for i in range(len(t)):
    print(i)
请使用enumrate输出元祖元素和序号（序号从10开始）
for index, val in enumerate(t, 10):
    print(index)
```

6、有如下变量，请实现要求的功能

tu = \("alex", \[11, 22, {"k1": 'v1', "k2": \["age", "name"\], "k3": \(11,22,33\)}, 44\]\)

* 讲述元祖的特性
* 请问tu变量中的第一个元素“alex”是否可被修改？
* 请问tu变量中的"k2"对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven”
* 请问tu变量中的"k3"对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven”

```python
# 讲述元祖的特性
1、有序的集合
2、通过偏移来取数据
3、属于不可变的对象，不能在原地修改内容，没有排序，修改等操作。
# 请问tu变量中的第一个元素“alex”是否可被修改？
上题中的元组的第三个特点
# 请问tu变量中的"k2"对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven”
type(tu[1][2]["k2"])  -- list
可以
tu[1][2]["k2"].append("Seven")
# 请问tu变量中的"k3"对应的值是什么类型？是否可以被修改？如果可以，请在其中添加一个元素“Seven”
type(tu[1][2]["k3"])
tuple
不可以
```

7、字典

dic = {'k1': "v1", "k2": "v2", "k3": \[11,22,33\]}

* 请循环输出所有的key
* 请循环输出所有的value
* 请循环输出所有的key和value
* 请在字典中添加一个键值对，"k4": "v4"，输出添加后的字典
* 请在修改字典中“k1”对应的值为“alex”，输出修改后的字典
* 请在k3对应的值中追加一个元素44，输出修改后的字典
* 请在k3对应的值的第1个位置插入个元素18，输出修改后的字典

```python
# 请循环输出所有的key
dic.keys()
# 请循环输出所有的value
dic.values()
# 请循环输出所有的key和value
dic.items()
# 请在字典中添加一个键值对，"k4": "v4"，输出添加后的字典
dic["k4"] = "v4"
# 请在修改字典中“k1”对应的值为“alex”，输出修改后的字典
dic["k1"] = "alex"
{'k2': 'v2', 'k1': 'alex', 'k3': [11, 22, 33]}
# 请在k3对应的值中追加一个元素44，输出修改后的字典
dic["k3"].append(44)
{'k2': 'v2', 'k1': 'v1', 'k3': [11, 22, 33, 44]}
# 请在k3对应的值的第1个位置插入个元素18，输出修改后的字典
dic["k3"].insert(1, 18)
{'k2': 'v2', 'k1': 'v1', 'k3': [11, 18, 22, 33]}
```

8、转换

* 将字符串s = "alex"转换成列表
* 将字符串s = "alex"转换成元祖
* 将列表li = \["alex", "seven"\]转换成元组
* 将元祖tu = \('Alex', "seven"\)转换成列表
* 将列表li = \["alex", "seven"\]转换成字典且字典的key按照10开始向后递增

```python
# 将字符串s = "alex"转换成列表
list(s)
# 将字符串s = "alex"转换成元祖
tuple(s)
# 将列表li = ["alex", "seven"]转换成元组
tuple(li)
# 将元祖tu = ('Alex', "seven")转换成列表
list(tu)
# 将列表li = ["alex", "seven"]转换成字典且字典的key按照10开始向后递增
dict(zip([i for i in range(10, len(li)+11)], li))
```

9、元素分类

有如下值集合\[11,22,33,44,55,66,77,88,99,90\]，将所有大于66的值保存至字典的第一个key中，将小于66的值保存至第二个key的值中。

即：{'k1':大于66的所有值, 'k2':小于66的所有值}

```python
li = [11, 22, 33, 44, 55, 66, 77, 88, 99]
dic = {
    "k1": [],
    "k2": [],
}

for i in li:
    if i >= 66:
        dic["k1"].append(i)
    else:
        dic["k2"].append(i)

print(dic)
```

10、输出商品列表，用户输入序号，显示用户选中的商品

商品li = \["手机", "电脑", '鼠标垫', '游艇'\]

* 允许用户添加商品
* 用户输入序号显示内容

```python
goods = [
    {"name": "电脑", "price": 1999},
    {"name": "鼠标", "price": 10},
    {"name": "游艇", "price": 20},
    {"name": "美女", "price": 998}
]

wages = int(input('请输入工资：'))
shopping_car = []
exit_flag = False
while not exit_flag:
    print('--------商品列表--------')
    for index, i in enumerate(goods):
        print(index, i)
    choice = (input('请输入要购买的商品：'))
    if choice.isdigit():  
        if 0 <= int(choice) < len(goods):
            if wages >= goods[int(choice)].get('price'):  
                wages -= goods[int(choice)].get('price')
                print('\033[32;1m余额：\033[0m', wages)
                shopping_car.append(goods[int(choice)])
                print("\033[32;1m已将商品：%s 添加进购物车\033[0m" % (goods[int(choice)]))
            else:
                print('\033[31;1m余额不足\033[0m')
        else:
            print('\033[31;1m商品不存在！\033[0m')
    elif choice == "q":
        print('-----您已购买以下商品-----')
        for index, k in enumerate(shopping_car):
            print(index, k)
        print('\033[32;1m账户余额\033[0m', wages)
        exit_flag = True
    elif choice == "a":
        print("----您当前处于商品添加页面----")
        print("当前存在的商品：")
        for index, i in enumerate(goods):  
            print(index, i)
        name = input("商品名称：")
        price = input("商品价格：")

        dic = {"name": name, "price": price}

        goods.append(dic)
        print("添加成功：")
        for index, i in enumerate(goods):  # enumerate（枚举）列表的索引值
            print(index, i)
```

11、用户交互显示类似省市县N级联动的选择

* 允许用户增加内容
* 允许用户选择查看某一个级别内容

12、列举布尔值是False的所有值

13、有两个列表

​    l1 = \[11,22,33\]

​    l2 = \[22,33,44\]

* 获取内容相同的元素列表
* 获取l1中有，l2中没有的元素列表
* 获取l2中有，l3中没有的元素列表
* 获取l1和l2中内容都不同的元素

14、利用For循环和range输出

* For循环从大到小输出1 - 100
* For循环从小到到输出100 - 1
* While循环从大到小输出1 - 100
* While循环从小到到输出100 - 1

```python

```

15、利用for循环和range输出9 \* 9乘法表

```python
print('\n'.join([ ' '.join([ "%d*%d=%2s" %(y,x,x*y) for y in range(1,x+1)]) for x in range(1,10)]))
```

16、求100以内的素数和。（编程题）

\#求解思路，loop 100次，每次拿当前的值依次除以比它小的值，比如 当前值 是10， 那就拿10除以9，8，7，6，...2，如果其中任何一个可以被整除，就代表 10不是素数

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
# 素数又称为质数，它指的是只能被1和它本身整除的整数。其中，1不是素数，任何时候都不用考虑1。

L = [] # 定义一个初始的素数列表
for n in range(2,101): # 循环100以内的素数n,从2开始,0、1不是素数
    flag = True # 设置一个标志位,flag = True代表是素数，flag = Flase代表不是素数
    for i in range(2,n): # 除以比它小的所有数（不包括1和它本身）,看它是否还有其他因数
        if n % i == 0:
            flag = False # 出现一次余数为0就代表可以除尽，即代表这个数为素数，就可以设置flag = False
            break # 只要第一次出现flag = False，就不用继续往下循环，直接退出整个循环（第二层）
    if flag == True:
        L.append(n) # 当flag = True时代表n为素数,追加到素数列表中
print("100以内的所有素数:",L)
print(sum(L))
```

17. 在不改变列表中数据排列结构的前提下，找出以下列表中最接近最大值和最小值的平均值 的数

```python
# 解题思路，找到最大值 ，找到最小值 ，求平均值 ，找到列表中离这个平均值 最近的值
li = [-100,1,3,2,7,6,120,121,140,23,411,99,243,33,85,56]

max_n = li[0]
min_n = li[0]

for i in li:
    if i > max_n:
        max_n = i
    if i < min_n:
        min_n = i
avg_n = (min_n+max_n)//2
print(min_n,max_n,avg_n)

avg_like = li[0]
for i in li:
    if abs(i - avg_n) < abs(avg_like - avg_n):
        avg_like = i
print('最接近平均值 的是',avg_like)
```



