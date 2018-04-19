## Bootstrap的下载

一. 使用Bootstrap第一步，先将生成环境的Bootstrap下载下来。然后将下载，然后引入到自己建好的当前目录中

![](/jquery/01.png)
<br>



![](/jquery/03.jpg)





二、点到**起步**中的**基本模板**


将看到的整段代码复制粘贴到建好的index.html文件中

```
官网明确表示：
使用此给出的这份超级简单的HTML模板，或者修改这些实例。我们强烈建议你对这些实例按照自己的需求进行修改，而不要简单的复制、粘贴
```


本来是想在这里写Book，但发现官网上的语言组织的更牛逼！接下来就跟着我一起进入Bootstrap的css样式、组件、插件。



### Bootstrap支持移动设备优先

也就是说使用Bootstrap可以在移动设备上运行。为了确保适当的绘制和触屏缩放，需要在```<head>```之中添加viewport元数据标签。

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

在移动设备浏览器上，通过为视口（viewport）设置 meta 属性为 user-scalable=no 可以禁用其缩放（zooming）功能。这样禁用缩放功能后，用户只能滚动屏幕，就能让你的网站看上去更像原生应用的感觉。注意，这种方式我们并不推荐所有网站使用，还是要看你自己的情况而定！

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
```


### Bootstrap重置样式

为了增强跨浏览器表现的一致性，我们使用了 Normalize.css，这是由 Nicolas Gallagher 和 Jonathan Neal 维护的一个CSS 重置样式库。


### 布局容器

Bootstrap 需要为页面内容和栅格系统包裹一个 .container 容器。我们提供了两个作此用处的类。注意，由于 padding 等属性的原因，这两种 容器类不能互相嵌套。


.container 类用于固定宽度并支持响应式布局的容器。

```html
<div class="container">
  ...
</div>
```

.container-fluid 类用于 100% 宽度，占据全部视口（viewport）的容器。

```html
<div class="container-fluid">
  ...
</div>
```


### 栅格系统

栅格系统的鼻祖是 <a>https://960.gs/</a>.

Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列

栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。下面就介绍一下 Bootstrap 栅格系统的工作原理：


![](/jquery/04.png)


#### 栅格参数

![](/jquery/05.png)



使用单一的一组 .col-md-* 栅格类，就可以创建一个基本的栅格系统，在手机和平板设备上一开始是堆叠在一起的（超小屏幕到小屏幕这一范围），在桌面（中等）屏幕设备上变为水平排列。所有“列（column）必须放在 ” .row 内。




一些常使用网站


阿里巴巴图标库网站：

[](http://www.iconfont.cn/)

如果想做图表，那可以去官网：

[](http://echarts.baidu.com/)

[](https://chartjs.bootcss.com/)




**
PS:还是那句话，使用Bootstrap非常简单，根据项目的需求适当去官网复制粘贴，然后根据需求更改自己的内容，如果想修改自己的样式，可以添加类，按照之前咱们学习css一样的方式，给它相应的样式**






