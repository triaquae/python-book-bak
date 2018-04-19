# 高级选择器

![CSS语法](/assets/chapter9/CSS/图片 3.png)

## 后代选择器

因为HTML元素可以嵌套，所以我们可以从某个元素的后代查找特定元素，并设置样式：

```css
div p {
  color: red;
}
```

从div的所有后代中找p标签，设置字体颜色为红色。

## 儿子选择器

```css
div>p {
  color: red;
}
```

从div的直接子元素中找到p标签，设置字体颜色为红色。

## 毗邻选择器

```css
div+p {
  color: red;
}
```

找到所有紧挨在div后面的第一个p标签，设置字体颜色为红色。

## 弟弟选择器

```css
div~p {
  color: red;
}
```

找到所有div标签后面同级的p标签，设置字体颜色为红色。

