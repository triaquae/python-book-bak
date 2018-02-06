## body中常用标签

### 标题标签

标题标签一共有6个，h1、h2、h3、h4、h5、h6分别为一级标题、二级标题、三级标题、四级标题、五级标题、六级标题。`<h1>`是最高的等级。`<h6>`是最低的等级。
标题标签通常用来制作文章或网站的标题。

h1~h6标签的默认样式：

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <h1>一级标题</h1>
        <h2>二级标题</h2>
        <h3>三级标题</h3>
        <h4>四级标题</h4>
        <h5>五级标题</h5>
        <h6>六级标题</h6>
    </body>
</html>
```
将上面的代码复制粘贴到demo3.html文件中，用浏览器打开，看到效果如图：

![标题标签效果演示](/assets/chapter9/html/HTML_05.png)


### p标签

HTML页面中通过`<p></p>`来定义段落，通常大段的文字我们都会放在p标签中。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <title>路飞学城</title>
    </head>
    <body>
        <p>夜仿佛纸浸了油，变成半透明体，它给太阳拥抱住了，分不出身来，也许是给太阳陶醉了，所以夕阳晚霞隐褪后的夜色也带着酡红。</p>
        <p>忠厚老实人的恶毒，像饭里的沙砾或者出骨鱼片里未净的刺，给人一种不期待的伤痛。</p>
    </body>
</html>
```
我们将上面的代码保存在demo4.html文件中，使用浏览器打开看一下效果：

![段落效果展示](/assets/chapter9/html/HTML_06.png)

### hr标签

`<hr>`标签用来在HTML页面中创建水平线，通常用来分隔内容。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <p>夜仿佛纸浸了油，变成半透明体，它给太阳拥抱住了，分不出身来，也许是给太阳陶醉了，所以夕阳晚霞隐褪后的夜色也带着酡红。</p>
        <hr>
        <p>忠厚老实人的恶毒，像饭里的沙砾或者出骨鱼片里未净的刺，给人一种不期待的伤痛。</p>
    </body>
</html>
```

hr标签的效果如图：

![hr标签效果展示](/assets/chapter9/html/HTML_07.png)

### br标签

`<br>`标签用来将内容换行，其在HTML网页上的效果相当于我们平时使用word编辑文档时使用回车换行。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <p>夜仿佛纸浸了油，变成半透明体，它给太阳拥抱住了，分不出身来，也许是给太阳陶醉了，所以夕阳晚霞隐褪后的夜色也带着酡红。</p>
        <hr>
        <p>忠厚老实人的恶毒，<br>像饭里的沙砾或者出骨鱼片里未净的刺，<br>给人一种不期待的伤痛。</p>
    </body>
</html>
```
效果如图：

![br标签效果展示](/assets/chapter9/html/HTML_08.png)

**注意：**
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

表示简短的单行代码可以使用`<code>`标签，如果是带有缩进的大段代码就要使用`<pre>`标签了。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <code>
            print("Hello world!")
        </code>

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

### 列表标签

网站页面上一些列表相关的内容比如说物品列表、人名列表等等都可以使用列表标签来展示。

对于无序的列表，可以使用`<ul><li></li></ul>`标签，对于有序的列表，可以使用`<ol><li></li></ol>`标签：

注意：这里的无序指的是页面上的内容前面不会显示序号。
```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <p>有序列表</p>
        <ol>
            <li>Python基础</li>
            <li>前端开发基础</li>
            <li>Python Web开发</li>
        </ol>

        <p>无序列表</p>
        <ul>
            <li>前端开发是做什么的？</li>
            <li>我们为什么要学习前端开发？</li>
            <li>前端开发都需要掌握哪些内容？</li>
        </ul>
    </body>
</html>
```

效果如图：

![列表效果](/assets/chapter9/html/HTML_14.png)


### a标签
网页上可以设置超链接，链接到其他的网页。
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


### img标签

一个网页除了有文字，还会有图片。我们使用`<img/>`标签在网页中插入图片。

语法：`<img src="图片地址" alt="图片加载失败时显示的内容" title = "提示信息" />`

注意：
1. src设置的图片地址可以是本地的地址也可以是一个网络地址。
2. 图片的格式可以是png、jpg和gif。
3. alt属性的值会在图片加载失败时显示在网页上。
4. 还可以为图片设置宽度(width)和高度(height)，不设置就显示图片默认的宽度和高度。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <img src="https://hcdn1.luffycity.com/static/frontend/index/index_banner_1513933077.167929.png" alt="路飞学城" title="路飞学城" width="800" height="
        400">
    </body>
</html>
```

效果如图：

![img标签效果](/assets/chapter9/html/HTML_16.png)


### div标签和span标签

我们上面学过的标签都有自己的特点，但是div和span标签就没有任何特殊的样式。`<div>`标签用来表示一块内容（一行或多行），它多用来处理页面布局，我们的网页可以分成很多不同的区域，这些区域可以使用div标签来分割。
而`<span>`标签通常在给一部分文档内容单独设置样式时使用。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <div>
            <h3>路飞学城</h3>
            <p>帮助有志向的年轻人通过<span>努力</span>学习获得<span>体面</span>的工作和生活。</p>
        </div>
        <div>
            <img src="https://hcdn1.luffycity.com/static/frontend/index/index_banner_1513933077.167929.png" alt="路飞学城" title="路飞学城" width="800" height="
            400">
        </div>
    </body>
</html>
```
效果如图：

![div和span标签](/assets/chapter9/html/HTML_17.png)

### HTML表格

有些时候我们需要在页面上用表格展示一些数据，
如：

那如何在HTML页面上定义表格呢？

HTML中使用`table`标签来定义表格，通常`table`还会分为`thead`(表头)和`tbody`(表格内容)两部分。
你看表格中的数据都是分很多行，每一行又会有很多列。
在`thead`和`tbody`中都用`tr`表示一行，在`thead`中用`th`表示一列，用`tbody`中用`td`表示一列。

我们来动手自己写一个表格。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <table>
            <thead>
                <tr>
                    <th>#</th>
                    <th>名称</th>
                    <th>价格</th>
                    <th>库存</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>苹果</td>
                    <td>9.99</td>
                    <td>100</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>香蕉</td>
                    <td>11.99</td>
                    <td>80</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>芒果</td>
                    <td>14.99</td>
                    <td>160</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```
看一下效果：
![表格默认效果](/assets/chapter9/html/HTML_18.png)

这样的表格默认是不显示边框，我们可以通过为表格设置边框属性让表格显示边框。

在`table`标签中通过设置`border="1"`为表格设置一个宽度为1像素的边框：

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <table border="1">
            <thead>
                <tr>
                    <th>#</th>
                    <th>名称</th>
                    <th>价格</th>
                    <th>库存</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>苹果</td>
                    <td>9.99</td>
                    <td>100</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>香蕉</td>
                    <td>11.99</td>
                    <td>80</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>芒果</td>
                    <td>14.99</td>
                    <td>160</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```
设置了边框的表格效果：

![代表框的表格](/assets/chapter9/html/HTML_19.png)