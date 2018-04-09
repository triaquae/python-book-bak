## jQuery的文档操作

### 1、插入操作

一、父元素.append(子元素) 追加某元素  父元素中添加新的元素


```javascript
			var oli = document.createElement('li');
			oli.innerHTML = '哈哈哈'
			
			
			//jquery中的dom操作
			
			//1.append(content)追加  往父元素中添加新的元素
			//content:string | element | jquery元素
			$('ul').append('<li>1233</li>')
			$('ul').append(oli)
			$('ul').append($('#app'))
			
```


二、子元素.appendTo(父元素) 追加到某元素 子元素添加到父元素

```javascript

$('<li>天王盖地虎</li>').appendTo($('ul')).addClass('hu')
			
```
三、prepend（） 前置添加， 添加到父元素的第一个位置

```javascript
$('ul').prepend('<li>我是第一个</li>')
```

四、prependTo 后置添加，第一个元素添加到父元素中

```javascript
 $('<a href="#">路飞学诚</a>').prependTo('ul')
```

五、after() 在匹配的元素之后插入内容 === insertAfter()

```javascript

```

六、before() 在匹配的元素之前插入内容 === insertBefor()


### 2、复制操作

### 3、替换操作

### 4、删除操作

### 5、删除相关操作的区别

