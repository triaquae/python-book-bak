### 图片标签

一个网页除了有文字，还会有图片。我们使用`<img/>`标签在网页中插入图片。

语法：`<img src="图片地址" alt="图片加载失败时显示的内容" title = "提示信息" />`

注意：
1. src设置的图片地址可以是本地的地址也可以是一个网络地址。
2. 图片的格式可以是png、jpg和gif。
3. alt属性的值会在图片加载失败时显示在网页上。
4. 还可以为图片设置宽度(width)和高度(height)，不设置就显示图片默认的宽度和高度。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <img src="https://hcdn1.luffycity.com/static/frontend/index/index_banner_1513933077.167929.png" alt="路飞学城" title="路飞学城" width="800" height="
        400">
    </body>
</html>
```

效果如图：

![img标签效果](/assets/chapter9/html/HTML_16.png)