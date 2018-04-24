```
<div id="search">
    <input type="text" id="text" />        
    <label for="txt" id="msg">路飞学城</label>
</div>
```

```css
*{
    padding: 0;
    margin: 0;
}

#search{
    position: relative;
}

input{
    outline: none;
    display: block;
    width: 490px;
    height: 50px;
    margin-top: 20px;
    font-size: 20px;
    border: 2px solid orange;
    border-radius: 10px;


}
label{
    position: absolute;
    top: 20px;
    left: 10px;
    font-size:8px;
    color: gray;

}
```

```js
var txt = document.getElementById('text');
var msg = document.getElementById('msg');

//检测用户表单输入的时候
txt.oninput = function(){
    
    //控制元素显示隐藏
    if (this.value == '') {
                msg.style.display = 'block'
            }else{
        msg.style.display = 'none'
    }
}
```



