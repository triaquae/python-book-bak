# 伪类选择器

常用的几种伪类选择器。

没有访问的超链接a标签样式：

```css
a:link {
  color: blue;
}
```

访问过的超链接a标签样式：

```css
a:visited {
  color: gray;
}
```

鼠标悬浮在元素上应用样式：

```css
a:hover {
  background-color: #eee; 
}
```

鼠标点击瞬间的样式：

```css
a:active {
  color: green;
}
```

input输入框获取焦点时样式：

```css
input:focus {
  outline: none;
  background-color: #eee;
}
```

_**hover选择器在网页中非常好用，如果是我鼠标悬浮的是父盒子，想让父盒子的子盒子显示出来，这种效果其实也可以用hover选择器。但是我们要将hover选择器和后代选择器结合起来一起用,下面是个例子，大家copy看效果，瞬间就明白,鼠标悬浮alex上 会显示一张图片。**_

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
		ul{
			list-style: none;

		}

		ul li{
			position: relative;
		}
		ul li img{
			display: none;
			position: absolute;
			top: -16px;
			left: 36px;
		}
		ul li:hover img{
			display: block;
		}
	</style>

</head>
<body>

	<ul>
	    <li>
	    	 alex
	    	<img class="original-img" src="https://i8.mifile.cn/b2c-mimall-media/4f036ae4d45002b2a6fb6756cedebf02.png" >
	    </li>
	    
	 
	</ul>
	
</body>
</html>
```



