# 网页中引用CSS样式
+ 内联样式
+ 行内样式表
+ 外部样式表
  - 链接式
  - 导入式
  
![CSS语法](/assets/chapter9/CSS/图片 1.png)





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




## @import url()方式

了解即可。

index.css
```css
@import url(other.css)
```
注意：
`@import url()`必须写在文件最开始的位置。