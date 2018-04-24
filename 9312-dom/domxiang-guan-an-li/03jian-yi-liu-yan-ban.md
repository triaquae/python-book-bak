```
<h1>简易留言板</h1>
<div id="box">

</div>
<textarea id="msg"></textarea>
<input type="button" id="btn" value="留言"/>
<button onclick="sum()">统计</button>
```



```js
//创建ul标签元素
var ul = document.createElement('ul');
//获取父级元素
var box = document.getElementById('box');
//添加子元素
box.appendChild(ul);

//获取按钮元素
var btn = document.getElementById('btn');

var msg = document.getElementById('msg')

var count = 0;
btn.onclick = function(){

    console.log(msg.value);

    var li = document.createElement('li');

    //设置内容
    li.innerHTML = msg.value + "<span>&nbsp;&nbsp;X</span>"

    var lis = document.getElementsByTagName('li');
    if(lis.length == 0){
        ul.appendChild(li);
        count++;

    }else{
        ul.insertBefore(li,lis[0]);
        count++;
    }
    msg.value = '';

    var spans = document.getElementsByTagName('span');

    for(var i = 0; i< spans.length; i++){
        spans[i].onclick  = function(){
            ul.removeChild(this.parentNode)
            count--;
        }
    }


}

 function sum(){
    alert('一共发布了'+count+'条留言');

}
```



