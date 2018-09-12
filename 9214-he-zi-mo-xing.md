# 盒模型

### width:内容的宽高

### height:内容的高

### padding:内边距

### border:边框

### margin:外边距

## 盒模型的概念

在CSS中，"box model"这一术语是用来设计和布局时使用，然后在网页中基本上都会显示一些方方正正的盒子。我们称为这种盒子叫盒模型。

盒模型有两种：标准模型和IE模型。我们在这里重点讲标准模型。

## 盒模型示意图

![](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180514180637276-468859360.gif)

## 盒模型的属性

width：内容的宽度

height: 内容的高度

padding：内边距，边框到内容的距离

border: 边框，就是指的盒子的宽度

margin：外边距，盒子边框到附近最近盒子的距离

如果让你做一个宽高402\*402的盒子，您如何来设计呢？

答案有上万种，甚至上一种。

## 盒模型的计算

如果一个盒子设置了padding，border，width，height，margin\(咱们先不要设置margin，margin有坑，后面课程会讲解\)

盒子的真实宽度=width+2\*padding+2\*border

盒子的真实宽度=height+2\*padding+2\*border

那么在这里要注意看了。标准盒模型，width不等于盒子真实的宽度。

另外如果要保持盒子真实的宽度，那么加padding就一定要减width，减padding就一定要加width。真实高度一样设置。

## padding

padding：就是内边距的意思，它是边框到内容之间的距离

另外padding的区域是有背景颜色的。并且背景颜色和内容的颜色一样。也就是说background-color这个属性将填充所有的border以内的区域

## padding的设置

padding有四个方向，分别描述4个方向的padding。

描述的方法有两种

1、写小属性,分别设置不同方向的padding

```css
padding-top: 30px;
padding-right: 30px;
padding-bottom: 30px;
padding-left: 30px;
```

2、写综合属性，用空格隔开

```css
/*
上 右 下 左
*/

padding: 20px 30px 40px 50px ;

/*
上 左右  下
*/

padding: 20px 30px 40px;

/*
 上下 左右
*/

padding: 20px 30px;

/*
上下左右
*/
padding: 20px;
```

## 一些标签默认有padding

比如ul标签，有默认的padding-left值。

那么我们一般在做站的时候，是要清除页面标签中默认的padding和margin。以便于我们更好的去调整元素的位置。

我们现在初学可以使用通配符选择器

```css
*{
  padding:0;
  margin:0;    
}
```

But，这种方法效率不高。

所以我们要使用并集选择器来选中页面中应有的标签（不同背，因为有人已经给咱们写好了这些清除默认的样式表，reset.css）

> [https://meyerweb.com/eric/tools/css/reset/](https://meyerweb.com/eric/tools/css/reset/)

边框

border:边框的意思，描述盒子的边框

边框有三个要素： 粗细 线性样式 颜色

```
border: solid
```

如果颜色不写，默认是黑色。如果粗细不写，不显示边框。如果只写线性样式，默认的有上下左右 3px的宽度,实体样式，并且黑色的边框。

## 按照3要素来写border

```css
border-width: 3px;
border-style: solid;
border-color: red;

/*

border-width: 5px 10px;
border-style: solid dotted double dashed;
border-color: red green yellow;

*/
```

## 按照方向划分

```css
border-top-width: 10px;
border-top-color: red;
border-top-style: solid;

border-right-width: 10px;
border-right-color: red;
border-right-style: solid;

border-bottom-width: 10px;
border-bottom-color: red;
border-bottom-style: solid;

border-left-width: 10px;
border-left-color: red;
border-left-style:solid;
```

上面12条语句，相当于 bordr: 10px solid red;

另外还可以这样：

```css
border-top: 10px solid red;
border-right: 10px solid red;
border-bottom: 10px solid red;
border-left: 10px solid red;
```

清除边框的默认样式，比如input输入框

```css
 border:none;
 border:0;
```

## 使用border来制作小三角

```css
/*小三角 箭头指向下方*/
        div{
            width: 0;
            height: 0;
            border-bottom: 20px solid red;
            border-left: 20px solid transparent;
            border-right: 20px solid transparent;
        }
```

## margin

margin：外边距的意思。表示边框到最近盒子的距离。\(兄弟之间\)

```css
/*表示四个方向的外边距离为20px*/
margin: 20px;
/*表示盒子向下移动了30px*/
margin-top: 30px;
/*表示盒子向右移动了50px*/
margin-left: 50px;
margin-bottom: 100px;
```



