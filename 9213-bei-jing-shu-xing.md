# 背景属性

常用背景相关属性：

| 属性      | 描述     |
|:--------:|:---------:|
|background-color	|规定要使用的背景颜色。|
|background-image	|规定要使用的背景图像。|
|background-size	|规定背景图片的尺寸。|
|background-repeat	|规定如何重复背景图像。|
|background-attachment	|规定背景图像是否固定或者随着页面的其余部分滚动。|
|background-position	|规定背景图像的位置。|
|inherit	|规定应该从父元素继承background属性的设置。|

`background-repeat`取值范围：

| 值      | 描述     |
|:--------:|:---------:|
|repeat	|默认。背景图像将在垂直方向和水平方向重复。|
|repeat-x	|背景图像将在水平方向重复。|
|repeat-y	|背景图像将在垂直方向重复。|
|no-repeat	|背景图像将仅显示一次。|
|inherit	|规定应该从父元素继承background-repeat属性的设置。|

`background-attachment`取值范围：

| 值      | 描述     |
|:--------:|:---------:|
|scroll	|默认值。背景图像会随着页面其余部分的滚动而移动。|
|fixed	|当页面的其余部分滚动时，背景图像不会移动。|
|inherit	|规定应该从父元素继承background-attachment属性的设置。|


`background-position`取值范围：

| 值      | 描述     |
|:--------:|:---------:|
|top left <br> top center <br> top right <br> center left <br> center center <br> center right <br> bottom left <br> bottom center <br> bottom right|如果只设置了一个关键词，那么第二个值就是"center"。<br> 默认值：0% 0%。|
|x% y% |第一个值是水平位置，第二个值是垂直位置。<br> 左上角是 0% 0%。右下角是 100% 100%。<br> 如果只设置了一个值，另一个值就是50%。
|xpos ypos|第一个值是水平位置，第二个值是垂直位置。<br> 左上角是 0 0。单位是像素 (0px 0px) 或任何其他的 CSS 单位。<br> 如果只设置了一个值，另一个值就是50%。<br> 可以混合使用`%`和`position`值。

示例：

```css
body {
  background-color: red;
  backgraound-image: url(xx.png);
  background-size: 300px 300px;
  background-repeat: no-repeat;
  background-position: center 
}
```

简写：

```css
body { 
  background: red url(xx.png) no-repeat fixed center/300px 300px; 
}
```
