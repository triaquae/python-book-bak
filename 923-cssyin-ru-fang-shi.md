# CSS引入方式


## 内嵌方式

`style`标签

```HTML

p {
  color: red;
}

```


## 链接式

`link`标签

index.css

```CSS
p {
  color: green;
}

```

然后在HTML文件中通过link标签引入：

```html

<link rel="stylesheet" href="index.css">
```


## 