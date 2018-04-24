```
<div id="wrap">

    <button id="btn">运动</button>
    <div class="box" id="box1">

    </div>

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
    background-color: #FF0000;
    position: absolute;
    top: 50px;
    left: 0px;
}
```

```js
    var btn = document.getElementById('btn');

    var box1 = document.getElementById('box1')

    var count  = 0;
    var time = null;
    btn.onclick = function(){

        time = setInterval(function(){
            count+=10;
            if(count>1000){
                clearInterval(time)
                box1.style.display = 'none'
            }

            box1.style.left = count + 'px'                

        },10)

    }
```



