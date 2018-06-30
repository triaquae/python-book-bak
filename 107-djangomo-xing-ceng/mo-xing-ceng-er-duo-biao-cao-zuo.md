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
-	对于外键字段，Django 会在字段名上添加"\_id" 来创建数据库中的列名
-	这个例子中的CREATE TABLE SQL 语句使用PostgreSQL 语法格式，要注意的是Django 会根据settings 中指定的数据库类型来使用相应的SQL 语句。
-	定义好模型之后，你需要告诉Django \_使用_这些模型。你要做的就是修改配置文件中的INSTALL_APPSZ中设置，在其中添加models.py所在应用的名称。
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

create(\*\*kwargs)

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

如果外键关系满足null=True，关联管理器会在添加new\_list中的内容之前，首先调用clear()方法来解除关联集中一切已存在对象的关联。否则， new\_list中的对象会在已存在的关联的基础上被添加。　　

### 三、基于对象的跨表查询

一对多查询（Publish 与 Book）  
正向查询(按字段：publish)：  

```py
# 查询主键为1的书籍的出版社所在的城市
book_obj=Book.objects.filter(pk=1).first()
# book_obj.publish 是主键为1的书籍对象关联的出版社对象
print(book_obj.publish.city) 　
```

反向查询(按表名：book_set)：

```py
publish=Publish.objects.get(name="苹果出版社")
#publish.book_set.all() : 与苹果出版社关联的所有书籍对象集合
book_list=publish.book_set.all()    
for book_obj in book_list:
       print(book_obj.title)
```

一对一查询(Author 与 AuthorDetail)  
正向查询(按字段：authorDetail)：  

```py
egon=Author.objects.filter(name="egon").first()
print(egon.authorDetail.telephone)
```

反向查询(按表名：author)：

```py
# 查询所有住址在北京的作者的姓名

authorDetail_list=AuthorDetail.objects.filter(addr="beijing")
for obj in authorDetail_list:
     print(obj.author.name)
```

多对多查询 (Author 与 Book)  
正向查询(按字段：authors)：  

```py
# 金瓶眉所有作者的名字以及手机号

book_obj=Book.objects.filter(title="金瓶眉").first()
authors=book_obj.authors.all()
for author_obj in authors:
     print(author_obj.name,author_obj.authorDetail.telephone)
```

反向查询(按表名：book_set)：

```py
# 查询egon出过的所有书籍的名字

    author_obj=Author.objects.get(name="egon")
    book_list=author_obj.book_set.all()        #与egon作者相关的所有书籍
    for book_obj in book_list:
        print(book_obj.title)
```

注意：  
你可以通过在 ForeignKey() 和ManyToManyField的定义中设置 related_name 的值来覆写 FOO_set 的名称。例如，如果 Article model 中做一下更改：  

```py
publish = ForeignKey(Book, related_name='bookList')
```

那么接下来就会如我们看到这般：

```py
# 查询 人民出版社出版过的所有书籍

publish=Publish.objects.get(name="人民出版社")
book_list=publish.bookList.all()  # 与人民出版社关联的所有书籍对象集合
```

### 四、基于双下划线的跨表查询
Django 还提供了一种直观而高效的方式在查询(lookups)中表示关联关系，它能自动确认 SQL JOIN 联系。要做跨关系查询，就使用两个下划线来链接模型(model)间关联字段的名称，直到最终链接到你想要的 model 为止。  
关键点：正向查询按字段，反向查询按表名。  

一对多查询

```py
# 练习1:  查询苹果出版社出版过的所有书籍的名字与价格(一对多)
     # 正向查询 按字段:publish
     queryResult=Book.objects
　　　　　　　　　　　　.filter(publish__name="苹果出版社")
　　　　　　　　　　　　.values_list("title","price")
     # 反向查询 按表名:book
     queryResult=Publish.objects
　　　　　　　　　　　　　　.filter(name="苹果出版社")
　　　　　　　　　　　　　　.values_list("book__title","book__price")
```

多对多查询　

```py
# 练习2: 查询alex出过的所有书籍的名字(多对多)
     # 正向查询 按字段:authors:
    queryResult=Book.objects
　　　　　　　　　　　　.filter(authors__name="yuan")
　　　　　　　　　　　　.values_list("title")
     # 反向查询 按表名:book
    queryResult=Author.objects
　　　　　　　　　　　　　　.filter(name="yuan")
　　　　　　　　　　　　　　.values_list("book__title","book__price")
```

