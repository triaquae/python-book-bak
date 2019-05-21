# 字体相关CSS属性介绍

## font-family

字体系列。

`font-family`可以把多个字体名称作为一个“回退”系统来保存。如果浏览器不支持第一个字体，则会尝试下一个。浏览器会使用它可识别的第一个值。

简单实例：

```css
body {
  font-family: "Microsoft Yahei", "微软雅黑", "Arial", sans-serif
}
```

如果设置成`inherit`，则表示继承父元素的字体。

## font-weight

字重（字体粗细）。

取值范围：

| 值 | 描述 |
| :---: | :---: |
| normal | 默认值，标准粗细 |
| bold | 粗体 |
| bolder | 更粗 |
| lighter | 更细 |
| 100~900 | 设置具体粗细，400等同于normal，而700等同于bold |
| inherit | 继承父元素字体的粗细值 |

## font-size

字体大小。

```css
p {
  font-size: 14px;
}
```

如果设置成`inherit`表示继承父元素的字体大小值。

## color

设置内容的字体颜色。

支持三种颜色值：

* 十六进制值 如: ＃FF0000
* 一个RGB值 如: RGB\(255,0,0\)
* 颜色的名称 如:  red

```css
p {
  color: red;
}
```



