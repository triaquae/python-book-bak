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
请看上面代码 `<h1>`和`<h2>`书写在一行上展示，但是在浏览器的效果却是换行了，大家现在可以回顾一下9.1.4标签分类的特点了

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


## 其他标签
### 换行标签 `<br>`
### 分割线 `<hr>`
###特殊
