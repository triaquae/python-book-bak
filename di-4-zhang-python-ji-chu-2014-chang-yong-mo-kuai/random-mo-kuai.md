## 本节重点：

* 使学员掌握random模块的使用

> **本节时长需控制在5分钟内**



程序中有很多地方需要用到随机字符，比如登录网站的随机验证码，通过random模块可以很容易生成随机字符串

```py
>>> random.randrange(1,10) #返回1-10之间的一个随机数，不包括10
>>> random.randint(1,10) #返回1-10之间的一个随机数，包括10

>>> random.randrange(0, 100, 2) #随机选取0到100间的偶数

>>> random.random()  #返回一个随机浮点数
>>> random.choice('abce3#$@1') #返回一个给定数据集合中的随机字符
'#'

>>> random.sample('abcdefghij',3)  #从多个字符中选取特定数量的字符
['a', 'd', 'b']

#生成随机字符串
>>> import string 
>>> ''.join(random.sample(string.ascii_lowercase + string.digits, 6)) 
'4fvda1'

#洗牌
>>> a
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> random.shuffle(a)
>>> a
[3, 0, 7, 2, 1, 6, 5, 8, 9, 4]
```



