### 7.3 多表操作

#### 一、创建模型
实例：我们来假定下面这些概念，字段和关系  
作者模型：一个作者有姓名和年龄。  
作者详细模型：把作者的详情放到详情表，包含生日，手机号，家庭住址等信息。作者详情模型和作者模型之间是一对一的关系（one-to-one）  
出版商模型：出版商有名称，所在城市以及email。  
书籍模型： 书籍有书名和出版日期，一本书可能会有多个作者，一个作者也可以写多本书，所以作者和书籍的关系就是多对多的关联关系(many-to-many);一本书只应该由一个出版商出版，所以出版商和书籍是一对多关联关系(one-to-many)。  
模型建立如下：  

```py
from django.db import models
# Create your models here.

class Author(models.Model):
    nid = models.AutoField(primary_key=True)
    name=models.CharField( max_length=32)
    age=models.IntegerField()

    # 与AuthorDetail建立一对一的关系
    authorDetail=models.OneToOneField(to="AuthorDetail",on_delete=models.CASCADE)

class AuthorDetail(models.Model):

    nid = models.AutoField(primary_key=True)
    birthday=models.DateField()
    telephone=models.BigIntegerField()
    addr=models.CharField( max_length=64)

class Publish(models.Model):
    nid = models.AutoField(primary_key=True)
    name=models.CharField( max_length=32)
    city=models.CharField( max_length=32)
    email=models.EmailField()

class Book(models.Model):

    nid = models.AutoField(primary_key=True)
    title = models.CharField( max_length=32)
    publishDate=models.DateField()
    price=models.DecimalField(max_digits=5,decimal_places=2)

    # 与Publish建立一对多的关系,外键字段建立在多的一方
    publish=models.ForeignKey(to="Publish",to_field="nid",on_delete=models.CASCADE)
    # 与Author表建立多对多的关系,ManyToManyField可以建在两个模型中的任意一个，自动创建第三张表
    authors=models.ManyToManyField(to='Author',)
```

生成表如下：

