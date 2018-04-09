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
## 基本过滤选择器
```html
		<ul>
			<li>哈哈哈</li>
			<li>嘿嘿嘿</li>
			<li>天王盖地虎</li>
			<li>小鸡炖蘑菇</li>
			
		</ul>
```
```javascript

	//:first  获取第一个元素
		$('li:first').text('真的吗？')
		//:last 获取最后一个元素
		$('li:last').html('我是最后一个元素？')

		//:odd 匹配所有索引值为奇数的元素，从0开始计数
		$('li:odd').css('color','green');
		
		//:even 匹配所有索引值为偶数的元素，从0开始计数
		$('li:even').css('color','red')
		
		//:eq(index) 获取给定索引值的元素 从0开始计数
		$('li:eq(1)').css('font-size','30px')
		
		//:gt(index)匹配所有大于给定索引值的元素
		$('li:gt(1)').css('font-size','40px')
		
		//:lt(index) 匹配所有小于给定索引值的元素
		$('li:lt(1)').css('font-size','40px')
	
		//一个给定索引值的元素
		console.log($('p:eq(3)').text())

```

## 属性选择器
```html
	<div id="box">
			<h2 class="title">属性元素器</h2>
			<p class="p1">我是一个段落</p>
			<ul>
				<li id="li1">分手应该体面</li>
				<li class="what">分手应该体面</li>
				<li class="what">分手应该体面</li>
				<li class="heihei">分手应该体面</li>
				
			</ul>
			
			<form action="" method="post">
				
				<input name="username" type='text' value="1" checked="checked"></input>
				<input name="username1111" type='text' value="1"></input>
				<input name="username2222" type='text' value="1"></input>
				<input name="username3333" type='text' value="1"></input>
				<button class="btn-default">按钮1</button>
				<button class="btn-info">按钮1</button>
				<button class="btn-success">按钮1</button>
				<button class="btn-danger">按钮1</button>
				
				
			</form>
		</div>
```
```javascript
	//属性选择器
		
		//标签名[属性名] 查找所有含有id属性的该标签名的元素
		$("li[id]").css('color','red')
		
		//[attr=value] 匹配给定的属性是某个特定值的元素
		$('li[class=what]').css('font-size','30px')
		
		//[attr!=value] 匹配所有不含有指定的属性，或者属性不等于特定值的元素
		$('li[class!=what]').css('color','darkgreen')
		
		//匹配给定的属性是以某些值开始的元素
		$('input[name^=username]').css('background','red')
		
		//匹配给定的属性是以某些值结尾的元素
		$('input[name$=222]').css('background','yellow')
		//匹配给定的属性是以包含某些值的元素
		$("button[class*='btn']").css('background','#0000FF')
```


## 筛选选择器
```html
		<div id="box">
			<p class="p1">
				<span>我是第一个span标签</span>
				<span>我是第二个span标签</span>
				<span>我是第三个span标签</span>
			</p>
			<button>按钮</button>
		</div>
		<ul>
			<li class="list">2</li>
			<li>3</li>
			<li>4</li>
			<li>5</li>
		</ul>
		
```

```javascript
	//获取第n个元素 数值从0开始
		$('span').eq(0).css('font-size','30px')

		//first()获取第一个元素
		$('span').first().css('background','red')
		
		//last()获取最后一个元素
		
		//.parent() 选择父亲元素
		$('span').parent('.p1').css({width:'300px',height:'300px',background:'yellow'})
		
		
		//.siblings()选择所有的兄弟元素
		$('.list').siblings('li').css('color','red')
		
		//.find()
		//查找所有的后代元素
		$('div').find('button').css('background','#313131')
```

### silbings

