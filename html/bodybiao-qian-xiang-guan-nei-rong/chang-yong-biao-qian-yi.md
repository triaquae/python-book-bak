## 标题标签 h1~h6

`<h1>` - `<h6>` 标签可定义标题。`<h1>` 定义最大的标题。`<h6>` 定义最小的标题。
由于 h 元素拥有确切的语义，因此请您慎重地选择恰当的标签层级来构建文档的结构。因此，请不要利用标题标签来改变同一行中的字体大小。相反，我们应当使用css来定义来达到漂亮的显示效果。
标题标签通常用来制作文章或网站的标题。

h1~h6标签的默认样式：

```html
<!DOCTYPE HTML>
<html>
    <head lang='en'>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <h1>一级标题</h1><h2>二级标题</h2>
        <h3>三级标题</h3>
        <h4>四级标题</h4>
        <h5>五级标题</h5>
        <h6>六级标题</h6>
    </body>
</html>
```

请看上面代码 `<h1>`和`<h2>`书写在一行上展示，但是在浏览器的效果却是换行了，大家现在预习一下9.1.9标签分类知识点。
```
文本样式标签主要用来对HTML页面中的文本进行修饰，比如加粗、斜体、线条样式等...

1. `<b></b>`：加粗
2. `<i></i>`：斜体
3. `<u></u>`：下划线
4. `<s></s>`：删除线
5. `<sup></sup>`：上标 
6. `<sub></sub>`：下标



现在如果想在一段文字中特别强调某几个字，这时候就可以用到`<em>`或`<strong>`标签。

这两个标签都是表示强调，但是两者在强调的语气上有区别:`<em>`表示强调，`<strong>`表示更强烈的强调。
在浏览器中`<em>`默认会用斜体表示，`<strong>`会用粗体来表示。两个标签相比，我们通常会推荐大家使用`<strong>`表示强调
```

## 段落标签 p
`<p>`,paragraph的简写。定义段落

```html
<body>
        <p>路飞学城立志帮助有志向的年轻人通过努力学习获得体面的工作和生活!路飞学员通过学习Python ,金融分析,人工智能等互联网最前沿技术,开启职业生涯新可能</p>
        <p>路飞学城立志帮助有志向的年轻人通过努力学习获得体面的工作和生活!路飞学员通过学习Python ,金融分析,人工智能等互联网最前沿技术,开启职业生涯新可能</p>

</body>
```
浏览器展示特点：
1. 跟普通文本一样，但我们可以通过css来设置当前段落的样式
2. 是否又独占一行呢？ 答案是的 块级元素


## 超链接标签 a
超级链接`<a>`标记代表一个链接点，是英文anchor（锚点）的简写。它的作用是把当前位置的文本或图片连接到其他的页面、文本或图像

```html
<body>
    <h1>
     
		<!-- a链接 超链接  
		target:_blank 在新的网站打开链接的资源地址
				_self 在当前网站打开链接的资源地址
		title: 鼠标悬停时显示的标题
		-->
		<a href="http://www.baidu.com" target="_blank" title="路飞学城">路飞学城</a>
		<a href="a.zip">下载包</a>
		<a href="mailto:zhaoxu@tedu.cn">联系我们</a>
		<!-- 返回页面顶部的内容 -->
		<a href="#">跳转到顶部</a>

		<!-- 返回某个id -->
		<a href="#p1">跳转到p1</a>
		<!-- javascript:是表示在触发<a>默认动作时，执行一段JavaScript代码，而 javascript:; 表示什么都不执行，这样点击<a>时就没有任何反应。 -->
		<a href="javascript:alert(1)">内容</a>
		<a href="javascript:;">内容</a>


	</h1>
</body>
```
target:_blank 在新的网站打开链接的资源地址
target：_self 在当前网站打开链接的资源地址
title: 表示鼠标悬停时显示的标题

链接其他表现形式：
1. 目标文档为下载资源
  例如：href属性值，指定的文件名称，就是下载操作(rar、zip等)
2. 电子邮件链接
  前提：计算机中必须安装邮件客户端，并且配置好了邮件相关信息。
  例如：`<a href="mailto:zhaoxu@tedu.cn">联系我们</a>`
3. 返回页面顶部的空链接或具体id值的标签
  例如：`<a href="#">内容</a>`或`<a href="#id值">内容</a>`
4. javascript:是表示在触发`<a>`默认动作时，执行一段JavaScript代码。
  例如：`<a href="javascript:alert()">内容</a>`
5. javascript:;表示什么都不执行，这样点击`<a>`时就没有任何反应
   例如：`<a href="javascrip:;">`内容</a



## 列表标签 ul，ol
网站页面上一些列表相关的内容比如说物品列表、人名列表等等都可以使用列表标签来展示。通常后面跟`<li>`标签一起用，每条li表示列表的内容

`<ul>`:unordered lists的缩写 无序列表
`<ol>`:ordered listsde的缩写 有序列表
```html

	<!-- 无序列表 type可以定义无序列表的样式-->
	<ul type="circle">
		<li>我的账户</li>
		<li>我的订单</li>
		<li>我的优惠券</li>
		<li>我的收藏</li>
		<li>退出</li>
	</ul>
	<!-- 有序列表 type可以定义有序列表的样式 -->
	<ol type="a">
		<li>我的账户</li>
		<li>我的订单</li>
		<li>我的优惠券</li>
		<li>我的收藏</li>
		<li>退出</li>
	</ol>

```

ol标签的属性：

type：列表标识的类型 
  - 1：数字
  - a：小写字母
  - A：大写字母
  - i：小写罗马字符
  - I：大写罗马字符

列表标识的起始编号
  - 默认为1

ul标签的属性：
type：列表标识的类型
  - disc：实心圆(默认值)
  - circle：空心圆
  - square：实心矩形
  - none：不显示标识
  
