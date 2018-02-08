### 下拉框和多选的下拉框

有时候如果备选的选项太多我们还会用到下拉的选择框来展示相关信息，比如我们经常遇到选择省市相关信息的时候就会用到下拉选择框，在HTML中用`select`标签来展示：

```html
<select name="">
    <option value="提交的值">显示的值</option>
</select>
```
属性介绍：

1. name：为选择框命名，往后端提交数据时使用。
2. select标签内部用`option`表示具体的选项，可以有多个。
3. select标签默认为单选，如果加上multiple属性就会变成多选

举个例子：

```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>下拉框和多选下拉框</title>
</head>
<body>
<form action="" method="post">
    <p>居住地：</p>
    <p>
        <select name="city">
            <option value="010">北京</option>
            <option value="021">上海</option>
            <option value="020">广州</option>
            <option value="023">重庆</option>
        </select>
    </p>
    <p>我的爱好（多选）：</p>
    <p>
        <select name="hobby" multiple>
            <option value="1">篮球</option>
            <option value="1">足球</option>
            <option value="1">排球</option>
            <option value="1">双色球</option>
        </select>
    </p>
</form>
</body>
</html>
```

看一下在页面上的效果：

![下拉框效果](/assets/chapter9/html/HTML_23.png)