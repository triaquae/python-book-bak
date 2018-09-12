# 在玩浮动之前先看一下标准文档流

## 什么是标准文档流

宏观的将，我们的web页面和ps等设计软件有本质的区别，web 网页的制作，是个“流”，从上而下 ，像 “织毛衣”。而设计软件 ，想往哪里画东西，就去哪里画

标准文档流下 有哪些微观现象？

### 1.空白折叠现象

多个空格会被合并成一个空格显示到浏览器页面中。img标签换行写。会发现每张图片之间有间隙，如果在一行内写img标签，就解决了这个问题，但是我们不会这样去写我们的html结构。这种现象称为空白折叠现象。

### 2.高矮不齐，底边对齐

文字还有图片大小不一，都会让我们页面的元素出现高矮不齐的现象，但是在浏览器查看我们的页面总会发现底边对齐

### 3.自动换行，一行写不满，换行写

如果在一行内写文字，文字过多，那么浏览器会自动换行去显示我们的文字。

## 浮动

浮动是css里面布局最多的一个属性，也是很重要的一个属性。

float：表示浮动的意思。它有四个值。

* none: 表示不浮动，默认
* left: 表示左浮动
* right：表示右浮动

看个栗子

```html
<div class="box1"></div>
<div class="box2"></div>
<span>路飞学城</span>
```

```css
.box1{
     width: 300px;
     height: 300px;
     background-color: red;
     float:left;
  }
 .box2{
     width: 400px;
     height: 400px;
     background-color: green;
     float:right;
   }
   span{
     float: left;
     width: 100px;
     height: 200px;
     background-color: yellow;
    }
```

我们会发现，三个元素并排显示，.box1和span因为是左浮动，紧挨在一起，这种现象贴边。.box2盒子因为右浮动，所以紧靠着右边。\(UI很多都是模糊了用户的双眼，脱离了文档标准流，其实不在文档中了，好比是有个盒子，我给它设置了透明色，我们看不到它，但是它实际存在的。\)

那么浮动如果大家想学好，一定要知道它的四大特性

**1.浮动的元素脱标**

**2.浮动的元素互相贴靠**

**3.浮动的元素由"子围"效果**

**4.收缩的效果**

### 浮动元素脱标

脱标：就是脱离了标准文档流

看例子

```html
     <div class="box1">小红</div>
     <div class="box2">小黄</div>
     <span>小马哥</span>
     <span>小马哥</span>
```

```
.box1{
            width: 200px;
            height: 200px;
            background-color: red;
            float: left;

        }
        .box2{
            width: 400px;
            height: 400px;
            background-color: yellow;

        }
        span{
            background-color: green;
            float: left;
            width: 300px;
            height: 50px;
        }
```

效果：红色盒子压盖住了黄色的盒子，一个行内的span标签竟然能够设置宽高了。

原因1：小红设置了浮动，小黄没有设置浮动，小红脱离了标准文档流，其实就是它不在页面中占位置了，此时浏览器认为小黄是标准文档流中的第一个盒子。所以就渲染到了页面中的第一个位置上。这种现象，也有一种叫法，浮动元素“飘起来了”，但我不建议大家这样叫。

原因2：所有的标签一旦设置浮动，就能够并排，并且都不区分行内、块状元素，都能够设置宽高

### 浮动元素互相贴靠

看例子

html结构

```html
<div class="box1">1</div>
<div class="box2">2</div>
<div class="box3">3</div>
```

css样式

```css
.box1{
            width: 100px;
            height: 400px;
            float: left;
            background-color: red;
        }
        .box2{
            width: 150px;       
            height: 450px;
            float: left;
            background-color: yellow;
        }
        .box3{
            width: 300px;
            height: 300px;
            float: left;
            background-color: green;
        }
```

效果发现：

如果父元素有足够的空间，那么3哥紧靠着2哥，2哥紧靠着1哥，1哥靠着边。  
如果没有足够的空间，那么就会靠着1哥，如果再没有足够的空间靠着1哥，自己往边靠

### 浮动元素字围效果

html结构：

```html
<div>
   <img src="./images/企业1.png" alt="">    
</div>
<p>
   123路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞路飞
</p>
```

