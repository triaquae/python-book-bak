## jquery的事件

想到事件，大家一定会想到对象了，那就是我们的DOM元素。jquery的事件是非常重要的内容，大家一定要把经常使用的事件熟记在心，其余的事件了解


### 1.ready

DOM元素加载完成之后，就会调用此方法，通常写jquery代码的时候要使用此方法。注意：跟window.onload()方法的区别

```javascript
$(document).ready(function(){

})
//等价与
$(function(){

})

```