混合使用

```py
# 练习3: 查询人民出版社出版过的所有书籍的名字以及作者的姓名

    # 正向查询
    queryResult=Book.objects
　　　　　　　　　　　　.filter(publish__name="人民出版社")
　　　　　　　　　　　　.values_list("title","authors__name")
    # 反向查询
    queryResult=Publish.objects
　　　　　　　　　　　　　　.filter(name="人民出版社")
　　　　　　　　　　　　　　.values_list("book__title","book__authors__age","book__authors__name")

# 练习4: 手机号以151开头的作者出版过的所有书籍名称以及出版社名称

    queryResult=Book.objects
　　　　　　　　　　　　.filter(authors__authorDetail__telephone__regex="151")
　　　　　　　　　　　　.values_list("title","publish__name")
```

注意：  
反向查询时，如果定义了related_name ，则用related_name替换表名，例如：  

```py
publish = ForeignKey(Blog, related_name='bookList')
```

练习1: 查询人民出版社出版过的所有书籍的名字与价格(一对多)

```py
#反向查询 不再按表名:book,而是related_name:bookList

queryResult=Publish.objects
　　　　　　　　　　.filter(name="人民出版社")
　　　　　　　　　　.values_list("bookList__title","bookList__price")
```

### 五、聚合查询与分组查询
聚合
aggregate(\*args, \*\*kwargs)

```py
# 计算所有图书的平均价格
    >>> from django.db.models import Avg
    >>> Book.objects.all().aggregate(Avg('price'))
    {'price__avg': 34.35}
```

aggregate()是QuerySet 的一个终止子句，意思是说，它返回一个包含一些键值对的字典。键的名称是聚合值的标识符，值是计算出来的聚合值。键的名称是按照字段和聚合函数的名称自动生成出来的。如果你想要为聚合值指定一个名称，可以向聚合子句提供它。

```py
>>> Book.objects.aggregate(average_price=Avg('price'))
{'average_price': 34.35}
```

如果你希望生成不止一个聚合，你可以向aggregate()子句中添加另一个参数。所以，如果你也想知道所有图书价格的最大值和最小值，可以这样查询：

```py
>>> from django.db.models import Avg, Max, Min
>>> Book.objects.aggregate(Avg('price'), Max('price'), Min('price'))
{'price__avg': 34.35, 'price__max': Decimal('81.20'), 'price__min': Decimal('12.99')}
```

分组

```py
###################################－－单表分组查询－－#######################################################
查询每一个部门名称以及对应的员工数
emp:
id  name age   salary    dep
1   alex  12   2000     销售部
2   egon  22   3000     人事部
3   wen   22   5000     人事部
sql语句:
select dep,Count(*) from emp group by dep;
ORM:
emp.objects.all().values("dep").annotate(Count("id")
###################################－－多表分组查询－－#######################################################
多表分组查询：
查询每一个部门名称以及对应的员工数
emp:
id  name age   salary   dep_id
1   alex  12   2000       1
2   egon  22   3000       2
3   wen   22   5000       2
dep
id   name
1    销售部
2    人事部
emp－dep:
id  name age   salary   dep_id   id   name
1   alex  12   2000       1      1    销售部
2   egon  22   3000       2      2    人事部
3   wen   22   5000       2      2    人事部
sql语句:
select dep.name,Count(*) from emp left join dep on emp.dep_id=dep.id group by emp.dep_id
select dep.name,Count(*) from emp left join dep on emp.dep_id=dep.id group by dep.id,dep.name
ORM:
dep.objetcs.all().annotate(c=Count("emp")).values("name","c")
```

annotate()为调用的QuerySet中每一个对象都生成一个独立的统计值（统计方法用聚合函数）。　  
(1) 练习：统计每一本书的作者个数  

```py
bookList=Book.objects.annotate(authorsNum=Count('authors'))
for book_obj in bookList:
    print(book_obj.title,book_obj.authorsNum)
```

