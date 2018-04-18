# 开发工具介绍

前端常用开发工具：sublime、visual Studio Code、HBuilder、Webstorm。

那么大家使用的PCharm跟WebStorm是JetBrains公司推出的编辑工具，开发阶段建议使用。





# 我的第一个javascript实例

```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
	<style type="text/css">
		.span1{
			color: red;
		}
		
	</style>
	<!-- 外链式 -->
	<!-- <script src="./1.js"></script> -->

</head>
<body>
	<!-- dom  == document object model   行内式引入-->
	<p id='p1' onclick="clickhandler()">123</p>


</body>

<!-- 内部式  建议 引入的时候要在body之后，我们要等待所有的dom元素和图片资源加载完成之后再去执行相应的js操作-->
<script type="text/javascript">

	document.write('<span class="span1">233</span>')

	console.log('星儿今天很漂亮！')

	console.error('错了')
	console.dir(window)
	var a = prompt('请输入你的名字');
	console.log(a);

	function clickhandler(){
		// 弹出警告框
		// 都好好的好好的
		/*
		这是一个方法
		一个很好的方法
		*/
		// window.alert(1);
	}

	
</script>
</html>
```



