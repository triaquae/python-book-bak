# 字体相关CSS属性介绍


## font-family

```css
body {
  font-family: "Microsoft Yahei", "微软雅黑", "Arial", sans-serif
}
```

## font-weight

表示字重（字体粗细）。

取值范围：

| 值      | 描述     |
|:--------:|:---------:|
| normal  | 默认值，标准粗细  |
| bord    | 粗体  |
| border  | 更粗粗体  |
| lighter | 更细的体  |
| 100~900 | 设置具体粗细，400等同于normal，而700等同于bold  |
| inherit |从父标签继承字体的粗细|


## font-size

字体大小。

```css
p {
  font-size: inherit;
}
```

inherit表示继承，父标签字体是多大，我的字体就是多大。