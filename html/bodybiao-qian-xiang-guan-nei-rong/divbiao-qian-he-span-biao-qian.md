## div标签和span标签

我们上面学过的标签都有自己的特点，但是div和span标签就没有任何特殊的样式。`<div>`标签用来表示一块内容（一行或多行），它多用来处理页面布局，我们的网页可以划分成很多不同的区域，这些区域可以使用 `<div>` 标签来分割。
而`<span>`标签通常在给一部分文档内容单独设置样式时使用。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <div>
            <h3>路飞学城</h3>
            <p>帮助有志向的年轻人通过<span>努力</span>学习获得<span>体面</span>的工作和生活。</p>
        </div>
        <div>
            <img src="https://hcdn1.luffycity.com/static/frontend/index/index_banner_1513933077.167929.png" alt="路飞学城" title="路飞学城" width="800" height="
            400">
        </div>
    </body>
</html>
```
效果如图：

![div和span标签](/assets/chapter9/html/HTML_17.png)