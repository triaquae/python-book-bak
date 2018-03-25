#### Lint

```python
对你的代码运行pylint
```

##### 定义:

pylint是一个在Python源代码中查找bug的工具. 对于C和C++这样的不那么动态的(译者注: 原文是less dynamic)语言, 这些bug通常由编译器来捕获. 由于Python的动态特性, 有些警告可能不对. 不过伪告警应该很少.

##### 优点:

可以捕获容易忽视的错误, 例如输入错误, 使用未赋值的变量等.

##### 缺点:

pylint不完美. 要利用其优势, 我们有时侯需要: a) 围绕着它来写代码 b) 抑制其告警 c) 改进它, 或者d) 忽略它.

##### 结论:

确保对你的代码运行pylint.抑制不准确的警告,以便能够将其他警告暴露出来。

你可以通过设置一个行注释来抑制告警. 例如:

```python
dict = 'something awful'  # Bad Idea... pylint: disable=redefined-builtin
```

pylint警告是以一个数字编号(如 ```C0112``` )和一个符号名(如 ```empty-docstring``` )来标识的. 在编写新代码或更新已有代码时对告警进行抑制, 推荐使用符号名来标识.

如果警告的符号名不够见名知意，那么请对其增加一个详细解释。

采用这种抑制方式的好处是我们可以轻松查找抑制并回顾它们.

你可以使用命令 ```pylint --list-msgs``` 来获取pylint告警列表. 你可以使用命令 ```pylint --help-msg=C6409``` , 以获取关于特定消息的更多信息.

相比较于之前使用的 ```pylint: disable-msg``` , 本文推荐使用 ```pylint: disable``` .

要抑制”参数未使用”告警, 你可以用”\_”作为参数标识符, 或者在参数名前加```”unused_”```. 遇到不能改变参数名的情况, 你可以通过在函数开头”提到”它们来消除告警. 例如:

```python
def foo(a, unused_b, unused_c, d=None, e=None):
    _ = d, e
    return a
```

#### 导入

```python
仅对包和模块使用导入
```

##### 定义:

模块间共享代码的重用机制.
#
#### 优点:

命名空间管理约定十分简单. 每个标识符的源都用一种一致的方式指示. x.Obj表示Obj对象定义在模块x中.

##### 缺点:

模块名仍可能冲突. 有些模块名太长, 不太方便.

##### 结论:
使用 ```import x``` 来导入包和模块.

使用 ```from x import y``` , 其中x是包前缀, y是不带前缀的模块名.

使用 ```from x import y as z```, 如果两个要导入的模块都叫做y或者y太长了.

例如, 模块 ```sound.effects.echo``` 可以用如下方式导入:

```python
from sound.effects import echo
...
echo.EchoFilter(input, output, delay=0.7, atten=4)
```

导入时不要使用相对名称. 即使模块在同一个包中, 也要使用完整包名. 这能帮助你避免无意间导入一个包两次.

#### 包

```python
使用模块的全路径名来导入每个模块
```

##### 优点:

避免模块名冲突. 查找包更容易.

##### 缺点:

部署代码变难, 因为你必须复制包层次.

##### 结论:

所有的新代码都应该用完整包名来导入每个模块.

应该像下面这样导入:

```python
# Reference in code with complete name.
import sound.effects.echo

# Reference in code with just module name (preferred).
from sound.effects import echo
```

#### 异常

```python
允许使用异常, 但必须小心
```

##### 定义:

异常是一种跳出代码块的正常控制流来处理错误或者其它异常条件的方式.

##### 优点:

正常操作代码的控制流不会和错误处理代码混在一起. 当某种条件发生时, 它也允许控制流跳过多个框架. 例如, 一步跳出N个嵌套的函数, 而不必继续执行错误的代码.

##### 缺点:

可能会导致让人困惑的控制流. 调用库时容易错过错误情况.

##### 结论:

异常必须遵守特定条件:

1. 像这样触发异常: ```raise MyException("Error message")``` 或者 ```raise MyException``` . 不要使用两个参数的形式( ```raise MyException, "Error message"``` )或者过时的字符串异常( ```raise "Error message"``` ).

2. 模块或包应该定义自己的特定域的异常基类, 这个基类应该从内建的Exception类继承. 模块的异常基类应该叫做”Error”.

    ```python
    class Error(Exception):
        pass
    ```
    
3. 永远不要使用 ```except```: 语句来捕获所有异常, 也不要捕获 ```Exception``` 或者 ```StandardError``` , 除非你打算重新触发该异常, 或者你已经在当前线程的最外层(记得还是要打印一条错误消息). 在异常这方面, Python非常宽容, ```except```: 真的会捕获包括Python语法错误在内的任何错误. 使用 ```except```: 很容易隐藏真正的bug.

4. 尽量减少```try/except```块中的代码量. try块的体积越大, 期望之外的异常就越容易被触发. 这种情况下, ```try/except```块将隐藏真正的错误.

5. 使用finally子句来执行那些无论try块中有没有异常都应该被执行的代码. 这对于清理资源常常很有用, 例如关闭文件.

6. 当捕获异常时, 使用 ```as``` 而不要用逗号. 例如

