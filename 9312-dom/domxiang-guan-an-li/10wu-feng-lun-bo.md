```
<div class="box">
    <ul>
        <li><img src="images/01.jpg"/></li>
        <li><img src="images/02.jpg"/></li>
        <li><img src="images/03.jpg"/></li>
        <li><img src="images/04.jpg"/></li>

    </ul>


 </div>
```

```css
*{
    padding: 0;
    margin: 0;
}
ul{list-style: none;}
.box{
    width: 600px;
    height: 200px;
    margin: 50px auto;
    overflow: hidden;
    position: relative;

}
ul li{
    float: left;
}
.box ul{
    width: 400%;
    position: absolute;
    top: 0;
    left: 0;

}
```

```js
var box = document.getElementsByClassName('box')[0];
var ul = box.children[0];
var num = 0;
var timer = null;

timer = setInterval(autoPlay,30)
//函数的声明
function autoPlay(){
    num--;

    num <=-600 ? num=0 : num ;
    ul.style.left = num + 'px'

}
//鼠标移动上去
box.onmouseover = function(){
    clearInterval(timer)
}
box.onmouseout = function(){
    timer  = setInterval(autoPlay,30);
}
```



