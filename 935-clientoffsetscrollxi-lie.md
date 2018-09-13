# 本节知识

* ### client
* ### offset

* ### scroll



#### client、offset、scroll系列

他们的作用主要与计算盒模型、盒子的偏移量和滚动有关

```javascript
clientTop 内容区域到边框顶部的距离 ，说白了，就是边框的高度
clientLeft 内容区域到边框左部的距离，说白了就是边框的乱度
clientWidth 内容区域+左右padding   可视宽度
clientHeight 内容区域+ 上下padding   可视高度
```

##### client演示

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style type="text/css">
            .box{
                width: 200px;
                height: 200px;
                position: absolute;
                border: 10px solid red;
                /*margin: 10px 0px 0px 0px;*/
                padding: 80px;
            }
        </style>
    </head>
    <body>
        <div class="box">
            专业丰富的课程体系，博学多闻的实力讲师以及风趣生动的课堂，在路飞，不是灌输知识，而是点燃你的学习火焰。专业丰富的课程体系，博学多闻的实力讲师以及风趣生动的课堂，在路飞，不是灌输知识，而是点燃你的学习火焰。专业丰富的课程体系，博学多闻的实力讲师以及风趣生动的课堂，在路飞，不是灌输知识，而是点燃你的学习火焰。专业丰富的课程体系，博学多闻的实力讲师以及风趣生动的课堂，在路飞，不是灌输知识，而是点燃你的学习火焰。
        </div>
    </body>
    <script type="text/javascript">
        /*
         *      clientTop 内容区域到边框顶部的距离 ，说白了，就是边框的高度
         *      clientLeft 内容区域到边框左部的距离，说白了就是边框的乱度
         *      clientWidth 内容区域+左右padding   可视宽度
         *      clientHeight 内容区域+ 上下padding   可视高度
         * */

        var oBox = document.getElementsByClassName('box')[0];
        console.log(oBox.clientTop);
        console.log(oBox.clientLeft);
        console.log(oBox.clientWidth);
        console.log(oBox.clientHeight)；   

    </script>

</html>
```

###### 屏幕的可视区域

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
    </body>
    <script type="text/javascript">

        // 屏幕的可视区域
        window.onload = function(){

            // document.documentElement 获取的是html标签
            console.log(document.documentElement.clientWidth);
            console.log(document.documentElement.clientHeight);
            // 窗口大小发生变化时，会调用此方法
            window.onresize = function(){    
                console.log(document.documentElement.clientWidth);
                console.log(document.documentElement.clientHeight);
            }         
        }
    </script>
</html>
```

##### offset演示

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style type="text/css">
            *{
                padding: 0;
                margin: 0;
            }
        </style>

    </head>
    <body style="height: 2000px">
        <div>
            <div class="wrap" style=" width: 300px;height: 300px;background-color: green">
                <div id="box" style="width: 200px;height: 200px;border: 5px solid red;position: absolute;top:50px;left: 30px;">            
                </div>
            </div>
        </div>
    </body>
    <script type="text/javascript">
        window.onload = function(){
            var box = document.getElementById('box')
            /*
             offsetWidth占位宽  内容+padding+border
             offsetHeight占位高 
             offsetTop: 如果盒子没有设置定位 到body的顶部的距离,如果盒子设置定位，那么是以父辈为基准的top值
             offsetLeft： 如果盒子没有设置定位 到body的左部的距离，如果盒子设置定位，那么是以父辈为基准的left值

             * */
            console.log(box.offsetTop)
            console.log(box.offsetLeft)
            console.log(box.offsetWidth)
            console.log(box.offsetHeight)

        }

    </script>
</html>
```

##### scroll演示

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style type="text/css">
            *{padding: 0;margin: 0;}
        </style>
    </head>
    <body style="width: 2000px;height: 2000px;">
        <div style="height: 200px;background-color: red;"></div>
        <div style="height: 200px;background-color: green;"></div>
        <div style="height: 200px;background-color: yellow;"></div>
        <div style="height: 200px;background-color: blue;"></div>
        <div style="height: 200px;background-color: gray;"></div>
        <div id = 'scroll' style="width: 200px;height: 200px;border: 1px solid red;overflow: auto;padding: 10px;margin: 5px 0px 0px 0px;">
            <p>学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界学习新技能，达成人生目标，开始用自己的力量影响世界
            </p>

        </div>


    </body>
    <script type="text/javascript">

        window.onload = function(){

            //实施监听滚动事件
            window.onscroll = function(){
//                console.log(1111)
//                console.log('上'+document.documentElement.scrollTop)
//                console.log('左'+document.documentElement.scrollLeft)
//                console.log('宽'+document.documentElement.scrollWidth)
//                console.log('高'+document.documentElement.scrollHeight)


            }

            var s = document.getElementById('scroll');

            s.onscroll = function(){
//            scrollHeight : 内容的高度+padding  不包含边框
                console.log('上'+s.scrollTop)
                console.log('左'+s.scrollLeft)
                console.log('宽'+s.scrollWidth)
                console.log('高'+s.scrollHeight)
            }
        }

    </script>
</html>
```



