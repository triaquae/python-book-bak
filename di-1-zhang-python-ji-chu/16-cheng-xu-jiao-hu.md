<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?9cae5942a3c39f3b6fcf0a32b00277e2";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>

## 本节重点：

* 使学生掌握如何让程序读取用户输入

> **本节时长需控制在15分钟之内**

## 读取用户输入\(5-8分钟\)

```py
name = input("What is your name?")

print("Hello " + name )
```

执行脚本就会发现，程序会等待你输入姓名后再往下继续走。

可以让用户输入多个信息，如下

```py
name = input("What is your name?")
age = input("How old are you?")
hometown = input("Where is your hometown?")

print("Hello ",name , "your are ", age , "years old, you came from",hometown)
```

执行输出

```bash
What is your name?Alex Li
How old are you?22
Where is your hometown?ShanDong
Hello  Alex Li your are  22 years old, you came from ShanDong
```

> 为避免学生蒙逼，py2.7 的raw\_input 以后再补充

## 注释\(5-8分钟\)

随着学习的深入，用不了多久，你就可以写复杂的上千甚至上万行的代码啦，有些代码你花了很久写出来，过了些天再回去看，发现竟然看不懂了，哈哈，这太正常了。 另外，你以后在工作中会发现，一个项目多是由几个甚至几十个开发人员一起做，你要调用别人写的代码，别人也要用你的，如果代码不加注释，你自己都看不懂，更别说别人了，这样写会挨打的。所以为了避免这种尴尬的事情发生，一定要增加你代码的可读性。

代码注释分单行和多行注释， 单行注释用`#`，多行注释可以用三对双引号`""" """`

下面给大家看一段标准代码的注释，忽略代码意思

```
def subclass_exception(name, parents, module, attached_to=None):
    """
    Create exception subclass. Used by ModelBase below.

    If 'attached_to' is supplied, the exception will be created in a way that
    allows it to be pickled, assuming the returned exception class will be added
    as an attribute to the 'attached_to' class.
    """
    class_dict = {'__module__': module}
    if attached_to is not None:
        def __reduce__(self):
            # Exceptions are special - they've got state that isn't
            # in self.__dict__. We assume it is all in self.args.
            return (unpickle_inner_exception, (attached_to, name), self.args)

        def __setstate__(self, args):
            self.args = args

        class_dict['__reduce__'] = __reduce__
        class_dict['__setstate__'] = __setstate__

    return type(name, parents, class_dict)
```

**代码注释原则:**

1. 不用全部加注释，只需要在自己觉得重要或不好理解的部分加注释即可
2. 注释可以用中文或英文，但绝对不要拼音噢 



