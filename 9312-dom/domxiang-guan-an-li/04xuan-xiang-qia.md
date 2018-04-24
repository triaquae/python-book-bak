```
<div id="tab">
  <ul>
     <li class="active"><a href="#">首页</a></li>
     <li><a href="#">新闻</a></li>
     <li><a href="#">图片</a></li>

 </ul>
     <p class="active">首页内容</p>
     <p>新闻内容</p>
     <p>图片内容</p>


/div>
```

```css
*{
    padding: 0;
    margin: 0;
}
ul{list-style: none;}
#tab{
    width: 480px;
    margin: 20px auto;
    border: 1px solid red;
}
ul li{
    float: left;
    width: 160px;
    height: 60px;
    line-height: 60px;
    text-align: center;
    background-color: #cccccc;
}

ul li a{
    text-decoration: none;
    color:black;
}
li.active{
    background-color: #FFFFFF;
}
p{
    display: none;
    height: 200px;
    text-align: center;
    line-height: 200px;
    background-color: #FFFFFF;
}
p.active{
    display: block;

}
```

```js
var tabli = document.getElementsByTagName('li');
var tabContent = document.getElementsByTagName('p')

for(var i = 0; i < tabli.length; i++){
	//为了保存我的i的变量
	tabli[i].index  = i;
	tabli[i].onclick = function(){
		
		for(var j = 0; j < tabli.length; j++){
			tabli[j].className = '';
			tabContent[j].className = '';
		}	
		this.className = 'active'
		console.log(this.index)
		tabContent[this.index].className = 'active';
	}
}
```



