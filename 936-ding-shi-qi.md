# 本节知识点：\(重点\)

* ### setTimeout\(\)
* ### setInterval\(\)

##### 定时器

在js中有两种定时器：

* 一次性定时器：setTimeout\(\)

* 周期性循环定时器: setInterval\(\)

###### setTimeout\(\)

只在指定的时间后执行一次

```javascript
/定时器 异步运行  
function hello(){  
alert("hello");  
}  
//使用方法名字执行方法  
var t1 = window.setTimeout(hello,1000);  
var t2 = window.setTimeout("hello()",3000);//使用字符串执行方法  
window.clearTimeout(t1);//去掉定时器
```

###### setInterval\(\)

在指定时间为周期循环执行

```javascript
/实时刷新  时间单位为毫秒  
setInterval('refreshQuery()',8000);   
/* 刷新查询 */  
function refreshQuery(){  
  console.log('每8秒调一次') 
}
```

两种方法根据不同的场景和业务需求择而取之，

对于这两个方法，需要注意的是如果要求在每隔一个固定的时间间隔后就精确地执行某动作，那么最好使用setInterval，而如果不想由于连续调用产生互相干扰的问题，尤其是每次函数的调用需要繁重的计算以及很长的处理时间，那么最好使用setTimeout

