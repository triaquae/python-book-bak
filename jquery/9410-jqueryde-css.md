### position

获取匹配元素相对父元素的偏移位置


### offset

获取匹配元素在当前视口的相对偏移,返回的对象包含两个整型属性：top 和 left
```javascript
$("p").offset()
$('div').offset().top
$("p").offset().left
```

### scrollTop
获取匹配元素相对滚动条顶部的偏移  文档被卷起的像素值


### scrollLeft
获取匹配元素相对滚动条左侧的偏移  文档被卷起的像素值


```javascript
 //获取匹配元素相对滚动条顶部的偏移  文档被卷起的像素值
$(document).scrollTop()
$(document).scrollLeft()

//监听文档滚动的jquery方法
$(document).scroll(function(){
	console.log($(document).scrollTop())
	console.log($(document).scrollLeft())
		
 })
```



### innerHeight

获取第一个匹配元素内部区域高度（包括补白、不包括边框）

```javascript
$('#box').innerHeight()
```



### innerWidth

获取第一个匹配元素内部区域宽度（包括补白、不包括边框）

```javascript
$('#box').innerWeight()
```

### outerHeight

获取第一个匹配元素外部高度（默认包括补白和边框）

```javascript
$('#box').outerHeidth()
```

### outerWeight

获取第一个匹配元素外部宽度（默认包括补白和边框）

```javascript
$('#box').outerWeidth()

```


### weight
取得匹配元素当前计算的宽度值


```javascript
//获取值
$('p').width()

//设置值
$('p').width(200)
```

### height
取得匹配元素当前计算的高度值
```javascript
//获取值
$('p').height()
//设置值
$('p').Height(200）
```




