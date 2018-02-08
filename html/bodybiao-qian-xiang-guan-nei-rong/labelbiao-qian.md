### label标签

label标签不会在页面上任何特殊效果，它的作用主要是方便用户。如果你点击了`label`标签的文本，浏览器就会自动将焦点转到和标签相关的表单控件上（就自动选中和该label标签相关连的表单控件上）。通常我们都会为`form`表单中的输入控件搭配`label`标签。

我们把上面的例子在完善一下：

```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>搭配label标签的输入控件</title>
</head>
<body>
<form action="" method="post">
    <p>
        <label for="username">用户名：</label>
        <input type="text" name="username" id="username">
    </p>
    <p>
        <label for="password">密码：</label>
        <input type="password" name="password" id="password">
    </p>
    <p>性别：</p>
    <p>
        <label for="male">男</label>
        <input type="radio" value="1" name="gender" checked="checked" id="male"/>
        <label for="female">女</label>
        <input type="radio" value="2" name="gender" id="female"/>
    </p>
    <p>
        <label for="city">现居：</label>
        <select name="city" id="city">
            <option value="010">北京</option>
            <option value="021">上海</option>
            <option value="020">广州</option>
            <option value="023">重庆</option>
        </select>
    </p>
    <p>
        <input type="submit" value="提交">
        <input type="reset" value="重置">
    </p>
</form>
</body>
</html>
```

完善版form表单示例效果：
![form表单效果](/assets/chapter9/html/HTML_25.png)