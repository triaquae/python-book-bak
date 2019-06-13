随着学习的深入，用不了多久，你就可以写复杂的上千甚至上万行的代码啦，有些代码你花了很久写出来，过了些天再回去看，发现竟然看不懂了，哈哈，这太正常了。 另外，你以后在工作中会发现，一个项目多是由几个甚至几十个开发人员一起做，你要调用别人写的代码，别人也要用你的，如果代码不加注释，你自己都看不懂，更别说别人了，这样写会挨打的。所以为了避免这种尴尬的事情发生，一定要增加你代码的可读性。

代码注释分单行和多行注释， 单行注释用`#`，多行注释可以用三对双引号`“”” “””`

下面给大家看一段标准代码的注释，忽略代码意思

```py
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

1. 不用给全部代码加注释，只需要在自己觉得重要或不好理解的部分加注释即可

2. 注释可以用中文或英文，但绝对不要拼音噢

3. 注释不光要给自己看，还要给别人看，所以请认真写

  




  