```python
try:
    raise Error
except Error as error:
    pass
```

#### 全局变量

```python
避免全局变量
```

##### 定义:

定义在模块级的变量.

##### 优点:

偶尔有用.

##### 缺点:

导入时可能改变模块行为, 因为导入模块时会对模块级变量赋值.

##### 结论:

避免使用全局变量, 用类变量来代替. 但也有一些例外:

1. 脚本的默认选项.
2. 模块级常量. 例如:　PI = 3.14159. 常量应该全大写, 用下划线连接.
3. 有时候用全局变量来缓存值或者作为函数返回值很有用.
4. 如果需要, 全局变量应该仅在模块内部可用, 并通过模块级的公共函数来访问.

#### 嵌套/局部/内部类或函数

```python
鼓励使用嵌套/本地/内部类或函数
```

##### 定义:

类可以定义在方法, 函数或者类中. 函数可以定义在方法或函数中. 封闭区间中定义的变量对嵌套函数是只读的.

##### 优点:

允许定义仅用于有效范围的工具类和函数.

##### 缺点:

嵌套类或局部类的实例不能序列化(pickled).

##### 结论:

推荐使用.

#### 列表推导(List Comprehensions)

```python
可以在简单情况下使用
```

##### 定义:

列表推导(list comprehensions)与生成器表达式(generator expression)提供了一种简洁高效的方式来创建列表和迭代器, 而不必借助map(), filter(), 或者lambda.

##### 优点:

简单的列表推导可以比其它的列表创建方法更加清晰简单. 生成器表达式可以十分高效, 因为它们避免了创建整个列表.

##### 缺点:

复杂的列表推导或者生成器表达式可能难以阅读.

##### 结论:

适用于简单情况. 每个部分应该单独置于一行: 映射表达式, for语句, 过滤器表达式. 禁止多重for语句或过滤器表达式. 复杂情况下还是使用循环.

```python
Yes:
  result = []
  for x in range(10):
      for y in range(5):
          if x * y > 10:
              result.append((x, y))

  for x in xrange(5):
      for y in xrange(5):
          if x != y:
              for z in xrange(5):
                  if y != z:
                      yield (x, y, z)

  return ((x, complicated_transform(x))
          for x in long_generator_function(parameter)
          if x is not None)

  squares = [x * x for x in range(10)]

  eat(jelly_bean for jelly_bean in jelly_beans
      if jelly_bean.color == 'black')
```

```python
No:
  result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]

  return ((x, y, z)
          for x in xrange(5)
          for y in xrange(5)
          if x != y
          for z in xrange(5)
          if y != z)
```

#### 默认迭代器和操作符

```python
如果类型支持, 就使用默认迭代器和操作符. 比如列表, 字典及文件等.
```

##### 定义:

容器类型, 像字典和列表, 定义了默认的迭代器和关系测试操作符(in和not in)

##### 优点:

默认操作符和迭代器简单高效, 它们直接表达了操作, 没有额外的方法调用. 使用默认操作符的函数是通用的. 它可以用于支持该操作的任何类型.

##### 缺点:

你没法通过阅读方法名来区分对象的类型(例如, has_key()意味着字典). 不过这也是优点.

##### 结论:

如果类型支持, 就使用默认迭代器和操作符, 例如列表, 字典和文件. 内建类型也定义了迭代器方法. 优先考虑这些方法, 而不是那些返回列表的方法. 当然，这样遍历容器时，你将不能修改容器.

```python
Yes:  for key in adict: ...
      if key not in adict: ...
      if obj in alist: ...
      for line in afile: ...
      for k, v in dict.iteritems(): ...
```

```python
No:   for key in adict.keys(): ...
      if not adict.has_key(key): ...
      for line in afile.readlines(): ...
```

#### 生成器

```python
按需使用生成器.
```

##### 定义:

所谓生成器函数, 就是每当它执行一次生成(yield)语句, 它就返回一个迭代器, 这个迭代器生成一个值. 生成值后, 生成器函数的运行状态将被挂起, 直到下一次生成.

##### 优点:

简化代码, 因为每次调用时, 局部变量和控制流的状态都会被保存. 比起一次创建一系列值的函数, 生成器使用的内存更少.

##### 缺点:

没有.

##### 结论:

鼓励使用. 注意在生成器函数的文档字符串中使用”Yields:”而不是”Returns:”.

#### Lambda函数

```python
适用于单行函数
```

##### 定义:
与语句相反, lambda在一个表达式中定义匿名函数. 常用于为 map() 和 filter() 之类的高阶函数定义回调函数或者操作符.

##### 优点:

方便.

##### 缺点:

比本地函数更难阅读和调试. 没有函数名意味着堆栈跟踪更难理解. 由于lambda函数通常只包含一个表达式, 因此其表达能力有限.

##### 结论:

适用于单行函数. 如果代码超过60\-80个字符, 最好还是定义成常规(嵌套)函数.

对于常见的操作符，例如乘法操作符，使用 operator 模块中的函数以代替lambda函数. 例如, 推荐使用 operator.mul , 而不是 lambda x, y: x \* y .