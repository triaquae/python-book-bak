```
<div id="box" class="wrap">
    <img src="images/mi.png"/ id="xiaomi">

    <span class="up" id="picUp"></span>

    <span class="down" id="picDown"></span>


</div>
```

```css
*{padding: 0;margin: 0;}
.wrap{
    width: 512px;
    height: 400px;
    border: 3px solid #808080;
    position: relative;
    overflow: hidden;
    margin: 100px auto;
}
.wrap span{
    width: 100%;
    height: 200px;
    position: absolute;        
}
.up{
    top: 0;
}
.down{
    bottom: 0;
}
img{
    position: absolute;
    top: 0;
    left: 0;        
}
```

```js
var up = document.getElementById('picUp');
var down = document.getElementById('picDown');

var img = document.getElementById('xiaomi')

var count = 0;
var time = null;
//鼠标移入的时候吧
up.onmouseover = function(){
	
	//不管怎样 上来先清定时器
	clearInterval(time);
	time = setInterval(function(){
		count-=3;
		
		count >= -1070 ? img.style.top = count + 'px': clearInterval(time);  
		
		
		
	},30)
}
down.onmouseover = function(){
	clearInterval(time)
	
	time = setInterval(function(){
		count+=1;
		
		count < 0 ? img.style.top = count + 'px': clearInterval(time);  
		
		
		
	},30)
}

	
```



