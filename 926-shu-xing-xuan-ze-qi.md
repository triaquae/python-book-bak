# 属性选择器

除了HTML标签的id属性和class属性外，还可以根据HTML标签的特定属性选择标签。


## 根据属性查找

```css
[title] {
  color: red;
}
```

## 根据属性和值查找

找到所有title属性等于hello的标签：
```css
[title="hello"] {
  color: red;
}
```

找到所有title属性以hello开头的标签：
```css
[title^="hello"] {
  color: red;
}
```

找到所有title属性以hello结尾的标签：
```css
[title$="hello"] {
  color: red;
}
```

找到所有title属性中包含（字符串包含）hello的标签：

```css
[title*="hello"] {
  color: red;
}
```
找到所有title属性(有多个值或值以空格分割)中有一个值为hello的标签：

```css
[title~="hello"] {
  color: red;
}
```



## 
