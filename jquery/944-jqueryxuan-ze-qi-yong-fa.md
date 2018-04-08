## jquery的基础选择器

选择器的用法其实跟咱们当时讲css的选择器用法类似，只是代码书写的不同
```html

<ul>
	<li id="brother" class="item">路飞学诚1</li>
	<li >路飞学诚2</li>
	<li class="item">路飞学诚3</li>
	<li>路飞学诚4</li>
	<li class="item">路飞学诚5</li>
	<li>路飞学诚6</li>
	<li class="item">路飞学诚7</li>
		<a href="#">百度一下</a>
	</ul>
	<div id="duanzi">
		<p>天王盖地虎</p>
		<p><h1>小鸡炖蘑菇</h1></p>
		<p>宝塔镇河妖</p>
		<p>蘑菇放辣椒</p>
	</div>
```

```javascript

		// 基本选择器
		// 1.id选择器
		$('#brother').css('color','black');
		// 2.标签选择器
		$('a').css('color','yellow')

		// 3.类选择器
		$('.item').css('background','#FC4708')

		// 4.通配符选择器
		// console.log($('*').html())
		console.log($('a').val())
		
```
## 层级选择器
```javascript
	// 后代选择器
		console.log($('div p'))
		$('div p').css('color','red')

		// 子代选择器
		$('div >p').css('background','green')

		// 毗邻选择器 匹配 所有紧接在#brother元素后的下一个元素
		$('#brother+ li').css('color','yellow')

		// 兄弟选择器
		// 匹配所有#brother之后的所有兄弟姐妹元素
		$('#brother~li').css('background','#996633')
		
		// :first  获取第一个元素
		$('li:first').text('真的吗？')
		// :last 获取最后一个元素
		$('li:last').html('真的吗？')


		
		//一个给定索引值的元素
		console.log($('p:eq(3)').text())
```
```javascript
```