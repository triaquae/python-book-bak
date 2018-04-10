## jquery的属性操作

jquery对象有它自己的属性和方法，我们先研究一下jquery的属性操作。  
jquery的属性操作模块分为四个部分：html属性操作，dom属性操作，类样式操作和值操作

```
html属性操作：是对html文档中的属性进行读取，设置和移除操作。比如attr()、removeAttr()

DOM属性操作：对DOM元素的属性进行读取，设置和移除操作。比如prop()、removeProp()

类样式操作：是指对DOM属性className进行添加，移除操作。比如addClass()、removeClass()、toggleClass()

值操作：是对DOM属性value进行读取和设置操作。比如html()、text()、val()
```

### attr

概念：设置属性值或者 返回被选元素的属性值

```javascript
        //获取值：attr()设置一个属性值的时候 只是获取值
        var id = $('div').attr('id')
        console.log(id)
        var cla = $('div').attr('class')
        console.log(cla)
        //设置值
        //1.设置一个值 设置div的class为box
        $('div').attr('class','box')
        //2.设置多个值，参数为对象，键值对存储
        $('div').attr({name:'hahaha',class:'happy'})
```

### removeAttr

从每一个匹配的元素中删除一个属性

### prop

prop\(\)获取在匹配的元素集中的第一个元素的属性值.它是对当前匹配到的dom对象设置属性。

### removeProp

用来删除由.prop\(\)方法设置的属性集

### addClass（添加多个类名）

为每个匹配的元素添加指定的类名。  
$\('div'\).addClass\("box"\):添加一个类名

$\('div'\).addClass\("box box2"\):**添加多个类名**

### removeClass

从所有匹配的元素中删除全部或者指定的类。

$\('div'\).removeClass\('box'\)移除指定的类

$\('div'\).removeClass\(\)移除全部的类

```javascript
var tag  = false;
        $('span').click(function(){
            if(tag){
                $('span').removeClass('active')
                tag=false;
            }else{
                $('span').addClass('active')
                tag=true;
            }    
        })
```

### toggleClass

如果存在（不存在）就删除（添加）一个类。

语法：toggleClass\('box'\)

```javascript
$('span').click(function(){
    //动态的切换class类名为active
    $(this).toggleClass('active')
})
```

### html

获取值：

html\(\) 是获取选中标签元素中所有的内容

设置值：设置该元素的所有内容 会替换掉 标签中原来的内容

```javascript
$('ul').html('<a href="#">百度一下</a>')
    //可以使用函数来设置所有匹配元素的内容
$('ul').html(function(){
    return '哈哈哈'
})
```

### text

获取值：

text\(\) 获取匹配元素包含的文本内容

设置值：  
设置该所有的文本内容   
**注意**：值为标签的时候 不会被渲染为标签元素 只会被当做值渲染到浏览器中

### val

获取值：

val\(\)用于表单控件中获取值，比如input textarea select等等

设置值：

```javascript
$('input').val('设置了表单控件中的值')
```



