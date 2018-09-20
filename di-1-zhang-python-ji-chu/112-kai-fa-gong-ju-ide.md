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

* 使学生掌握Pycharm开发工具的使用
* 掌握代码调试功能

> **本节时长需控制在10分钟之内**

## 为什么要用IDE？

到现在为止，我们也是写过代码的人啦，但你有没有发现，每次写代码要新建文件、写完保存时还要选择存放地点，执行时还要切换到命令行调用python解释器，好麻烦呀，能否一气呵成，让我简单的写代码？此时开发工具IDE上场啦，一个好的IDE能帮你大大提升开发效率。

很多语言都有比较流行的开发工具，比如JAVA 的Eclipse, C\#,C++的VisualStudio, Python的是啥呢？ Pycharm，最好的Python 开发IDE

**安装**

下载地址:[https://www.jetbrains.com/pycharm/download](https://www.jetbrains.com/pycharm/download) 选择Professional 专业版

> Comunnity社区版是免费的，但支持的功能不多，比如以后我们会学的Django就不支持，所以还是用专业版，但专业版是收费的，一年一千多，不便宜。唉，万能的淘宝。。。不宜再多说啦。

注册完成后启动，会让你先创建一个项目，其实就是一个文件夹，我们以后的代码都存在这里面![](/assets/create%20project.jpeg)

你以后写的项目可能有成百上千个代码文件 ，全放在一起可不好，所以一般把同样功能的代码放在一个目录，我们现在以天为单位，为每天的学习创建一个目录day1,day2,day3...这样![](/assets/CREATE%20DIR.jpeg)

创建代码文件 ![](/assets/create%20file.jpeg)

执行代码![](/assets/执行文件.jpeg)

#### 代码调试

想不想看代码一步步的执行过程？比如想看每次循环某个变量有没有变化，总是print太low了，试试pycharm 牛逼的debug功能吧![](/assets/代码调试.jpeg)

