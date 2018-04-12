## 什么是AJAX

AJAX = 异步的javascript和XML（Asynchronous Javascript and XML）

简言之，在不重载整个网页的情况下，AJAX通过后台加载数据，并在网页上进行显示。

通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON - 同时您能够把这些外部数据直接载入网页的被选元素中。

**1.jQuery的load()方法
**
jQuery load()方法是简单但强大的AJAX方法。

load()方法从服务器加载数据，并把返回的数据放入被选元素中。

**语法：**
```javascript
$("selector").load(url,data,callback);
```

```
必须的url参数规定记载的url地址
可选的data参数规定与请求一同发送的查询字符串键/值对的集合
可选的callback参数是load()方法完成后所执行的函数名称
```

```javascript
    

```
