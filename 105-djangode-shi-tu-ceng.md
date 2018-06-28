### 5.1 视图函数
一个视图函数，简称视图，是一个简单的Python 函数，它接受Web请求并且返回Web响应。响应可以是一张网页的HTML内容，一个重定向，一个404错误，一个XML文档，或者一张图片. . . 是任何东西都可以。无论视图本身包含什么逻辑，都要返回响应。代码写在哪里也无所谓，只要它在你的Python目录下面。除此之外没有更多的要求了——可以说“没有什么神奇的地方”。为了将代码放在某处，约定是将视图放置在项目或应用程序目录中的名为views.py的文件中。
下面是一个返回当前日期和时间作为HTML文档的视图：  


```py
from django.shortcuts import render, HttpResponse, HttpResponseRedirect, redirect
import datetime

def current_datetime(request):
    now = datetime.datetime.now()
    html = "<html><body>It is now %s.</body></html>" % now
    return HttpResponse(html)
```

让我们逐行阅读上面的代码：  
1. 首先，我们从 django.shortcuts模块导入了HttpResponse类，以及Python的datetime库。
2. 接着，我们定义了current_datetime函数。它就是视图函数。每个视图函数都使用HttpRequest对象作为第一个参数，并且通常称之为request。  
注意,视图函数的名称并不重要；不需要用一个统一的命名方式来命名，以便让Django识别它。我们将其命名为current_datetime，是因为这个名称能够精确地反映出它的功能。
3. 这个视图会返回一个HttpResponse对象，其中包含生成的响应。每个视图函数都负责返回一个HttpResponse对象。

