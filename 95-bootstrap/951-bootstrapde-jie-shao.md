## Bootstrap的介绍

凡是使用过Bootstrap的开发者，都不在乎做这么两件事情：复制and粘贴。哈哈~，是的使用Bootstrap非常简单，但是在复制粘贴之前，需要先对Bootstrap的用法一一熟悉之后我们才开始干活！


Bootstrap，来自 Twitter，是目前最受欢迎的前端框架。Bootstrap 是基于 HTML、CSS、javascript 的，它简洁灵活，使得 Web 开发更加快捷。

它用于开发响应式布局、移动设备优先的 WEB 项目




#### 首先要知道，我们为什么要写自适应的页面（响应式页面）


众所周知，电脑、平板、手机的屏幕是差距很大的，假如在电脑上写好了一个页面，在电脑上看起来不错，但是如果放到手机上的话，那可能就会乱的一塌糊涂，这时候怎么解决呢？以前，可以再专门为手机定制一个页面，当用户访问的时候，判断设备是手机还是电脑，如果是手机就跳转到相应的手机页面，例如百度的就是，手机访问www.baidu.com就会跳转到m.baidu.com，这样做简直就是费力不讨好的活，所以聪明的程序员开发了一种自适应写法，即一次开发，处处显示！这到底是一个什么样的神器东西呢，接下来就揭晓它的神秘面纱。

#### CSS3 的 @media 查询

定义和使用

使用 @media 查询，你可以针对不同的屏幕大小定义不同的样式。 @media 可以针对不同的屏幕尺寸设置不同的样式，特别是如果你需要设置设计响应式的页面，@media 是非常有用的。 当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面，这对调试来说是一个极大的便利。

CSS 语法：
```css
@media mediaType and|not|only (media feature) {
     /*CSS-Code;*/
}
```
媒体类型（mediaType ）
类型有很多，在这里不一一列出来了，只列出了常用的几个。



all	用于所有设备 
print	用于打印机和打印预览
screen	用于电脑屏幕，平板电脑，智能手机等。（最常用）
speech	应用于屏幕阅读器等发声设备
媒体功能（media feature）
媒体功能也有很多，以下列出常用的几个

值	描述

max-width:定义输出设备中的页面最大可见区域宽度
min-width:定义输出设备中的页面最小可见区域宽度


开始编写响应式页面


编写之前呢，有几个要准备的工作

准备工作1：设置Meta标签

首先我们在使用 @media 的时候需要先设置下面这段代码，来兼容移动设备的展示效果：

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
```

这段代码的几个参数解释：

width = device-width：宽度等于当前设备的宽度
initial-scale：初始的缩放比例（默认设置为1.0，即代表不缩放）

user-scalable：用户是否可以手动缩放（默认设置为no，因为我们不希望用户放大缩小页面）
其他还有很多参数呢，想要了解的童鞋可以直接去百度


准备工作2：加载兼容文件JS

因为IE8既不支持HTML5也不支持CSS3 @media ，所以我们需要加载两个JS文件，来保证我们的代码实现兼容效果：

```html
<!--[if lt IE 9]>
　　<script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
　　<script src="https://oss.maxcdn.com/libs/respond.js/1.3.0/respond.min.js"></script>
<![endif]-->
```

准备工作3：设置IE渲染方式默认为最高(可选)
现在有很多人的IE浏览器都升级到IE9以上了，所以这个时候就有又很多诡异的事情发生了，例如现在是IE9的浏览器，但是浏览器的文档模式却是IE8 为了防止这种情况，我们需要下面这段代码来让IE的文档渲染模式永远都是最新的
```html

<meta http-equiv="X-UA-Compatible" content="IE=Edge，chrome=1">
```
这段代码后面加了一个chrome=1，如果用户的电脑里安装了 chrome，就可以让电脑里面的IE不管是哪个版本的都可以使用Webkit引擎及V8引擎进行排版及运算，如果没有安装，就显示IE最新的渲染模式。

代码实例

1、如果文档宽度小于等于 300px 则应用花括号内的样式——修改body的背景颜色(background-color):

```css
@media screen and (max-width: 300px) {
    body {
        background-color:lightblue;
    }
}
```
从上面的代码可以看出，媒体类型是屏幕（screen），使用 一个 and 连接后面的媒体功能，这里写的是 max-width:300px ，也就是说，当屏幕的最大宽度 小于等于 300px 的时候，就应用花括号里面的样式。
 
2、当文档宽度大于等于300px 的时候显示的样式

```css
@media screen and (min-width: 300px){
    body {
        background-color:lightblue;
    }
}
```

注意，这里的媒体功能使用的是 min-width 而不是 max-width，我已经标红高亮显示出来了。

 
3、当文档宽度大于等于 300px 并且小于等于500px （ width >=300 && width <=500）的时候显示的样式
```css
@media screen and (min-width:300px) and (max-width:500px) {
    /* CSS 代码 */
}
```

注意，这里使用了两个 and ，用来连接 两个媒体功能，一个用于限制最小，一个用于限制最大。

※ 需要注意的地方（划重点）

1、通过灵活应用以上技巧，开发出一个响应式页面，还不是近在咫尺的感觉。

2、不要被 min-width 和 max-width 所迷惑，初学者很容易误以为 min-width 的意思是小于xxx的时候才应用，然而这就陷入误区了，其实它的意思是：当设置了 min-width 的时候，文档的宽度如果小于设置的值，就不会应用这个区块里的CSS样式，所以 min-width 它才能实现大于等于设置的值得时候，才会应用区块里的CSS样式，max-width 也是如此。

3、或者这样想想，先看代码，这句代码的意思是宽度大于等于 300px ，小于等于 500px （ width >=300 && width <=500）的时候应用样式

```css
@media screen and (min-width:300px) and (max-width:500px) {
    /* CSS 代码 */
}
```

min-width:300px 的作用是当文档宽度不小于 300px 的时候就应用 {} 里的CSS代码块，即大于等于 300px，max-width:500px 的作用是当文档宽度不大于 500px 的时候就应用{} 里的CSS代码块，即小于等于 500px 是不是这样想就容易明白了些呢？

4、这里有个弯很难绕过来，自己多动手做做实验，多动脑想想，就豁然开朗了。
