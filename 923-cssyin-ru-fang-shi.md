# 网页中引用CSS样式

* 内联样式
* 行内样式表
* 外部样式表
  * 链接式
  * 导入式

![CSS语法](/assets/chapter9/CSS/图片 2.png)

## 内嵌方式

`style`标签

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf8">
        <style>
            p {
                color: red;
            }
        </style>
    </head>
    <body>
        <p>这是一个p标签！</p>
    </body>
</html>
```

## 行内样式

```html
<!doctype html>
<html>
<head>
<meta charset="utf8">
</head>
<body>
<p style="color: blue;">这是一个p标签！</p>
</body>
</html>
```

## 外联样式表-链接式

`link`标签

index.css

```css
p {
  color: green;
}
```

然后在HTML文件中通过link标签引入：

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf8">
        <link rel="stylesheet" href="index.css">
    </head>
    <body>
        <p>这是一个p标签！</p>
    </body>
</html>
```

## 外联样式表-@import url\(\)方式 导入式

了解即可。

index.css

```css
@import url(other.css)
```

注意：  
`@import url()`必须写在文件最开始的位置。

#### 链接式与导入式的区别

```
1、<link/>标签属于XHTML,@import是属性css2.1
2、使用<link/>链接的css文件先加载到网页当中，再进行编译显示
3、使用@import导入的css文件，客户端显示HTML结构，再把CSS文件加载到网页当中
4、@import是属于CSS2.1特有的，对于不兼容CSS2.1的浏览器来说就是无效的
```



