## jquery的属性操作
对象：有它自己的属性和方法，我们先研究一下jquery的属性操作

### attr
概念：设置属性值或者 返回被选元素的属性值

```javascript	
		//获取值：attr()设置一个属性值的时候 只是获取值
		var id = $('div').attr('id')
		console.log(id)
		var cla = $('div').attr('class')
		console.log(cla)
		//设置值
		//1.设置一个值 设置div的class为box
		$('div').attr('class','box')
		//2.设置多个值，参数为对象，键值对存储
		$('div').attr({name:'hahaha',class:'happy'})

		
```
### removeAttr
从每一个匹配的元素中删除一个属性
### prop
prop()获取在匹配的元素集中的第一个元素的属性值，但是不可以设置多个属性，可以设置一个属性。

### removeProp
用来删除由.prop()方法设置的属性集
### addClass（添加多个类名）
为每个匹配的元素添加指定的类名。
$('div').addClass("box"):添加一个类名

$('div').addClass("box box2"):**添加多个类名**

### removeClass
从所有匹配的元素中删除全部或者指定的类。

$('div').removeClass('box')移除指定的类

$('div').removeClass()移除全部的类
### toggleClass
### html
### text
### val