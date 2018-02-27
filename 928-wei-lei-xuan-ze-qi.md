# 伪类选择器

常用的几种伪类选择器。

没有访问的超链接a标签样式：

```css
a:link {
  color: blue;
}
```

访问过的超链接a标签样式：
```css
a:visited {
  color: gray;
}
```

鼠标悬浮在标签上应用样式：

```css
a:hover {
  background-color: #eee; 
}
```

鼠标点击瞬间的样式：

```css
a:active {
  color: green;
}
```

input输入框获取光标时样式：

```css
input:focus {
  outline: none;
  background-color: #eee;
}
```