# CSS引入方式


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


## 链接式

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


## 