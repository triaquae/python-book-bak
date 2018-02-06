## HTML文档结构

这一节课我们来学习HTML文件的结构：一个HTML文件是有自己固定结构的。

```html
<!DOCTYPE HTML>
<html>
    <head>...</head>
    <body>...</body>
</html>
```
![HTML结构](/assets/chapter9/imgs/html/HTML_02.png)
让我们来解释一下上面的代码：

首先，`<!DOCTYPE HTML>`是文档声明，必须写在HTML文档的第一行，位于`<html>`标签之前，表明该文档是HTML5文档。
1. `<html></html>` 称为根标签，所有的网页标签都在`<html></html>`中。
2. `<head></head>` 标签用于定义文档的头部，它是所有头部元素的容器。常见的头部元素有`<title>`、`<script>`、`<style>`、`<link>`和`<meta>`等标签，头部标签在下一节中会有详细介绍。
3. 在`<body>`和`</body>`标签之间的内容是网页的主要内容，如`<h1>`、`<p>`、`<a>`、`<img>`等网页内容标签，在`<body>`标签中的内容（图中淡绿色部分内容）最终会在浏览器中显示出来。