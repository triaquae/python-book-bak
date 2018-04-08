## jquery文件的引入
 上节课说到，一般情况下，是库的文件，该库中都会抛出来构造函数或者对象 ，如果是构造函数，那么创建对象，如果是对象直接调用属性和方法

使用jquery第一步，先引入jquery，然后再写相应的jquery代码


## 使用jquery注意了

DOM元素加载完成之后就会调用

```javascript
// DOM元素加载完成之后就会调用

//程序执行需要有入口 1.入口函数的方式
$(document).ready(function(){

  alert(1)

 })
 等价于
 $(function(){
    //alert(22);
     $('#btn').click(function(){
       $('div').show().html('我的内容')
    })
 
 })

```