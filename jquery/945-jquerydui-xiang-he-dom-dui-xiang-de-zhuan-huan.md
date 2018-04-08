## jquery对象和DOM对象转换

### DOM对象转换成jquery对象

```javascript
var box = document.getElementById('box');
console.log($(box));

```

### jquery对象转化成DOM对象

第一种方式：

$('button')[0]

第二种方式：

$('button').get(0)