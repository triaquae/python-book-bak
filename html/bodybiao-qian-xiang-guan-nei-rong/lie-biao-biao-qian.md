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

ol标签的属性：

type：列表标识的类型 
  - 1：数字
  - a：小写字母
  - A：大写字母
  - i：小写罗马字符
  - I：大写罗马字符

start：列表标识的起始编号
  - 默认为1

ul标签的属性：
type：列表标识的类型
  - disc：实心圆(默认值)
  - circle：空心圆
  - square：实心矩形
  - none：不显示标识