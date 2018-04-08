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

如果存在（不存在）就删除（添加）一个类。

语法：toggleClass('box')
### html
获取值：

html() 是获取选中标签元素中所有的内容

设置值：设置该元素的所有内容 会替换掉 标签中原来的内容
```javascript
$('ul').html('<a href="#">百度一下</a>')
	//可以使用函数来设置所有匹配元素的内容
	$('ul').html(function(){
			return '哈哈哈'
		})
```
### text
text() 获取匹配元素包含的文本内容
### val
val()用于表单控件中获取值，比如input textarea select等等