##  盒子标签 `div`
`<div>`可定义文档的分区 division的缩写 译：区
`<div>` 标签可以把文档分割为独立的、不同的部分,请看下面代码我们将他们进行分区
```html
<!DOCTYPE html>
<html>
<head lang="en">
	<meta charset="utf-8" >
	<title>常用标签一</title>
</head>
<body>
	<div id="wrap">
		<div class="para">
			<p style="height: 1000px" id="p1">段落</p>
		</div>
		
		<div class="anchor">
			我是普通的文本
			<h1>
				
				<a href="http://www.baidu.com" target="_blank" title="路飞学城">路飞学城</a>
				<a href="a.zip">下载包</a>
				<a href="mailto:zhaoxu@tedu.cn">联系我们</a>
				<a href="#">跳转到顶部</a>
				<a href="#p1">跳转到p1</a>
			
				<a href="javascript:alert(1)">内容</a>
				<a href="javascript:;">内容</a>
			</h1>
		</div>
		<!-- <h2>路飞学城</h2>
		<h3>路飞学城</h3>
		<h4>路飞学城</h4>
		<h5>路飞学城</h4>
		<h6>路飞学城</h6> -->
		<div class="para">
		<!-- 定义段落 通常指文章一段内容 -->
		<p>路飞学城立志帮助有志向的年轻人通过努力学习获得体面的工作和生活!路飞学员通过学习Python ,金融分析,人工智能等互联网最前沿技术,开启职业生涯新可能</p>
		<p>路飞学城立志帮助有志向的年轻人通过努力学习获得体面的工作和生活!路飞学员通过学习Python ,金融分析,人工智能等互联网最前沿技术,开启职业生涯新可能</p>
		<p>路飞学城立志帮助有志向的年轻人通过努力学习获得体面的工作和生活!路飞学员通过学习Python ,金融分析,人工智能等互联网最前沿技术,开启职业生涯新可能</p>
		</div>

		<div class="lists">
			<!-- 无序列表 -->
			<ul type="circle">
				<li>我的账户</li>
				<li>我的订单</li>
				<li>我的优惠券</li>
				<li>我的收藏</li>
				<li>退出</li>
			</ul>
			<!-- 有序列表 -->
			<ol type="a">
				<li>我的账户</li>
				<li>我的订单</li>
				<li>我的优惠券</li>
				<li>我的收藏</li>
				<li>退出</li>
			</ol>
		</div>
	</div>
</body>
</html>
```

分析上面代码可以下面的层次结构
```
<div id='wrap'>
	<div class='para'></div>
	<div class='anchor'></div>
	<div class='para'></div>
	<div class='lists'></div>	
</div>	
```

我们将文档放在一个父级的区（div）中，它里面包含四块区（div）域，浏览器查看效果,你会发现每小块区域都是独占一行的，所以div是块级元素。另外，每块区域表示独立的一块，id属性和class属性其实很简单，你可以看成给这个区域起个名字。id是唯一的，一个页面中不能有两个重复的id，跟身份证号码一样，class可以设置同样的属性值，并且可以设置多个，例如class=’para n1‘

## 图片标签 `<img/>`

一个网页除了有文字，还会有图片。我们使用`<img/>`标签在网页中插入图片。

语法：`<img src="图片地址" alt="图片加载失败时显示的内容" title = "提示信息" />`

注意：
1. src设置的图片地址可以是本地的地址也可以是一个网络地址。
2. 图片的格式可以是png、jpg和gif。
3. alt属性的值会在图片加载失败时显示在网页上。
4. 还可以为图片设置宽度(width)和高度(height)，不设置就显示图片默认的宽度和高度
```html
	<div>
		<span>与行内元素展示的标签<span>
		<span>与行内元素展示的标签<span>
		<img src="./machine-right.png" alt="金融量化分析" style="width:200px;height:200px">
		<img src="./finance-right.png" alt="人工智能实战"  style="width: 200px;height: 200px">
	</div>
```
浏览器查看效果：行内块元素
1. 与行内元素在一行内显示
2. 可以设置宽度和高度
3. span标签可以单独摘出某块内容，结合css设置相应的样式

```html
<p>路飞学城立志帮助有志向的年轻人通过努力学习获得体面的工作和生活!路飞学员通过学习Python ,<span>金融分析</span>,<span>人工智能</span>等互联网最前沿技术,开启职业生涯新可能</p>
```

好的，同学们，此时大家是不是对于以上标签有所认知了呢？
这样吧！我来出一个小练习，你来做！
练习：将img标签中的图片独占一行展示，并设置设置相应标题，在图片下方，描述该图片内容的信息。

## 其他标签
#### 换行标签 `<br>`

`<br>`标签用来将内容换行，其在HTML网页上的效果相当于我们平时使用word编辑文档时使用回车换行。
#### 分割线 `<hr>`
`<hr>`标签用来在HTML页面中创建水平分隔线，通常用来分隔内容
#### 特殊符号
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

> 所以HTML代码对缩进的要求并不严格，我们通常使用缩进来让我们的代码结构更清晰，仅此而已。

### 特殊字符
在上一个实例中，我们演示了HTML中输入空格、回车都是没有作用的。要想输入空格，需要用特殊符号 -- `&nbsp;`。

常用的特殊字符：

| 内容       | 代码   |
| :-------: | :--------:|
| 空格       | `&nbsp;`    |
| >         | `&gt; `     |
| <         | `&lt;  `    |
| &         | `&amp;`     |
| ¥         | `&yen;`     |
| 版权       | `&copy;`    |
| 注册        | `&reg;`     |

[HTML特殊符号对照表](http://tool.chinaz.com/Tools/HtmlChar.aspx)

