## 什么是AJAX

AJAX = 异步的javascript和XML（Asynchronous Javascript and XML）

简言之，在不重载整个网页的情况下，AJAX通过后台加载数据，并在网页上进行显示。

通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON - 同时您能够把这些外部数据直接载入网页的被选元素中。

**1.jQuery的load()方法**

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
  $.getJSON("./data/getJSON.json", function (data) {
       var str = "";//初始化保存内容变量
       $.each(data, function(index,ele) {
          $('ul').append("<li>"+ele.name+"</li>")
                    	
          });
       })


```

**3.jquery的$.get()方法**


$.get() 方法通过 HTTP GET 请求从服务器上请求数据

语法:$.get(URL,callback);

```
url参数规定你请求的路径，是必需参数，callback参数为数据请求成功后执行的函数
```

```javascript
 
                $.get('./data/getJSON.json',function(data,status){
    console.log(status);   //success    200状态码 ok的意思          	
})
```

**4.jquery的post()方法**

与get()方法相比，post()方法多用于以POST方式向服务器发送数据，服务器接收到数据之后，进行处理，并将处理结果返回页面

语法：$.post(URL,data,callback);

```
url参数规定你请求的路径，是必需参数，可选的data参数是连同请求发送的数据。可选的callback参数为数据请求成功后执行的函数
```

```javascript
 $.post('/index',{name:'张三'},function(data,status){
      console.log(status);
                	
 })
```

**5. jquery的$.ajax()方法**

```
jquery的$.ajax()方法 是做ajax技术经常使用的一个方法。

