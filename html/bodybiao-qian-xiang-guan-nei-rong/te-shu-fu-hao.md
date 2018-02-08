浏览器在显示的时候会移除源代码中多余的空格和空行。
所有连续的空格或空行都会被算作一个空格。需要注意的是，HTML代码中的所有连续的空行（换行）也被显示为一个空格。

举个例子：
```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>

        <p>帮助有志向的年轻人
            
            
            通过努力学习获得
            体面的   工作    和    生活！</p>
    </body>
</html>
```
上面的代码在浏览器中最终的显示效果：

![连续空行空格效果](/assets/chapter9/html/HTML_09.png)

### 特殊字符
在上一个实例中，我们演示了HTML中输入空格、回车都是没有作用的。要想输入空格，需要用特殊符号 -- `&nbsp;`。

常用的特殊字符：

| 内容       | 对应代码   |
| :-------: | :--------:|
| 空格       | &nbsp;    |
| >         | &gt;      |
| <         | &lt;      |
| &         | &amp;     |
| ¥         | &yen;     |
| 版权       | &copy;    |
| 注册        | &reg;     |

[HTML特殊符号对照表](http://tool.chinaz.com/Tools/HtmlChar.aspx)
