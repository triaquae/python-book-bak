## head标签

我们首先来介绍一下`head`标签的主要内容和作用，文档的头部描述了文档的各种属性和信息，包括文档的标题、编码方式及URL等信息,这些信息大部分是用于提供索引,辩认或其他方面的应用（移动端）的等。
以下标签是可以用在`head`标签中的：

```html
<head lang='en'>
    <title>标题信息</title>
    <meta charset='utf-8'>
    <link>
    <style type='text/css'></style>
    <script type='text/javascript'></script>
</head>
```

### title标签

`<title>`标签：在`<title>`和`</title`>标签之间的文字内容是网页的标题信息，它会显示在浏览器标签页的标题栏中。可以把它看成是一个网页的标题。主要用来告诉用户和搜索引擎这个网页的主要内容是什么，搜索引擎可以通过网页标题，迅速的判断出当前网页的主题。

我们接下来做一个小练习，创建一个带有我们自定义标题内容的网页：

```html
<!DOCTYPE HTML>
<html>
    <head>
        <title>路飞学城</title>
    </head>
    <body></body>
</html>
```
将上面的文件另存为`demo.html`，然后用浏览器打开，就可以看到下面的内容。

![title标签效果展示](/assets/chapter9/html/HTML_03.png)

上面我们介绍了`title`标签的用法，接下来我们继续看一下`head`标签中可以使用的其他标签：

### meta标签

Meta标签介绍：

<meta>元素可提供有关页面的原信息（mata-information）,针对搜索引擎和更新频度的描述和关键词。
<meta>标签位于文档的头部，不包含任何内容。
<meta>提供的信息是用户不可见的。
meta标签的组成：meta标签共有两个属性，它们分别是http-equiv属性和name属性，不同的属性又有不同的参数值，这些不同的参数值就实现了不同的网页功能。 

常用的meta标签：

1. http-equiv属性

它用来向浏览器传达一些有用的信息，帮助浏览器正确地显示网页内容，与之对应的属性值为content，content中的内容其实就是各个参数的变量值。

```html
<!--重定向 2秒后跳转到对应的网址，注意分号-->
<meta http-equiv="refresh" content="2;URL=http://www.luffycity.com">
<!--指定文档的内容类型和编码类型 -->
<meta http-equiv="Content-Type" content="text/html;charset=utf-8" />
<!--告诉IE浏览器以最高级模式渲染当前网页-->
<meta http-equiv="x-ua-compatible" content="IE=edge">
```

2. name属性

主要用于页面的关键字和描述，是写给搜索引擎看的，关键字可以有多个用 ‘,’号隔开，与之对应的属性值为content，content中的内容主要是便于搜索引擎机器人查找信息和分类信息用的。

```html
<meta name="keywords" content="meta总结,html meta,meta属性,meta跳转">
<meta name="description" content="路飞学城">
```

### 其他标签

```html
<!--标题-->
<title>路飞学城</title>
<!--icon图标（网站的图标）-->
<link rel="icon" href="fav.ico">
<!--定义内部样式表-->
<style></style>
<!--引入外部样式表文件-->
<link rel="stylesheet" href="mystyle.css">
<!--定义JavaScript代码或引入JavaScript文件-->
<script src="myscript.js"></script>
```