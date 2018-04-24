```
<div class="box">
    点击有惊喜！！
</div>
```

```css
*{
    padding: 0;
    margin: 0;
}
.box{
    width: 200px;
    height: 200px;
    background: red;
    text-align: center;
    color: white;
    line-height: 200px;
    font-size: 23px;
    font-weight: bold;
    margin: 20px auto;
}
```

```js
var oBox = document.getElementsByClassName('box')[0];

//初始化点击的次数。通过次数的增加来改变DOM的样式
var a = 0;
oBox.onclick  = function(){
	a++;
	if(a%4===1){
		this.style.background = 'green';
		this.innerText = '继续点击哦！';
	}else if(a%4==2){
		this.style.background = 'blue';
		this.innerText = '哈哈！骗你的';
	}else if(a%4==3){
		this.style.background = 'transparent';
		this.innerText = '';
	}else{
		this.style.background = 'red';
		this.innerText = '点击有惊喜！！';
	}	
	
}
```



