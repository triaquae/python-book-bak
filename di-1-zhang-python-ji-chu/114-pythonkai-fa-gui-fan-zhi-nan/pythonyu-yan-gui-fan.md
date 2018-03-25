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

#### 定义:

模块间共享代码的重用机制.

#### 优点:

命名空间管理约定十分简单. 每个标识符的源都用一种一致的方式指示. x.Obj表示Obj对象定义在模块x中.

#### 缺点:

模块名仍可能冲突. 有些模块名太长, 不太方便.

#### 结论:
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

