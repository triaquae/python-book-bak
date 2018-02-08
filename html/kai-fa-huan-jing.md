## 开发环境

市面上有很多的HTML编辑器可以选择，常见的Notepad++和Sublime Text都可以用来开发HTML。
当然PyCharm也支持HTML开发。


HTML文件的后缀名常见的是`.html`，当然一些老旧的网站可能还使用`.htm`。
我们以后都使用`.html`作为HTML文件的后缀名。

一个简单的例子：

打开你的编辑器新建一个文件，把下面的文本内容，复制粘贴到你新建的文件中，然后另存为名为`helloworld.html`的文件。再使用浏览器打开刚才保存的文件就可以看到效果了。

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>路飞学城(luffycity.com)</title>
</head>
<body>
    <h1>Hello world.</h1>
    <p>我的第一个HTML文件。</p>
</body>
</html>
```

> 注意：对于中文网页需要使用`<meta charset="utf-8">`来声明网页的编码，否则会出现乱码。如果需要设置浏览器的编码为GBK，则需要设置为`<meta charset="gbk">`。

怎么样，你现在已经完成了一个属于自己的第一个HTML页面了。