## 文本样式标签

文本样式标签主要用来对HTML页面中的文本进行修饰，比如加粗、斜体、线条样式等...

1. `<b></b>`：加粗
2. `<i></i>`：斜体
3. `<u></u>`：下划线
4. `<s></s>`：删除线
5. `<sup></sup>`：上标 
6. `<sub></sub>`：下标

举个例子：

```html
<!DOCTYPE HTML>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>文本格式标签</title>
</head>
<body>
    路飞学城
    <b>路飞学城</b>
    <i>路飞学城</i>
    <u>路飞学城</u>
    <s>路飞学城</s>
    <sup>路飞学城</sup>
    <sub>路飞学城</sub>    
</body>
</html>
```
将上面的代码保存成html文件，然后用浏览器打开看一下实际的显示效果：

![文本样式标签效果](/assets/chapter9/html/HTML_26.png)

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

![强调标签效果](/assets/chapter9/html/HTML_27.png)

### 表示引用的标签

`<blockquote>`通常用来展示大段的文本引用。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <p>作为一家互联网创业公司，路飞学城是由老男孩教育携手一众信任老男孩的学员众筹发起的在线教育项目。我们怀揣着帮助有志向的年轻人通过努力学习获得体面工作与品质生活的使命，坚守初心，砥砺前行。</p>
        <blockquote>
            作为一家互联网创业公司，路飞学城是由老男孩教育携手一众信任老男孩的学员众筹发起的在线教育项目。我们怀揣着帮助有志向的年轻人通过努力学习获得体面工作与品质生活的使命，坚守初心，砥砺前行。
        </blockquote>
    </body>
</html>
```

![引用标签效果](/assets/chapter9/html/HTML_11.png)

从上图中可以看出和普通的`<p>`标签相比，`<blockquote>`标签中的内容会有首尾缩进的效果。

### 表示代码的标签

表示简短的单行代码可以使用`<code>`标签，如果是带有缩进的大段代码就要使用`<pre>`标签了。`<pre>`标签会保留源文档中的格式(回车、空格)。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <p>单行代码：</p>
        <code>
            print("Hello world!")
        </code>
        <p>代码块：</p>
        <pre>
            while True:
            age = input("猜猜看啊:").strip()
            try:
                age = int(age)
                if age > 100 or age < 100:
                    print("不对!")
                else:
                    print("对了!")
                    break
            except ValueError:
                print("别捣乱!")            
        </pre>
    </body>
</html>
```
我们来看一下页面的效果：

![代码标签的效果](/assets/chapter9/html/HTML_12.png)

### 表示地址的标签

在网页上经常会有公司的联系地址信息，这个时候就需要用到`<address>`标签了。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <p>路飞学城地址：</p>
        <address>
            北京市昌平区顺沙路八号院汇德商厦402
        </address>
    </body>
</html>
```
看一下效果：

![地址标签效果](/assets/chapter9/html/HTML_13.png)

