### 多行文本标签
当用户需要在表单中输入大段文字时，就需要用到多行文本输入框`<textarea>`了。
语法：
`<textarea  rows="行数" cols="列数">文本</textarea>`
解释：
1. `<textarea>`标签是成对出现的，以`<textarea>`开始，以`</textarea>`结束。
2. cols：textarea一行最多能容纳的字符数。
3. rows：textarea最多能容纳的行数。
4. 在`<textarea></textarea>`标签之间可以输入默认值。

举个例子：
```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html;charset=utf-8">
<title>textarea标签</title>
</head>
<body>
<form action="save.php" method="post" >
    <label>个人简介：</label>
    <textarea cols="50" rows="10">姓甚名谁来自哪里...</textarea>
</form> 
</body>
</html>
```
看一下在浏览器中的效果：
![文本域效果](/assets/chapter9/html/HTML_21.png)