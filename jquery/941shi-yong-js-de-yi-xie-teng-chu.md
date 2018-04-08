## 使用javascript的一些疼处

```
书写繁琐，代码量大

代码复杂

动画效果，很难实现。使用定时器 各种操作和处理
```
#### HTML
```html
    <button id="btn">按钮</button>
    <div></div>
    <div></div>
    <div></div>
```
#### CSS
```css
<style type="text/css">
		div{
			width: 100%;
			height: 100px;
			background-color: pink;
			margin-top: 30px;
			display: none;
		}
		
</style>

```
#### javascript
```javascript
window.onload = function(){
document.getElementById('btn').onclick = function(){

	var divs = document.getElementsByTagName('div');
		for(var i = 0;i<divs.length;i++){
				divs[i].style.display = 'block';
				divs[i].innerHTML = '我出来了！！'
			}

		}
		}
		
//如果使用jQuery操作上面的案例，很简单，三句代码搞定
	$('#btn').click(function(){
			$('div').css('display','block');
			$('div').html('我出来了')
			
		})
```



