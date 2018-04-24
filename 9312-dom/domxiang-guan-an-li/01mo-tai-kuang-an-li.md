```
<body>
    <button id="btn">弹出</button>
</body>
```

```css
*{padding: 0;margin: 0;}
html,body{height: 100%;}
#box{width: 100%;height: 100%;background: rgba(0,0,0,.3);}
#content{
    position: relative;
    top: 150px;
    width: 400px;
    height: 200px;
    line-height: 200px;
    text-align: center;
    color: red;
    background-color: #fff;
    margin: auto;
}
#span1{
    position: absolute;
    background-color: red;
    top: 0;
    right: 0;
    width: 30px;
    height: 30px;
    line-height: 30px;
    text-align: center;
    color: #fff;
}
```

```js
//dom  Document Object Model

//树状结构
/*
    html
head    body  节点
    span div button img ....

  */

//获取dom元素
var btn = document.getElementById('btn')

//创建divdom元素
var oDiv = document.createElement('div')
var oP = document.createElement('p')
var oSpan = document.createElement('span')


oDiv.id = 'box';
oP.id = 'content'
oP.innerHTML = '模态框成功弹出'
oSpan.innerHTML = 'X';
oSpan.id = 'span1'


oDiv.appendChild(oP)
oP.appendChild(oSpan)


//给按钮添加点击事件
btn.onclick = function(){
  //动态的添加到body中一个div
    console.log(this);//当前this指向的是当前按钮元素
    this.parentNode.insertBefore(oDiv,btn)

}
oSpan.onclick = function(){
// removeChild()

    oDiv.parentNode.removeChild(oDiv)
}
```



