### 单选框和多选框

有时候像性别这样的数据并不需要用户自己来填写具体的值，只需要我们事先定义好选项让用户来选择就可以了。类似这样的数据我们都可以在我们的页面上用单选框或多选框来展示：

单选框语法：
name设置相同的属性值，以实现互斥选区
`<input type="radio" value="值" name="名称" checked="checked"/>`
多选框语法：
`<input type="checkbox" value="值" name="名称" checked="checked"/>`

属性解释：
1. value：提交到服务器的值
2. name：为选择框命名，往后端提交数据时使用。
3. checked：当设置checked="checked"时，该选项会默认被选中

举个例子：

```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>单选框和复选框</title>
</head>
<body>
<form action="" method="post">
    <p>我的性别：</p>
    
    <p>
        <input type="radio" value="1" name="gender" checked="checked"/>男
        <input type="radio" value="2" name="gender" />女
    </p>
    <p>我的标签：</p>
    <p>
        <input type="checkbox" value="1" name="tag" checked="checked">高
        <input type="checkbox" value="2" name="tag">富
        <input type="checkbox" value="3" name="tag" checked="checked">帅
    </p>
</form>
</body>
</html>
```
将上面的代码保存后使用浏览器打开，可以看到如下的效果：

![单选框和多选框效果](/assets/chapter9/html/HTML_22.png)