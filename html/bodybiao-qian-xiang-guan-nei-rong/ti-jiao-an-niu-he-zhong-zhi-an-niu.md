## 按钮

### 提交按钮和重置按钮
我们在`form`表单里面的各项数据填写完以后，通常会点击一个提交按钮来提交我们的数据，在HTML中使用`submit`按钮来触发提交数据。

语法：
`<input type="submit" value="提交">`

属性详解：
1. 只有当type属性为submit时才会提交数据。
2. value的属性值是显示在页面按钮上的文字。

举个例子：

```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>提交按钮</title>
</head>
<body>
<form action="" method="post">
    <p>用户名：<input type="text" name="username"></p>
    
    <p>密码：<input type="password" name="password"></p>

    <p>性别：</p>
    <p>
        <input type="radio" value="1" name="gender" checked="checked"/>男
        <input type="radio" value="2" name="gender" />女
    </p>
    <p>居住地：</p>
    <p>
        <select name="city">
            <option value="010">北京</option>
            <option value="021">上海</option>
            <option value="020">广州</option>
            <option value="023">重庆</option>
        </select>
    </p>
    <p>
        <input type="submit" value="提交">
    </p>
</form>
</body>
</html>
```

除了提交按钮，还有重置按钮。重置按钮可以将form表单里面的输入框都设置为初识状态。

重置按钮语法：`<input type="reset" value="重置">`

浏览器中显示的效果：

![提交按钮和重置按钮效果](/assets/chapter9/html/HTML_24.png)

### 普通的按钮

HTML中还有一个没有默认点击效果的按钮：`<input type="button" value="按钮">`，通常用于使用JavaScript来绑定点击事件。