```mysql
SELECT
"app01_book"."nid",
"app01_book"."title",
"app01_book"."publishDate",
"app01_book"."price",
"app01_book"."pageNum",
"app01_book"."publish_id",
COUNT("app01_book_authors"."author_id") AS "authorsNum"
FROM "app01_book" LEFT OUTER JOIN "app01_book_authors"
ON ("app01_book"."nid" = "app01_book_authors"."book_id")
GROUP BY
"app01_book"."nid",
"app01_book"."title",
"app01_book"."publishDate",
"app01_book"."price",
"app01_book"."pageNum",
"app01_book"."publish_id"
```

(2) 如果想对所查询对象的关联对象进行聚合：  
练习：统计每一个出版社的最便宜的书  

```py
publishList=Publish.objects.annotate(MinPrice=Min("book__price"))
for publish_obj in publishList:
    print(publish_obj.name,publish_obj.MinPrice)
```

annotate的返回值是querySet，如果不想遍历对象，可以用上valuelist：

```py
queryResult= Publish.objects
　　　　　　　　　　　　.annotate(MinPrice=Min("book__price"))
　　　　　　　　　　　　.values_list("name","MinPrice")
print(queryResult)
```

方式2:　

```py
queryResult=Book.objects.values("publish__name").annotate(MinPrice=Min('price')) ＃ 思考： if 有一个出版社没有出版过书会怎样？
```

(3) 统计每一本以py开头的书籍的作者个数：

```py
queryResult=Book.objects
　　　　　　　　　　 .filter(title__startswith="Py")
　　　　　　　　　 　.annotate(num_authors=Count('authors'))
```

(4) 统计不止一个作者的图书：

```py
queryResult=Book.objects
　　　　　　　　　　.annotate(num_authors=Count('authors'))
　　　　　　　　　　.filter(num_authors__gt=1)
```

(5) 根据一本图书作者数量的多少对查询集 QuerySet进行排序:

```py
Book.objects.annotate(num_authors=Count('authors')).order_by('num_authors')
```

(6) 查询各个作者出的书的总价格:

```py
#   按author表的所有字段 group by
    queryResult=Author.objects
　　　　　　　　　　　　　　.annotate(SumPrice=Sum("book__price"))
　　　　　　　　　　　　　　.values_list("name","SumPrice")
    print(queryResult)
```

### 六、F查询与Q查询
F查询  
在上面所有的例子中，我们构造的过滤器都只是将字段值与某个常量做比较。如果我们要对两个字段的值做比较，那该怎么做呢？  
Django 提供 F() 来做这样的比较。F() 的实例可以在查询中引用字段，来比较同一个 model 实例中两个不同字段的值。  

```py
# 查询评论数大于收藏数的书籍

   from django.db.models import F
   Book.objects.filter(commnetNum__lt=F('keepNum'))
```

Django 支持 F() 对象之间以及 F() 对象和常数之间的加减乘除和取模的操作。

```py
# 查询评论数大于收藏数2倍的书籍
    Book.objects.filter(commnetNum__lt=F('keepNum')*2)
```

修改操作也可以使用F函数,比如将每一本书的价格提高30元：

```py
Book.objects.all().update(price=F("price")+30)　
```

Q查询  
filter() 等方法中的关键字参数查询都是一起进行“AND” 的。 如果你需要执行更复杂的查询（例如OR 语句），你可以使用Q 对象。  

```py
from django.db.models import Q
Q(title__startswith='Py')
```

Q 对象可以使用& 和| 操作符组合起来。当一个操作符在两个Q 对象上使用时，它产生一个新的Q 对象。

```py
bookList=Book.objects.filter(Q(authors__name="yuan")|Q(authors__name="egon"))
```

等同于下面的SQL WHERE 子句：

```py
WHERE name ="yuan" OR name ="egon"
```

你可以组合& 和|  操作符以及使用括号进行分组来编写任意复杂的Q 对象。同时，Q 对象可以使用~ 操作符取反，这允许组合正常的查询和取反(NOT) 查询：

```py
bookList=Book.objects.filter(Q(authors__name="yuan") & ~Q(publishDate__year=2017)).values_list("title")
```

查询函数可以混合使用Q 对象和关键字参数。所有提供给查询函数的参数（关键字参数或Q 对象）都将"AND”在一起。但是，如果出现Q 对象，它必须位于所有关键字参数的前面。例如：

```py
bookList=Book.objects.filter(Q(publishDate__year=2016) | Q(publishDate__year=2017),
                              title__icontains="python"
                             )
```
