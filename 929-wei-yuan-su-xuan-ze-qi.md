# 伪元素

介绍常用的伪元素。

## first-letter

用于为文本的首字母设置特殊样式。

例如：

```css
p:first-letter {
  font-size: 48px;
}
```

## before

用于在元素的内容前面插入新内容。

例如：

```css
p:before {
  content: "*";
  color: red;
}
```

在所有p标签的内容前面加上一个红色的`*`。

## after

用于在元素的内容后面插入新内容。

例如：

```css
p:after {
  content: "?";
  color: red;
}
```

在所有p标签的内容后面加上一个蓝色的`?`。

