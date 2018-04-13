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

栅格系统的鼻祖是 <a>https://960.gs/</a>


