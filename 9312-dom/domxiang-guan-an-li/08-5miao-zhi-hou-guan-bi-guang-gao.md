```
<img src="images/1.gif"/ id="left">
        <img src="images/1.gif"/ id="right">
        <ul>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>
            <li>屠龙宝刀，点击就送</li>

</ul>
```

```css
*{
    padding: 0;
    margin: 0;
    }
img{
    position: fixed;
}
ul{
    list-style: none;
}
#left{
    left: 0;
    }
#right{
    right: 0;
    }
ul li{
    font-size: 25px;
}
```

```js
window.onload  = function(){
            var left = document.getElementById('left');
            var right = document.getElementById('right');

            setTimeout(function(){
                left.style.display = 'none';
                right.style.display = 'none';


            },5000)
}
```



