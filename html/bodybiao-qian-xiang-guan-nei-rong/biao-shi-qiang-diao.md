### 表示强调的标签

我们已经学习了展示段落的p标签和展示标题的h1~h6标签，现在如果想在一段文字中特别强调某几个字，这时候就可以用到`<em>`或`<strong>`标签。

这两个标签都是表示强调，但是两者在强调的语气上有区别:`<em>`表示强调，`<strong>`表示更强烈的强调。
在浏览器中`<em>`默认会用斜体表示，`<strong>`会用粗体来表示。两个标签相比，我们通常会推荐大家使用`<strong>`表示强调。

例如：电商网站的折扣数字，通常都使用`<strong>`标签来表示强烈的强调。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <p>路飞学城</p>
        <em>强调</em>
        <strong>更强烈的强调</strong>
    </body>
</html>
```

查看一下效果：

![强调标签效果](/assets/chapter9/html/HTML_09.png)