![](https://hcdn1.luffycity.com/data/python-book/10102/10.png)  
![](https://hcdn1.luffycity.com/data/python-book/10102/11.png)  
![](https://hcdn1.luffycity.com/data/python-book/10102/12.png)  
![](https://hcdn1.luffycity.com/data/python-book/10102/13.png)  
![](https://hcdn1.luffycity.com/data/python-book/10102/14.png)  

注意事项：
-	表的名称myapp_modelName，是根据 模型中的元数据自动生成的，也可以覆写为别的名称　　
-	id 字段是自动添加的
-	对于外键字段，Django 会在字段名上添加"_id" 来创建数据库中的列名
-	这个例子中的CREATE TABLE SQL 语句使用PostgreSQL 语法格式，要注意的是Django 会根据settings 中指定的数据库类型来使用相应的SQL 语句。
-	定义好模型之后，你需要告诉Django _使用_这些模型。你要做的就是修改配置文件中的INSTALL_APPSZ中设置，在其中添加models.py所在应用的名称。
-	外键字段 ForeignKey 有一个 null=True 的设置(它允许外键接受空值 NULL)，你可以赋给它空值 None 。

#### 二、添加表纪录
操作前先简单的录入一些数据：  
publish表：  

![](https://hcdn1.luffycity.com/data/python-book/10102/15.png)  

author表：

![](https://hcdn1.luffycity.com/data/python-book/10102/16.png)  

authordetail表:

![](https://hcdn1.luffycity.com/data/python-book/10102/17.png)  


一对多

```py
方式1:
   publish_obj=Publish.objects.get(nid=1)
   book_obj=Book.objects.create(title="金瓶眉",publishDate="2012-12-12",price=100,publish=publish_obj)

方式2:
   book_obj=Book.objects.create(title="金瓶眉",publishDate="2012-12-12",price=100,publish_id=1)　　
```


![](https://hcdn1.luffycity.com/data/python-book/10102/18.png)  

核心：book\_obj.publish与book\_obj.publish\_id是什么？

多对多

```py
# 当前生成的书籍对象
    book_obj=Book.objects.create(title="追风筝的人",price=200,publishDate="2012-11-12",publish_id=1)
    # 为书籍绑定的做作者对象
    yuan=Author.objects.filter(name="yuan").first() # 在Author表中主键为2的纪录
    egon=Author.objects.filter(name="alex").first() # 在Author表中主键为1的纪录

    # 绑定多对多关系,即向关系表book_authors中添加纪录
    book_obj.authors.add(yuan,egon)    #  将某些特定的 model 对象添加到被关联对象集合中。   =======    book_obj.authors.add(*[])
```

数据库表纪录生成如下：  
book表  

![](https://hcdn1.luffycity.com/data/python-book/10102/19.png)  

book_authors表

![](https://hcdn1.luffycity.com/data/python-book/10102/20.png)  

核心:book\_obj.authors.all()是什么？  
多对多关系其它常用API：  

```py
book_obj.authors.remove()      # 将某个特定的对象从被关联对象集合中去除。    ======   book_obj.authors.remove(*[])
book_obj.authors.clear()       #清空被关联对象集合
book_obj.authors.set()         #先清空再设置　　
```

补充 class RelatedManager

"关联管理器"是在一对多或者多对多的关联上下文中使用的管理器。它存在于下面两种情况：  
ForeignKey关系的“另一边”。像这样：  

```py
from django.db import models

class Reporter(models.Model):
    # ...
    pass

class Article(models.Model):
    reporter = models.ForeignKey(Reporter)
```

在上面的例子中，管理器reporter.article_set拥有下面的方法。  
ManyToManyField关系的两边：  

```py
class Topping(models.Model):
    # ...
    pass

class Pizza(models.Model):
    toppings = models.ManyToManyField(Topping)
```

这个例子中，topping.pizza_set 和pizza.toppings都拥有下面的方法。  
add(obj1[, obj2, ...])  


```py
把指定的模型对象添加到关联对象集中。

例如：

>>> b = Blog.objects.get(id=1)
>>> e = Entry.objects.get(id=234)
>>> b.entry_set.add(e) # Associates Entry e with Blog b.
在上面的例子中，对于ForeignKey关系，e.save()由关联管理器调用，执行更新操作。然而，在多对多关系中使用add()并不会调用任何 save()方法，而是由QuerySet.bulk_create()创建关系。

延伸：

# 1 *[]的使用
>>> book_obj = Book.objects.get(id=1)
>>> author_list = Author.objects.filter(id__gt=2)
>>> book_obj.authors.add(*author_list)


# 2 直接绑定主键
book_obj.authors.add(*[1,3])  # 将id=1和id=3的作者对象添加到这本书的作者集合中
                              # 应用: 添加或者编辑时,提交作者信息时可以用到.  
```

create(**kwargs)

```py
创建一个新的对象，保存对象，并将它添加到关联对象集之中。返回新创建的对象：

>>> b = Blog.objects.get(id=1)
>>> e = b.entry_set.create(
...     headline='Hello',
...     body_text='Hi',
...     pub_date=datetime.date(2005, 1, 1)
... )

# No need to call e.save() at this point -- it's already been saved.
这完全等价于（不过更加简洁于）：

>>> b = Blog.objects.get(id=1)
>>> e = Entry(
...     blog=b,
...     headline='Hello',
...     body_text='Hi',
...     pub_date=datetime.date(2005, 1, 1)
... )
>>> e.save(force_insert=True)
要注意我们并不需要指定模型中用于定义关系的关键词参数。在上面的例子中，我们并没有传入blog参数给create()。Django会明白新的 Entry对象blog 应该添加到b中。
```

remove(obj1[, obj2, ...])

```py
从关联对象集中移除执行的模型对象：

>>> b = Blog.objects.get(id=1)
>>> e = Entry.objects.get(id=234)
>>> b.entry_set.remove(e) # Disassociates Entry e from Blog b.
对于ForeignKey对象，这个方法仅在null=True时存在。
```

clear()

```py
从关联对象集中移除一切对象。

>>> b = Blog.objects.get(id=1)
>>> b.entry_set.clear()
注意这样不会删除对象 —— 只会删除他们之间的关联。

就像 remove() 方法一样，clear()只能在 null=True的ForeignKey上被调用。
```

set()方法  
先清空，在设置，编辑书籍时即可用到  

![](https://hcdn1.luffycity.com/data/python-book/10102/21.png)  

注意  
对于所有类型的关联字段，add()、create()、remove()和clear(),set()都会马上更新数据库。换句话说，在关联的任何一端，都不需要再调用save()方法。  
直接赋值：  
通过赋值一个新的可迭代的对象，关联对象集可以被整体替换掉。  

```py
>>> new_list = [obj1, obj2, obj3]
>>> e.related_set = new_list
```

如果外键关系满足null=True，关联管理器会在添加new_list中的内容之前，首先调用clear()方法来解除关联集中一切已存在对象的关联。否则， new_list中的对象会在已存在的关联的基础上被添加。　　
