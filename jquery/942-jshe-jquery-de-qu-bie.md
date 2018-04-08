## JavaScript和jquery的区别
1. Javascript是一门编程语言，我们用它来编写客户端浏览器脚本。
2. jQuery是javascript的一个库，包含多个可重用的函数，用来辅助我们简化javascript开发
3. jQuery能做的javascipt都能做到，而javascript能做的事情，jQuery不一定能做到

![](/jquery/jquery.jpg)


注意：一般情况下，是库的文件，该库中都会抛出来构造函数或者对象，如果是构造函数，那么使用new关键字创建对象，如果是对象直接调用属性和方法


## DOM文档加载的步骤
1. 解析HTML结构。
2. 加载外部脚本和样式表文件。
3. 解析并执行脚本代码。
4. DOM树构建完成。
5. 加载图片等外部文件。
6. 页面加载完毕。

## 执行时间不同

window.onload必须等到页面内包括图片的所有元素加载完毕后才能执行。

$(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。

## 编写个数不同

window.onload不能同时编写多个，如果有多个window.onload方法，只会执行一个

$(document).ready()可以同时编写多个，并且都可以得到执行

## 简化写法不同

window.onload没有简化写法

$(document).ready(function(){})可以简写成$(function(){});