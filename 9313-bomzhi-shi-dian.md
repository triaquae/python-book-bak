# 1.BOM输出

所谓BOM指的是浏览器对象模型 Browser Object Model，它的核心就是浏览器

```js
alert(1);//弹出框 调式使用
```

```js
console.log('路飞学城');//用于浏览器的调用 F12查看
```

```js
 prompt('message',defaultValue)
 var pro = prompt('路飞学城','33333');
 console.log(pro)
```

```js
confirm() //如果点击确定 返回true 如果点击取消 返回false
```

# 

# 2.open\_close方法

```js
open('https://www.baidu.com');//打开百度网页，winodow对象可以省略
//行间的js中的window不能省略
<button onclick="window.open('https://www.luffycity.com/')">路飞学城</button>

//打开空白页面
open('about:blank',"_self")

//关闭当前页面
close();
//行间js中的window还是不能省略
<button onclick="window.close()">关闭</button>
```

# 3.其他的BOM对象和方法

```js
//返回浏览器的用户设备信息
console.log(window.navigator.userAgent)


//获取用户本地信息
console.log(window.location)

//经常使用的一个方法，跳转一个网址
window.location.href = 'https://www.luffycity.com';

//全局刷新 后面会学习ajax来实现局部刷新操作，这才是我们要学习的重点。记住：尽量少用这个方法

setTimeout(function(){
    window.location.reload();
}
```

# 4.client系列

```
style：
     top
     left
     right
     bottom

client：
     clientTop 内容区域到边框顶部的距离
     clientLeft 内容区域到边框左部的距离
     clientWidth 内容区域+左右padding   可视宽度
     clientHeight 内容区域+ 上下padding   可视高度
```

# 5.屏幕的可视区域

```js
window.onload = function(){

    console.log(document.documentElement.clientWidth);
    console.log(document.documentElement.clientHeight);


    window.onresize = function(){

        console.log(document.documentElement.clientWidth);
        console.log(document.documentElement.clientHeight);
    }



}
```

# 6.offset系列

```
//占位宽 高 Top Left  

/*
* offsetTop: 如果盒子没有设置定位 到浏览器的顶部的距离,如果盒子设置定位，那么是以父盒子为基准的top值
* offsetLeft： 如果盒子没有设置定位 到浏览器的左部的距离，如果盒子设置定位，那么是以父盒子为基准的left值
  offsetWidth 内容+padding+border
* */
```

# 7.scroll系列

```
<body style="width: 2000px;height: 2000px;">
    <div style="height: 200px;background-color: red;"></div>
    <div style="height: 200px;background-color: green;"></div>
    <div style="height: 200px;background-color: yellow;"></div>
    <div style="height: 200px;background-color: blue;"></div>
    <div style="height: 200px;background-color: gray;"></div>
    <div id = 'scroll' style="width: 200px;height: 200px;border: 1px solid red;overflow: auto;padding: 10px;margin: 5px 0px 0px 0px;">
        <p>路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城
            路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城
            路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城
            路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城路飞学城
        </p>

    </div>


</body>
```

```css
*{
padding: 0;
margin: 0;
}
```

```js
window.onload = function(){

            //实施监听滚动事件
            window.onscroll = function(){

//                console.log('上'+document.documentElement.scrollTop)
//                console.log('左'+document.documentElement.scrollLeft)
//                console.log('宽'+document.documentElement.scrollWidth)
//                console.log('高'+document.documentElement.scrollHeight)


            }

            var s = document.getElementById('scroll');

            s.onscroll = function(){
                //scrollHeight : 内容的高度+padding  不包含边框
                console.log('上'+s.scrollTop)
                console.log('左'+s.scrollLeft)
                console.log('宽'+s.scrollWidth)
                console.log('高'+s.scrollHeight)
            }
        }
```