![](https://hcdn1.luffycity.com/data/python-book/10102/08.jpg)  

视图层，熟练掌握两个对象即可：请求对象(request)和响应对象(HttpResponse)

### 5.2 HttpRequest对象
request属性  
django将请求报文中的请求行、首部信息、内容主体封装成 HttpRequest 类中的属性。 除了特殊说明的之外，其他均为只读的。  

```py
/*

1.HttpRequest.GET
　　一个类似于字典的对象，包含 HTTP GET 的所有参数。详情请参考 QueryDict 对象。

2.HttpRequest.POST
　　一个类似于字典的对象，如果请求中包含表单数据，则将这些数据封装成 QueryDict 对象。
　　POST 请求可以带有空的 POST 字典 —— 如果通过 HTTP POST 方法发送一个表单，但是表单中没有任何的数据，QueryDict 对象依然会被创建。
   因此，不应该使用 if request.POST  来检查使用的是否是POST 方法；应该使用 if request.method == "POST"
　　另外：如果使用 POST 上传文件的话，文件信息将包含在 FILES 属性中。
     注意：键值对的值是多个的时候,比如checkbox类型的input标签，select标签，需要用：
        request.POST.getlist("hobby")

3.HttpRequest.body
　　一个字符串，代表请求报文的主体。在处理非 HTTP 形式的报文时非常有用，例如：二进制图片、XML,Json等。
　　但是，如果要处理表单数据的时候，推荐还是使用 HttpRequest.POST 。

4.HttpRequest.path
　　一个字符串，表示请求的路径组件（不含域名）。
　　例如："/music/bands/the_beatles/"

5.HttpRequest.method
　　一个字符串，表示请求使用的HTTP 方法。必须使用大写。
　　例如："GET"、"POST"

6.HttpRequest.encoding
　　一个字符串，表示提交的数据的编码方式（如果为 None 则表示使用 DEFAULT_CHARSET 的设置，默认为 'utf-8'）。
   这个属性是可写的，你可以修改它来修改访问表单数据使用的编码。
   接下来对属性的任何访问（例如从 GET 或 POST 中读取数据）将使用新的 encoding 值。
   如果你知道表单数据的编码不是 DEFAULT_CHARSET ，则使用它。

7.HttpRequest.META
 　　一个标准的Python 字典，包含所有的HTTP 首部。具体的头部信息取决于客户端和服务器，下面是一些示例：
    CONTENT_LENGTH —— 请求的正文的长度（是一个字符串）。
    CONTENT_TYPE —— 请求的正文的MIME 类型。
    HTTP_ACCEPT —— 响应可接收的Content-Type。
    HTTP_ACCEPT_ENCODING —— 响应可接收的编码。
    HTTP_ACCEPT_LANGUAGE —— 响应可接收的语言。
    HTTP_HOST —— 客服端发送的HTTP Host 头部。
    HTTP_REFERER —— Referring 页面。
    HTTP_USER_AGENT —— 客户端的user-agent 字符串。
    QUERY_STRING —— 单个字符串形式的查询字符串（未解析过的形式）。
    REMOTE_ADDR —— 客户端的IP 地址。
    REMOTE_HOST —— 客户端的主机名。
    REMOTE_USER —— 服务器认证后的用户。
    REQUEST_METHOD —— 一个字符串，例如"GET" 或"POST"。
    SERVER_NAME —— 服务器的主机名。
    SERVER_PORT —— 服务器的端口（是一个字符串）。
 　　从上面可以看到，除 CONTENT_LENGTH 和 CONTENT_TYPE 之外，请求中的任何 HTTP 首部转换为 META 的键时，
    都会将所有字母大写并将连接符替换为下划线最后加上 HTTP_  前缀。
    所以，一个叫做 X-Bender 的头部将转换成 META 中的 HTTP_X_BENDER 键。

8.HttpRequest.FILES
　　一个类似于字典的对象，包含所有的上传文件信息。
   FILES 中的每个键为<input type="file" name="" /> 中的name，值则为对应的数据。
　　注意，FILES 只有在请求的方法为POST 且提交的<form> 带有enctype="multipart/form-data" 的情况下才会
   包含数据。否则，FILES 将为一个空的类似于字典的对象。

9.HttpRequest.COOKIES
　　一个标准的Python 字典，包含所有的cookie。键和值都为字符串。

10.HttpRequest.session
 　　一个既可读又可写的类似于字典的对象，表示当前的会话。只有当Django 启用会话的支持时才可用。
    完整的细节参见会话的文档。

11.HttpRequest.user(用户认证组件下使用)
　　一个 AUTH_USER_MODEL 类型的对象，表示当前登录的用户。
　　如果用户当前没有登录，user 将设置为 django.contrib.auth.models.AnonymousUser 的一个实例。你可以通过 is_authenticated() 区分它们。

    例如：
    if request.user.is_authenticated():
        # Do something for logged-in users.
    else:
        # Do something for anonymous users.
     　　user 只有当Django 启用 AuthenticationMiddleware 中间件时才可用。
     -------------------------------------------------------------------------------------
    匿名用户
    class models.AnonymousUser
    django.contrib.auth.models.AnonymousUser 类实现了django.contrib.auth.models.User 接口，但具有下面几个不同点：
    id 永远为None。
    username 永远为空字符串。
    get_username() 永远返回空字符串。
    is_staff 和 is_superuser 永远为False。
    is_active 永远为 False。
    groups 和 user_permissions 永远为空。
    is_anonymous() 返回True 而不是False。
    is_authenticated() 返回False 而不是True。
    set_password()、check_password()、save() 和delete() 引发 NotImplementedError。
    New in Django 1.8:
    新增 AnonymousUser.get_username() 以更好地模拟 django.contrib.auth.models.User。

*/
```

request常用方法

```py
/*
1.HttpRequest.get_full_path()
　　返回 path，如果可以将加上查询字符串。
　　例如："/music/bands/the_beatles/?print=true"
2.HttpRequest.is_ajax()
　　如果请求是通过XMLHttpRequest 发起的，则返回True，方法是检查 HTTP_X_REQUESTED_WITH 相应的首部是否是字符串'XMLHttpRequest'。
　　大部分现代的 JavaScript 库都会发送这个头部。如果你编写自己的 XMLHttpRequest 调用（在浏览器端），你必须手工设置这个值来让 is_ajax() 可以工作。
　　如果一个响应需要根据请求是否是通过AJAX 发起的，并且你正在使用某种形式的缓存例如Django 的 cache middleware，
   你应该使用 vary_on_headers('HTTP_X_REQUESTED_WITH') 装饰你的视图以让响应能够正确地缓存。
*/
```

### 5.3 HttpResponse对象
响应对象主要有三种形式：  
1. HttpResponse()  
2. render()  
3. redirect()  
HttpResponse()括号内直接跟一个具体的字符串作为响应体，比较直接很简单，所以这里主要介绍后面两种形式。  
render()  

```py
render(request, template_name[, context]）
 结合一个给定的模板和一个给定的上下文字典，并返回一个渲染后的 HttpResponse 对象。
```

参数：

request： 用于生成响应的请求对象。  
template_name：要使用的模板的完整名称，可选的参数  
context：添加到模板上下文的一个字典。默认是一个空字典。如果字典中的某个值是可调用的，视图将在渲染模板之前调用它。  
render方法就是将一个模板页面中的模板语法进行渲染，最终渲染成一个html页面作为响应体。  

redirect()

传递要重定向的一个硬编码的URL

```py
def my_view(request):
    ...
    return redirect('/some/url/')
```

也可以是一个完整的URL：

```py
def my_view(request):
    ...
    return redirect('http://example.com/')　
```

key：两次请求　

```py
1）301和302的区别。
　　301和302状态码都表示重定向，就是说浏览器在拿到服务器返回的这个状态码后会自动跳转到一个新的URL地址，这个地址可以从响应的Location首部中获取
  （用户看到的效果就是他输入的地址A瞬间变成了另一个地址B）——这是它们的共同点。
　　他们的不同在于。301表示旧地址A的资源已经被永久地移除了（这个资源不可访问了），搜索引擎在抓取新内容的同时也将旧的网址交换为重定向之后的网址；
　　302表示旧地址A的资源还在（仍然可以访问），这个重定向只是临时地从旧地址A跳转到地址B，搜索引擎会抓取新的内容而保存旧的网址。 SEO302好于301
2）重定向原因：
（1）网站调整（如改变网页目录结构）；
（2）网页被移到一个新地址；
（3）网页扩展名改变(如应用需要把.php改成.Html或.shtml)。
        这种情况下，如果不做重定向，则用户收藏夹或搜索引擎数据库中旧地址只能让访问客户得到一个404页面错误信息，访问流量白白丧失；再者某些注册了多个域名的
    网站，也需要通过重定向让访问这些域名的用户自动跳转到主站点等。
```

用redirect可以解释APPEND_SLASH的用法！
