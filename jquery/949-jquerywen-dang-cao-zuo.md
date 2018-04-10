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
//如果直接的内容是当前页面中的某些元素，那么这些元素将从原位置上消失。简言之，就是一个移动操作
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

五、父.after(子) 在匹配的元素之后插入内容 与 子.insertAfter(父)

```javascript
$('ul').after('<h4>我是一个h3标题</h4>')
$('<h5>我是一个h2标题</h5>').insertAfter('ul')
```

六、父.before(子) 在匹配的元素之前插入内容 与 子.insertBefor(父)

```javascript
$('ul').before('<h3>我是一个h3标题</h3>')
$('<h2>我是一个h2标题</h2>').insertBefore('ul')
```


### 2、复制操作
clone() 克隆匹配的DOM元素并且选中这些克隆的副本

```javascript

$('button').click(function() {
  
  // 1.clone()：克隆匹配的DOM元素并且选中这些克隆的副本。
 // 2.clone(true)：元素以及其所有的事件处理并且选中这些克隆的副本(简言之，副本具有与真身一样的事件处理能力)
  $(this).clone(true).insertAfter(this);
})
```

### 3、替换操作
一、replaceWith()：将所有匹配的元素替换成指定的HTML或DOM元素。

```javascript
//将所有的h5标题替换为a标签
$('h5').replaceWith('<a href="#">hello world</a>')
//将所有h5标题标签替换成id为app的dom元素
$('h5').replaceWith($('#app'));


```
二、replaceAll():用匹配的元素替换掉所有 selector匹配到的元素

```javascript
$('<br/><hr/><button>按钮</button>').replaceAll('h4')

```

### 4、删除操作
一、remove() 删除节点后，事件也会删除（简言之，删除了整个标签）

```javascript
$('ul').remove();
```

二、detach() 删除节点后，事件会保留

```javascript
 var $btn = $('button').detach()
 //此时按钮能追加到ul中
 $('ul').append($btn)
```

三、empty(): 清空元素中的所有后代节点

```javascript
//清空掉ul中的子元素，保留ul
$('ul').empty()
```
