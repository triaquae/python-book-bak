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
### prop
### removeProp
### addClass
### removeClass
### toggleClass
### html
### text
### val