[![](https://common.cnblogs.com/images/copycode.gif "复制代码")](javascript:void%280%29;)

css样式：

```css
       *{
            padding: 0;
            margin: 0;
        }
        div{
            float: left;
        }
        p{
            background-color: #666;
        }
```

**效果发现**：所谓字围效果，当div浮动，p不浮动，div遮盖住了p，div的层级提高，但是p中的文字不会被遮盖，此时就形成了字围效果。

### 浮动元素紧凑效果

收缩：一个浮动元素。如果没有设置width，那么就自动收缩为文字的宽度（这点跟行内元素很像）

html结构：

```markdown
<div>alex</div>
```

css样式：

```css
div{
    float: left;
    background-color: red;
}
```

大家一定要谨记：关于浮动，我们初期一定要遵循一个原则，永远不是一个盒子单独浮动，要浮动就要一起浮动。另外，有浮动，一定要清除浮动。

### 为什么要清除浮动

在页面布局的时候，每个结构中的父元素的高度，我们一般不会设置。（为什么？）

大家想，如果我第一版的页面的写完了，感觉非常爽，突然隔了一个月，老板说页面某一块的区域，我要加点内容，或者我觉得图片要缩小一下。这样的需求在工作中非常常见的。真想打他啊。那么此时作为一个前端小白，肯定是去每个地方加内容，改图片，然后修改父盒子的高度。那问题来了，这样不影响开发效率吗？答案是肯定的。

看一个效果：

html效果：

```markdown
<div class="father">    
     <div class="box1"></div>
     <div class="box2"></div>
     <div class="box3"></div>

</div>

<div class="father2"></div>
```

css样式：

```css
       *{
            padding: 0;
            margin: 0;

        }
        .father{
            width: 1126px;
            /*子元素浮动 父盒子一般不设置高度*/

            /*出现这种问题，我们要清除浮动带来影响*/
            /*height: 300px;*/

        }
        .box1{
            width: 200px;
            height: 500px;
            float: left;
            background-color: red;
        }
        .box2{
            width: 300px;
            height: 200px;
            float: left;
            background-color: green;
        }
        .box3{
            width: 400px;
            float: left;
            height: 100px;
            background-color: blue;
        }
        .father2{
            width: 1126px;
            height: 600px;
            background-color: purple;
        }
```

效果发现：如果不给父盒子一个高度，那么浮动子元素是不会填充父盒子的高度，那么此时.father2的盒子就会跑到第一个位置上，影响页面布局。

那么我们知道，浮动元素确实能实现我们页面元素并排的效果，这是它的好处，同时它还带来了页面布局极大的错乱！！！所以我们要清除浮动

还好还好。我们有多种清除浮动的方法，在这里给大家介绍四种：

1. 给父盒子设置高度
2. clear:both
3. 伪元素清除法
4. overflow：hidden

#### 给父盒子设置高度

这个方法给大家上个代码介绍，它的使用不灵活，一般会常用页面中固定高度的，并且子元素并排显示的布局。比如：导航栏

#### clear：both

clear：意思就是清除的意思。

有三个值：

left：当前元素左边不允许有浮动元素

right：当前元素右边不允许有浮动元素

both：当前元素左右两边不允许有浮动元素

给浮动元素的后面加一个空的div，并且该元素不浮动，然后设置clear：both。

html结构：

```html
<div>
        <ul>
            <li>Python</li>
            <li>web</li>
            <li>linux</li>
            <!-- 给浮动元素最后面加一个空的div 并且该元素不浮动 ，然后设置clear:both  清除别人对我的浮动影响-->
            <!-- 内墙法 -->
            <!-- 无缘无故加了div元素  结构冗余 -->
            <div class="clear"></div>

        </ul>

</div>
<div class="box">

</div>
```

css样式

```css
*{
            padding: 0;
            margin: 0;
        }
        ul{
            list-style: none;

        }


        div{
            width: 400px;

        }


        div ul li {
            float: left;
            width: 100px;
            height: 40px;
            background-color: red;
        }
        .box{
            width: 200px;
            height: 100px;
            background-color: yellow;
        }
        .clear{
            clear: both;
        }
```

#### 伪元素清除法\(常用\)

给浮动子元素的父盒子，也就是不浮动元素，添加一个clearfix的类，然后设置

```css
.clearfix:after{
    /*必须要写这三句话*/
    content: '.';
    clear: both;
    display: block;
}
```

新浪首页推荐伪元素清除法的写法



```css
/*
新浪首页清除浮动伪元素方法
*/

              content: ".";
                display: block;
                height: 0;
                clear: both;
                visibility: hidden
```



#### overflow:hidden\(常用\)

overflow属性规定当内容溢出元素框时发生的事情。

说明：

这个属性定义溢出元素内容区的内容会如何处理。如果值为 scroll，不论是否需要，用户代理都会提供一种滚动机制。因此，有可能即使元素框中可以放下所有内容也会出现滚动条。

有五个值：

| 值 | 描述 |
| :--- | :--- |
| visible | 默认值。内容不会被修剪，会呈现在元素框之外。 |
| hidden | 内容会被修剪，并且其余内容是不可见的。 |
| scroll | 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。 |
| auto | 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。 |
| inherit | 规定应该从父元素继承 overflow 属性的值。 |

逐渐演变成overflow：hidden清除法。

其实它是一个BFC区域: [https://blog.csdn.net/riddle1981/article/details/52126522](https://blog.csdn.net/riddle1981/article/details/52126522)

到此为止。关于浮动的实现并排、清除浮动的四个用法已经介绍完毕，大家一定要熟记于心。





### margin塌陷问题

当时说到了盒模型，盒模型包含着margin，为什么要在这里说margin呢？因为元素和元素在垂直方向上margin里面有坑。

我们来看一个例子：  


html结构：



```html
<div class="father">
    <div class="box1"></div>        
    <div class="box2"></div>
</div>
```



css样式：



```css
*{
            padding: 0;
            margin: 0;
        }
        .father{
            width: 400px;
            overflow: hidden;
            border: 1px solid gray;
        }
        .box1{
            width: 300px;
            height: 200px;
            background-color: red;
            margin-bottom: 20px;}
        .box2{
            width: 400px;
            height: 300px;
            background-color: green;
            margin-top: 50px;
        }
```



当给两个标准流下兄弟盒子 设置垂直方向上的margin时，那么以较大的为准，那么我们称这种现象叫塌陷。我们称为这种技巧叫“奇淫技巧”。记住这种现象，在布局垂直方向盒子的时候主要margin的用法。

当我们给两个标准流下的兄弟盒子设置浮动之后，就不会出现margin塌陷的问题。

### margin：0 auto;



```css
 div{
            width: 780px;
            height: 50px;
            background-color: red;
            /*水平居中盒子*/
            margin: 0px auto;
                        /*水平居中文字*/
            text-align: center;

        }
    
    
```

[](javascript:void%280%29;)

当一个div元素设置margin：0 auto;时就会居中盒子，那我们知道margin:0 auto;表示上下外边距离为0，左右为auto的距离，那么auto是什么意思呢？

设置margin-left:auto；我们发现盒子尽可能大的右边有很大的距离，没有什么意义。当设置margin-right:auto；我们发现盒子尽可能大的左边有很大的距离。当两条语句并存的时候，我们发现盒子尽可能大的左右两边有很大的距离。此时我们就发现盒子居中了。



另外如何给盒子设置浮动，那么margin:0 auto失效。



使用margin：0 auto;注意点：

1.使用margin: 0 auto;水平居中盒子必须有width，要有明确width，文字水平居中使用text-align: center;

2.只有标准流下的盒子 才能使用margin:0 auto; 

_当一个盒子浮动了，固定定位，绝对定位\(后面会讲\)，margin:0 auto; 不能用了_

3.margin：0 auto;居中盒子。而不是居中文本，文字水平居中使用text-align: center;



另外大家一定要知道margin属性是描述兄弟盒子的关系，而padding描述的是父子盒子的关系

### 善于使用父亲的padding，而不是margin

![](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180515111706875-433330922.png)

如果让大家实现如图的效果，应该有不少的同学做不出来。

那么我们来看看这个案例，它的坑在哪里？

下面这个代码应该是大家都会去写的代码。

[](javascript:void%280%29;)

```

        *{
            padding: 0;
            margin: 0;
        }
        .father{
            width: 300px;
            height: 300px;
            background-color: blue;
        }
        .xiongda{
            width: 100px;
            height: 100px;
            background-color: orange;
            
            margin-top: 30px;
        }
```

[](javascript:void%280%29;)

![](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180515112116947-1157225325.png)

因为父亲没有border，那么儿子margin-top实际上踹的是“流” 踹的是行,所以父亲掉下来了，一旦给父亲一个border发现就好了。

那么问题来了，我们不可能在页面中无缘无故的去给盒子加一个border，所以此时的解决方案只有一种。就是使用父亲的padding。让子盒子挤下来。



