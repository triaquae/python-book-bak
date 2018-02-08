## input标签

当用户要在表单中输入简单的字母、数字等单行内容时，就会用到input标签。

语法：
`<input type="text" name="名称" value="值">`
解释：
1. type：可以有多个值，常见的有text、password、email、file。
2. name：为文本框命名，往后端提交数据时使用。
3. value：为文本输入框设置默认值。(一般起到提示作用)

注意：
input标签的type根据应用场景的不同可以设置不同的值，常见的还有passsword（密码）、email（邮箱）以及file（文件）。
`<input type="password" name="名称" value="值">`用来让用户输入密码。
`<input type="email" name="名称" value="值">`用来让用户输入邮箱。
`<input type="email" name="名称" value="值">`用来让用户输入文件。

举个例子：

```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>输入框类型</title>
</head>
<body>
<form action="" method="post" enctype="multipart/form-data">
    <p>用户名：<input type="text"></p>
    <p>密码：<input type="password"></p>
    <p>邮箱：<input type="email"></p>
    <p>头像：<input type="file"></p>
</form>
</body>
</html>
```
看一下在浏览器中的效果：

![常用输入框效果](/assets/chapter9/html/HTML_20.png)

注意：

如果form表单中有type="file"类型的input标签时，需要在form标签上添加一个`enctype="multipart/form-data"`属性。