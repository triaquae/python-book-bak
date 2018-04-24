```js
setInterval(function(){
		
	var date = new Date();
	
	var y = date.getFullYear();
	var m = date.getMonth();
	var d = date.getDate();
	var h = date.getHours();
	var min = date.getMinutes();
	var s =  date.getSeconds();
	
	//今天是2018年2月23日 8:23:09
	
	
	document.body.innerHTML = "今天是"+y+'年' + num(m+1)+"月"+ num(d) + "日" + num(h)+":"+num(min)+":"+num(s)
	
},1000)

function num(n){
	if (n<10) {
		return "0"+ n;
				
			}
	return n
}

```



