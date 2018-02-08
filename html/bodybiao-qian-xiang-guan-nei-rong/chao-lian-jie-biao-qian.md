### 超链接标签
网页上可以设置超链接，允许用户通过点击的操作完成页面的跳转。
HTML中使用a标签来做超链接。语法是：`<a href="目标网址" title="鼠标滑过显示的提示文本">链接显示的文本内容</a>`

我们可以创建一个页面，使用一个a标签链接到路飞学城的官网：

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <a href="http://www.luffycity.com">路飞学城</a>
    </body>
</html>
```

使用浏览器打开上面的页面，点击页面中的路飞学城文字，浏览器就会跳转到路飞学城的官网了。

![a标签效果](/assets/chapter9/html/HTML_15.png)

注意：如果想让跳转的网页在浏览器的新标签页打开，只需要给a标签设置一个target参数即可：
`<a href="http://www.luffycity.com" target="_blank">路飞学城</a>`

链接其他表现形式：
1. 目标文档为下载资源
  例如：href属性值，指定的文件名称，就是下载操作(rar、zip等)
2. 电子邮件链接
  前提：计算机中必须安装邮件客户端，并且配置好了邮件相关信息。
  例如：`<a href="mailto:zhaoxu@tedu.cn">联系我们</a>`
3. 返回页面顶部的空链接或具体id值的标签
  例如：`<a href="#">内容</a>`或`<a href="#id值">内容</a>`
4. 链接到Javascript
  例如：`<a href="javascript:">内容</a>`