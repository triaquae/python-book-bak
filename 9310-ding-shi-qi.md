# 定时器

在js中的定时器分两种：1、setTimeout\(\) 2、setInterval\(\)

### 1.setTimeOut\(\)

只在指定时间后执行一次

```js
//定时器 异步运行  
function hello(){  
alert("hello");  
}  
//使用方法名字执行方法  
var t1 = window.setTimeout(hello,1000);  
var t2 = window.setTimeout("hello()",3000);//使用字符串执行方法  
window.clearTimeout(t1);//去掉定时器
```

### 2.setInterval\(\)

在指定时间为周期循环执行

```js
//实时刷新时间单位为毫秒  
setInterval('refreshQuery()',8000);   
/* 刷新查询 */  
function refreshQuery(){  
  console.log('每8秒调一次') 
}
```

两种方法根据不同的场景和业务需求择而取之，

一般情况下setTimeout用于延迟执行某方法或功能，

setInterval则一般用于刷新表单，对于一些表单的假实时指定时间刷新同步，动画效果等。

