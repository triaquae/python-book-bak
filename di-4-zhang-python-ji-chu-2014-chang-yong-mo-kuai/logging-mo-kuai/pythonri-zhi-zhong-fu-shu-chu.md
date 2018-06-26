### 问题起源：
​ 在学习了python的函数式编程后，又接触到了logging这样一个强大的日志模块。为了减少重复代码，应该不少同学和我一样便迫不及待的写了一个自己的日志函数，比如下面这样：

```py
# 这里为了便于理解，简单的展示了一个输出到屏幕的日志函数
def my_log():
    logger = logging.getLogger('mysql.log')

    ch = logging.StreamHandler()
    ch.setLevel(logging.ERROR)
    fmt = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    ch.setFormatter(fmt)
    logger.addHandler(ch)

    return logger

my_log().error('run one')
my_log().error('run two')
my_log().error('run three')
```

函数写好了，看起来似乎也没有问题，我们来运行一下！

结果如下：

```py
2018-06-21 13:06:37,569 - mysql.log - ERROR - run one
2018-06-21 13:06:37,569 - mysql.log - ERROR - run two
2018-06-21 13:06:37,569 - mysql.log - ERROR - run two
2018-06-21 13:06:37,569 - mysql.log - ERROR - run three
2018-06-21 13:06:37,569 - mysql.log - ERROR - run three
2018-06-21 13:06:37,569 - mysql.log - ERROR - run three
```

日志居然重复输出了，且数量递增。

### 问题解析

实际上`logger = logging.getLogger('mysql.log')`在执行时，没有每次生成一个新的logger，而是先检查内存中是否存在一个叫做‘mysql.log’的logger对象，存在则取出，不存在则新建。

实例化的logger对象具有‘handlers’这样一个属性来存储 Handler，代码演示如下：

```py
def my_log():
    logger = logging.getLogger('mysql.log')
    # 每次被调用后打印出logger的handlers列表
    print(logger.handlers)

    ch = logging.StreamHandler()
    ch.setLevel(logging.ERROR)
    fmt = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    ch.setFormatter(fmt)

    logger.addHandler(ch)

    return logger

my_log().error('run one')
my_log().error('run two')
my_log().error('run three')
```

运行结果：

```py
[]
2018-06-21 13:26:14,059 - mysql.log - ERROR - run one
[<StreamHandler <stderr> (ERROR)>]
2018-06-21 13:26:14,060 - mysql.log - ERROR - run two
2018-06-21 13:26:14,060 - mysql.log - ERROR - run two
[<StreamHandler <stderr> (ERROR)>, <StreamHandler <stderr> (ERROR)>]
2018-06-21 13:26:14,060 - mysql.log - ERROR - run three
2018-06-21 13:26:14,060 - mysql.log - ERROR - run three
2018-06-21 13:26:14,060 - mysql.log - ERROR - run three
```

1. logger.handlers最初是一个空列表，执行‘logger.addHandler(ch)’添加个‘StreamHandler’，输出一条日志
2. 在第二次被调用时，logger.handlers已经存在一个‘StreamHandler’，再次执行‘logger.addHandler(ch)’就会再次添加一个‘StreamHandler’，此时的logger有两个个‘StreamHandler’，输出两条重复的日志
3. 在第三次被调用时，logger.handlers已经存在两个‘StreamHandler’，再次执行‘logger.addHandler(ch)’就会再次添加一个，此时的logger有三个‘StreamHandler’，输出三条重复的日志

### 解决办法

#### 1. 改名换姓

```py
# 为日志函数添加一个name，每次调用时传入不同的日志名
def my_log(name):
    logger = logging.getLogger(name)

    ch = logging.StreamHandler()
    ch.setLevel(logging.ERROR)
    fmt = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    ch.setFormatter(fmt)
    logger.addHandler(ch)

    return logger

my_log('log1').error('run one')
my_log('log2').error('run two')
my_log('log3').error('run three')
```

运行结果：

```py
2018-06-21 13:40:51,685 - log1 - ERROR - run one
2018-06-21 13:40:51,685 - log2 - ERROR - run two
2018-06-21 13:40:51,685 - log3 - ERROR - run three
```

#### 2.及时清理（logger.handlers.clear）

```py
def my_log():
    logger = logging.getLogger()
    # 每次被调用后，清空已经存在handler
    logger.handlers.clear()

    ch = logging.StreamHandler()
    ch.setLevel(logging.ERROR)
    fmt = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    ch.setFormatter(fmt)

    logger.addHandler(ch)

    return logger

my_log().error('run one')
my_log().error('run two')
my_log().error('run three')

```

**ps：removeHandler方法（兼容性较差）**

```py
# 这种写法下的可以使用removeHandler方法(logger.handlers.clear也可以使用在这种写法的函数内)
import logging

def my_log(msg):
    logger = logging.getLogger('mysql.log')

    ch = logging.StreamHandler()
    ch.setLevel(logging.ERROR)
    fmt = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    ch.setFormatter(fmt)

    logger.addHandler(ch)
    logger.error(msg)
    # 在使用完ch后从移除
    logger.removeHandler(ch)

my_log('run one')
my_log('run two')
my_log('run three')
```

#### 3.用前判断

```py
import logging

def my_log():
    logger = logging.getLogger('mysql.log')
    # 判断logger是否已经添加过handler，是则直接返回logger对象，否则执行handler设定以及addHandler(ch)
    if not logger.handlers:
        ch = logging.StreamHandler()
        ch.setLevel(logging.ERROR)
        fmt = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
        ch.setFormatter(fmt)

        logger.addHandler(ch)

    return logger

my_log().error('run one')
my_log().error('run two')
my_log().error('run three')
```

### 总结

​ 第一次遇到日志重复输出问题，那时还没有学习到面向对象编程的内容，当时并没有真正理解logging模块。学习完面向对象编程后，回过头来再思考这些问题有了豁然开朗的感觉。

​ 比如起初对`logging.getLogger`的实际原理不是很理解，在学习了面向对象编程中的hasattr、getattr、setattr这样一些方法后就恍然大悟了。所以诸君如果现在还是对logging模块不太理解，不妨先不纠结于这些细节，继续学下去。

​ 知识面扩充后，曾经的一些难题自然就会迎刃而解：）

***注：转载路飞学员https://www.jianshu.com/p/92aa9b1ce9e7***

