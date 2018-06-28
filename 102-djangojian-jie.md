### 3.1 MVC与MTV模型  
MVC  
Web服务器开发领域里著名的MVC模式，所谓MVC就是把Web应用分为模型(M)，控制器(C)和视图(V)三层，他们之间以一种插件式的、松耦合的方式连接在一起，模型负责业务对象与数据库的映射(ORM)，视图负责与用户的交互(页面)，控制器接受用户的输入调用模型和视图完成用户的请求，其示意图如下所示：  

![](https://hcdn1.luffycity.com/data/python-book/10102/01.png) 

MTV  
Django的MTV模式本质上和MVC是一样的，也是为了各组件间保持松耦合关系，只是定义上有些许不同，Django的MTV分别是值：  
1. M 代表模型（Model）： 负责业务对象和数据库的关系映射(ORM)。
2. T 代表模板 (Template)：负责如何把页面展示给用户(html)。
3. V 代表视图（View）：   负责业务逻辑，并在适当时候调用Model和Template。  
除了以上三层之外，还需要一个URL分发器，它的作用是将一个个URL的页面请求分发给不同的View处理，View再调用相应的Model和Template，MTV的响应模式如下所示：  

![](https://hcdn1.luffycity.com/data/python-book/10102/02.png)   


一般是用户通过浏览器向我们的服务器发起一个请求(request)，这个请求回去访问视图函数，（如果不涉及到数据调用，那么这个时候视图函数返回一个模板也就是一个网页给用户），视图函数调用模型，模型去数据库查找数据，然后逐级返回，视图函数把返回的数据填充到模板中空格中，最后返回网页给用户。

### 3.2 Django的下载与基本命令

1、下载Django：

```py
pip3 install django
```

2、创建一个django project

```py
django-admin.py startproject mysite
```

当前目录下会生成mysite的工程，目录结构如下：

![](https://hcdn1.luffycity.com/data/python-book/10102/03.png) 

    
manage.py ----- Django项目里面的工具，通过它可以调用django shell和数据库等。  
settings.py ---- 包含了项目的默认设置，包括数据库信息，调试标志以及其他一些工作的变量。  
urls.py ----- 负责把URL模式映射到应用程序。  


3、在mysite目录下创建应用

```py
python manage.py startapp blog
```

![](https://hcdn1.luffycity.com/data/python-book/10102/04.png) 

4、启动django项目

```py
python manage.py runserver 8080
```

这样我们的django就启动起来了！当我们访问：http://127.0.0.1:8080/时就可以看到：

![](https://hcdn1.luffycity.com/data/python-book/10102/05.png) 

### 3.3 基于Django实现的一个简单示例

url控制器


```py
from django.contrib import admin
from django.urls import path

from app01 import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/',views.index),
]
```

视图

```py
from django.shortcuts import render

# Create your views here.

def index(request):

    import datetime
    now=datetime.datetime.now()
    ctime=now.strftime("%Y-%m-%d %X")

    return render(request,"index.html",{"ctime":ctime})
```

模板

```py
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h4>当前时间:{{ ctime }}</h4>

</body>
</html>
```

执行效果如下：

![](https://hcdn1.luffycity.com/data/python-book/10102/06.png) 

