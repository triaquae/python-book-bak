<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?9cae5942a3c39f3b6fcf0a32b00277e2";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>


## 本节重点：

* 使学生掌握字符串格式的方法

> **本节时长需控制在10分钟之内**

## 格式化输出\(10分钟\)

现有一练习需求，问用户的姓名、年龄、工作、爱好 ，然后打印成以下格式

```
------------ info of Alex Li -----------
Name  : Alex Li
Age   : 22
job   : Teacher
Hobbie: girl
------------- end -----------------
```

你怎么实现呢？你会发现，用字符拼接的方式还难实现这种格式的输出，所以一起来学一下新姿势

只需要把要打印的格式先准备好， 由于里面的 一些信息是需要用户输入的，你没办法预设知道，因此可以先放置个占位符，再把字符串里的占位符与外部的变量做个映射关系就好啦

```py
name = input("Name:")
age = input("Age:")
job = input("Job:")
hobbie = input("Hobbie:")

info = '''
------------ info of %s ----------- #这里的每个%s就是一个占位符，本行的代表 后面拓号里的 name 
Name  : %s  #代表 name 
Age   : %s  #代表 age  
job   : %s  #代表 job 
Hobbie: %s  #代表 hobbie 
------------- end -----------------
''' %(name,name,age,job,hobbie)  # 这行的 % 号就是 把前面的字符串 与拓号 后面的 变量 关联起来 

print(info)
```

%s就是代表字符串占位符，除此之外，还有%d,是数字占位符， 如果把上面的age后面的换成%d，就代表你必须只能输入数字啦

```
age     : %d
```

我们运行一下，但是发现出错了。。。![](/assets/format_print_sample.jpeg)说%d需要一个数字，而不是str, what? 我们明明输入的是数字呀，22，22呀。

不用担心 ，不要相信你的眼睛我，们调试一下，看看输入的到底是不是数字呢？怎么看呢？查看数据类型的方法是什么来着？type\(\)

```
name = input("Name:")
age = input("Age:")
print(type(age))
```

执行输出是

```
Name:Alex
Age:22
<class 'str'> #怎么会是str
Job:IT
....
```

让我大声告诉你，**input接收的所有输入默认都是字符串格式！**

要想程序不出错，那怎么办呢？简单，你可以把str转成int

```
age = int(  input("Age:")  )
print(type(age))
```

肯定没问题了。相反，能不能把数字转成字符串呢？必然可以，`str( yourStr )`