它的参数很多，总会有一些初学者记不住，在这里，演示几个经常使用的参数。后面讲django课程的时候老师会详细讲ajax技术的原理。大家先把每个参数做个笔记。
```
参数如下：
**1.url:** 
要求为String类型的参数，（默认为当前页地址）发送请求的地址。

**2.type: **
要求为String类型的参数，请求方式（post或get）默认为get。注意其他http请求方法，例如put和delete也可以使用，但仅部分浏览器支持。

3.timeout: 
要求为Number类型的参数，设置请求超时时间（毫秒）。此设置将覆盖$.ajaxSetup()方法的全局设置。

4.async: 
要求为Boolean类型的参数，默认设置为true，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为false。注意，同步请求将锁住浏览器，用户其他操作必须等待请求完成才可以执行。

5.cache: 
要求为Boolean类型的参数，默认为true（当dataType为script时，默认为false），设置为false将不会从浏览器缓存中加载请求信息。

**6.data:** 
要求为Object或String类型的参数，发送到服务器的数据。如果已经不是字符串，将自动转换为字符串格式。get请求中将附加在url后。防止这种自动转换，可以查看　　processData选项。对象必须为key/value格式，例如{foo1:"bar1",foo2:"bar2"}转换为&foo1=bar1&foo2=bar2。如果是数组，JQuery将自动为不同值对应同一个名称。例如{foo:["bar1","bar2"]}转换为&foo=bar1&foo=bar2。

7.dataType: 
要求为String类型的参数，预期服务器返回的数据类型。如果不指定，JQuery将自动根据http包mime信息返回responseXML或responseText，并作为回调函数参数传递。可用的类型如下：
xml：返回XML文档，可用JQuery处理。
html：返回纯文本HTML信息；包含的script标签会在插入DOM时执行。
script：返回纯文本JavaScript代码。不会自动缓存结果。除非设置了cache参数。注意在远程请求时（不在同一个域下），所有post请求都将转为get请求。
json：返回JSON数据。
jsonp：JSONP格式。使用SONP形式调用函数时，例如myurl?callback=?，JQuery将自动替换后一个“?”为正确的函数名，以执行回调函数。
text：返回纯文本字符串。

8.beforeSend：
要求为Function类型的参数，发送请求前可以修改XMLHttpRequest对象的函数，例如添加自定义HTTP头。在beforeSend中如果返回false可以取消本次ajax请求。XMLHttpRequest对象是惟一的参数。
            function(XMLHttpRequest){
               this;   //调用本次ajax请求时传递的options参数
            }
9.complete：

要求为Function类型的参数，请求完成后调用的回调函数（请求成功或失败时均调用）。参数：XMLHttpRequest对象和一个描述成功请求类型的字符串。
          function(XMLHttpRequest, textStatus){
             this;    //调用本次ajax请求时传递的options参数
          }

**10.success**：

要求为Function类型的参数，请求成功后调用的回调函数，有两个参数。
         (1)由服务器返回，并根据dataType参数进行处理后的数据。
         (2)描述状态的字符串。
         function(data, textStatus){
            //data可能是xmlDoc、jsonObj、html、text等等
            this;  //调用本次ajax请求时传递的options参数
         }

**11.error:**
要求为Function类型的参数，请求失败时被调用的函数。该函数有3个参数，即XMLHttpRequest对象、错误信息、捕获的错误对象(可选)。ajax事件函数如下：
       function(XMLHttpRequest, textStatus, errorThrown){
          //通常情况下textStatus和errorThrown只有其中一个包含信息
          this;   //调用本次ajax请求时传递的options参数
       }

12.contentType：
要求为String类型的参数，当发送信息至服务器时，内容编码类型默认为"application/x-www-form-urlencoded"。该默认值适合大多数应用场合。

13.dataFilter：
要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。提供data和type两个参数。data是Ajax返回的原始数据，type是调用jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处理。
            function(data, type){
                //返回处理后的数据
                return data;
            }

14.dataFilter：
要求为Function类型的参数，给Ajax返回的原始数据进行预处理的函数。提供data和type两个参数。data是Ajax返回的原始数据，type是调用jQuery.ajax时提供的dataType参数。函数返回的值将由jQuery进一步处理。
            function(data, type){
                //返回处理后的数据
                return data;
            }

15.global：
要求为Boolean类型的参数，默认为true。表示是否触发全局ajax事件。设置为false将不会触发全局ajax事件，ajaxStart或ajaxStop可用于控制各种ajax事件。

16.ifModified：
要求为Boolean类型的参数，默认为false。仅在服务器数据改变时获取新数据。服务器数据改变判断的依据是Last-Modified头信息。默认值是false，即忽略头信息。

17.jsonp：
要求为String类型的参数，在一个jsonp请求中重写回调函数的名字。该值用来替代在"callback=?"这种GET或POST请求中URL参数里的"callback"部分，例如{jsonp:'onJsonPLoad'}会导致将"onJsonPLoad=?"传给服务器。

18.username：
要求为String类型的参数，用于响应HTTP访问认证请求的用户名。

19.password：
要求为String类型的参数，用于响应HTTP访问认证请求的密码。

20.processData：
要求为Boolean类型的参数，默认为true。默认情况下，发送的数据将被转换为对象（从技术角度来讲并非字符串）以配合默认内容类型"application/x-www-form-urlencoded"。如果要发送DOM树信息或者其他不希望转换的信息，请设置为false。

21.scriptCharset：
要求为String类型的参数，只有当请求时dataType为"jsonp"或者"script"，并且type是GET时才会用于强制修改字符集(charset)。通常在本地和远程的内容编码不同时使用


```javascript

 //get()方式
  $.ajax({
     url:'./data/index.txt',
     type:'get',
     dataType:'text',
     success:function(data){
        $('p').html(data);
               		
     },
     error:function(error){
        console.log(error)
     }
```

```javascript

//post()方式
$.ajax({
   url:'/index',
   type:'post',
   data:{name:'张三',age:12},
   success:function(data){
      $('p').html(data);
   },
   error:function(error){
      console.log(error)
}
```

```
注意：以上所有操作,请在服务器上运行此代码，如果没有服务器，可以在本地搭建本地服务器。
好吧！！咱们还没学，我们可以使用PCCharm,WebStrom,HBuilder上运行此代码。但是post请求的方法 我们暂时没法演示，
后面在django部分讲到服务器的老师，会给大家详细演示get请求和post请求的处理。
```