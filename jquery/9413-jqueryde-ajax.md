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

1、
$('#btn').click(function(){

    //只传一个url，表示在id为#new-projects的元素里加载index.html
    $('#new-projects').load('./index.html');
})

```

```javascript
2、
$('#btn').click(function(){
    //只传一个url，导入的index.html文件含有多个传递参数，类似于：index/html?name='张三'
    $('#new-projects').load('./index.html',{"name":'张三',"age":12});
})

```
```javascript
3、
    //加载文件之后，会有个回调函数，表示加载成功的函数
    $('#new-projects').load('./index.html',{"name":'张三',"age":12},function(){
    
});
```
```
注意：load函数最好在服务器网页中应用，也就是说要在服务器上运行，本地调试需要搭建后端本地环境。
```

**2. jquery的getJSON方法**

jQuery的AJAX中使用getJSON()方法异步加载JSON格式数据。获取服务器中的数据，并对数据进行解析，显示到页面中


语法: $.getJSON(url,[data],[callback])

```
url参数为请求加载json格式文件的服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后执行的函数
```


```javascript


```