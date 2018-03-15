# CSS盒子模型

HTML文档中的每个元素都被描绘成矩形盒子，这些矩形盒子通过一个模型来描述其占用空间，这个模型称为盒子模型。
盒子模型通过四个边界来描述：margin（外边距），border（边框），padding（内填充），content（内容区域），如图所示：

![CSS盒子模型](/assets/chapter9/CSS/CSS_04.png)

注意：浏览器的调试窗口中通常会有相似的模型可供开发调试使用。


## border

边框的常用值：

| 值      | 描述     |
|:--------:|:---------:|
|none	|无边框。|
|dotted	|点状虚线边框。|
|dashed	|矩形虚线边框。|
|solid	|实线边框。|


示例：

```css
div.box {
    display: inline-block;
    width: 200px;
    height: 200px;
    background-color: red;
    padding: 5px 10px 15px 20px;
    border: 5px solid blue;
    margin: 5px 10px;
}
```
1.border会改变元素的实际大小
2.背景色会渲染到border区域
## 内边距
padding:内边距 控制内容到边框的距离
1.只写一个padding代表四个方向，也可以单独指定某一个方向
2.元素设置了padding值是额外家在原来大小之上的width+padding。如果不想改变实际大小，那就在width-padding对应方向的值
3.padding是添加给父级的，改变的是父级包含的内容的位置，自身位置不变
4.简写方法
1）一个值：4个方向
2）两个值：上下 左右
3）三个值：上 左右 下
4）四个值：上 右 下 左（顺时针方向）
注意：padding不支持负值


margin： 外边距  控制元素与元素之间的距离
1）margin 的4个方向
2）margin会改变实际大小，背景色不会渲染到margin区域
这个区域会以空白显示，但是也属于盒子的一部分
3)margin是添自身的,如果哪个想要改变自己的位置，就给谁添加margin
html的部分标签自带margin padding
p body ul


