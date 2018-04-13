## jquery的事件

### 事件的概念

HTML中与javascript交互是通过事件驱动来实现的，例如鼠标点击事件、页面的滚动事件onscroll等等，可以向文档或者文档中的元素添加事件侦听器来预订事件。想要知道这些事件是在什么时候进行调用的，就需要了解一下“事件流”的概念

### 什么是事件流

事件流描述的是从页面中接收事件的顺序

1、DOM事件流

“DOM2级事件”规定的事件流包括三个阶段：

① 事件捕获阶段；

② 处于目标阶段；

③ 事件冒泡阶段

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件流</title>
    <script>

    window.onload = function(){

        var oBtn = document.getElementById('btn');

        oBtn.addEventListener('click',function(){
            console.log('btn处于事件捕获阶段');
        }, true);
        oBtn.addEventListener('click',function(){
            console.log('btn处于事件冒泡阶段');
        }, false);

        document.addEventListener('click',function(){
            console.log('document处于事件捕获阶段');
        }, true);
        document.addEventListener('click',function(){
            console.log('document处于事件冒泡阶段');
        }, false);

        document.documentElement.addEventListener('click',function(){
            console.log('html处于事件捕获阶段');
        }, true);
        document.documentElement.addEventListener('click',function(){
            console.log('html处于事件冒泡阶段');
        }, false);

        document.body.addEventListener('click',function(){
            console.log('body处于事件捕获阶段');
        }, true);
        document.body.addEventListener('click',function(){
            console.log('body处于事件冒泡阶段');
        }, false);

    };

    </script>
</head>
<body>
    <a href="javascript:;" id="btn">按钮</a>
</body>
</html>
```

当我们点击这个btn的时候，看看页面都输出了什么：

![](/jquery/事件流.jpg)

在解释输出结果为什么是这样之前，还有几个知识点需要了解一下即可：

**1、addEventListene**r

addEventListener 是DOM2 级事件新增的指定事件处理程序的操作，这个方法接收3个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是true，表示在捕获阶段调用事件处理程序；如果是false，表示在冒泡阶段调用事件处理程序。

**2、document、documentElement和document.body三者之间的关系：**

document代表的是整个html页面；

document.documentElement代表的是`<html>`标签；

document.body代表的是`<body>`标签；

接着我们就来聊聊上面的例子中输出的结果为什么是这样：

在标准的“DOM2级事件”中规定，事件流首先是经过事件捕获阶段，接着是处于目标阶段，最后是事件冒泡阶段。这里可以画个图示意一下:

![](/jquery/事件流.png)

首先在事件捕获过程中，document对象首先接收到click事件，然后事件沿着DOM树依次向下，一直传播到事件的实际目标，就是id为btn的a标签。

接着在事件冒泡过程中，事件开始时由最具体的元素（a标签）接收，然后逐级向上传播到较为不具体的节点（document）。

**需要注意的点**：由于老版本的浏览器不支持事件捕获，因此在实际开发中需要使用事件冒泡，在由特殊需要时再使用事件捕获。

**补充：**

1、IE中的事件流只支持“事件冒泡”，但是版本到了IE9+以后，实现了“DOM2级事件”，也就是说IE9+以后也可以在捕获阶段对元素进行相应的操作。

2、在DOM事件流中，实际的目标在“捕获阶段”不会接收到事件。而是在“处于目标阶段”被触发，并在事件处理中被看成“冒泡阶段”的一部分。然后，“冒泡阶段”发生，事件又传播回文档。

### jquery的常用事件

jquery常用的事件，大家一定要熟记在心。


![](/jquery/jquery事件.png)



