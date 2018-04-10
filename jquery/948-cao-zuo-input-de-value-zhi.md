### 操作表单域中的value值

#### HTML

```html
    <form action="">
            <input type="radio" name="sex"  value="112" />男
            <input type="radio" name="sex"  value="11" checked="" />女
            <input type="radio" name="sex"  value="11" />gay

            <input type="checkbox" value="a" checked=""/>吃饭
            <input type="checkbox" value="b" checked=""/>睡觉
            <input type="checkbox" value="c" checked=""/>打豆豆

            <select name="timespan" id="timespan" class="Wdate"   >  
                <option value="1">8:00-8:30</option>  
                <option value="2">8:30-9:00</option>  
                <option value="3">9:00-9:30</option>  
            </select>  
            <input type="text" name="" id="" value="111" />
    </form>
```

#### JS

```javascript
    $(function(){
                //1.获取单选框被选中的value值
                console.log($('input[type=radio]:checked').val())

                //2.复选框被选中的value获取到第一个被选中的值
                console.log($('input[type=checkbox]:checked').val())

                //3.下拉列表被选中的值
                var obj = $("#timespan option:selected");
                var  artime_val  = obj.val();  
                console.log(artime_val)
                var  artime_text  = obj.text();  
                console.log("val:"+artime_val+" text"+ artime_text );//val:3 text 9:00-9:30


                //设置value  设置选中项
                $('input[type=radio]').val(['112'])
                $('input[type=checkbox]').val(['a','b'])


                //设置下拉列表框的选中值，必须使用select
                $('select').val(['3','2'])


                //文本框
                console.log($("input[type=text]").val())//获取文本框中的值
                //设置值
                $('input[type=text]').val('试试就试试')




        })
```



