# 属性选择器

除了HTML元素的id属性和class属性外，还可以根据HTML元素的特定属性选择元素。


## 根据属性查找

```css
[title] {
  color: red;
}
```

## 根据属性和值查找

找到所有title属性等于hello的元素：
```css
[title="hello"] {
  color: red;
}
```

找到所有title属性以hello开头的元素：
```css
[title^="hello"] {
  color: red;
}
```

找到所有title属性以hello结尾的元素：
```css
[title$="hello"] {
  color: red;
}
```

找到所有title属性中包含（字符串包含）hello的元素：

```css
[title*="hello"] {
  color: red;
}
```

找到所有title属性(有多个值或值以空格分割)中有一个值为hello的元素：

```css
[title~="hello"] {
  color: red;
}
```


## 表单常用

```css
input[type="text"] {
  backgroundcolor: red;
}
```
