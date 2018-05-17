## 练习答案

1. 简述编译型与解释型语言的区别，且分别列出你知道的哪些语言属于编译型，哪些属于解释型.  

	```
	答:
	  编译型语言：
		使用专门的编译器，针对特定的平台，将高级语言源代码一次性的编译成可被该平台硬件执行的机器码，并包装成该平台所能识别的可执行性程序的格式。
	  特点：
		在编译型语言写的程序执行之前，需要一个专门的编译过程，把源代码编译成机器语言的文件.
	  执行方式:
		源代码 ———> 编译(一次编译) ———>目标代码———>执行(多次执行)———>输出
		
	 解释型语言：
		使用专门的解释器对源程序逐行解释成特定平台的机器码并立即执行。
	 特点：
		解释型语言不需要事先编译，其直接将源代码解释成机器码并立即执行，所以只要某一平台提供了相应的解释器即可运行该程序。
	 执行方式:
	   源代码 ———> 解释器(每次执行都需要解释)———>输出    
	 
	 编译型: C c++, c#
	 解释型: python PHP ruby, java
	```  
 2. 执行 Python 脚本的两种方式是什么  

	```
	 答:
	 1、./run.py.shell直接调用python脚本  

	2、python run.py 调用python 解释器来调用python脚本  
	```     
3. Pyhton 单行注释和多行注释分别用什么?  

	```  
	 答:
	 1, 单行注释使用 # 号
	 2, 多行注释使用 “”“”“”  ‘’‘’‘’
	```   
4. 布尔值分别有什么?  
	 
	```
	 答:
	布尔值分别有：True 和False
	 布尔值为False的有：[] () {} 0 False ""  等
	```   
5. 声明变量注意事项有那些?  

	```
     答案：
        模块名，包名 ：小写字母， 单词之间用户_分割。
        类名：首字母大写。
        全局变量： 大写字母， 单词之间用户_分割。
        普通变量： 小写字母， 单词之间用户_分割。
        函数： 小写字母， 单词之间用户_分割。
        实例变量： 以_开头，其他和普通变量一样 。
        私有实例变量（外部访问会报错）： 以__开头（2个下划线），其他和普通变量一样 。
        专有变量： __开头，__结尾，一般为python的自有变量（不要以这种变量命名）。
              
     ```  
 6. 如何查看变量在内存中的地址?
 
	```
	id
	```  
7. 写代码  	1. 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败!  	2. 实现用户输入用户名和密码,当用户名为 seven 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次  	3. 实现用户输入用户名和密码,当用户名为 seven 或 alex 且 密码为 123 时,显示登陆成功,否则登陆失败,失败时允许重复输入三次  

	```
	username = ['seven','Alex']
	password = '123'
	count = 0
	while count < 3:
		username = input('用户名：')
		password = input('密码：')
		if username in username and password == password:
			print('登陆成功!')
			break
		else:
			print('登陆失败！')
		count += 1
	```  
8. 写代码  a. 使用while循环实现输出2-3+4-5+6...+100 的和  

	```
	答:
	i = 2
	count = 0
	while i <= 100:
		if i % 2 == 0:
			count += i
		else:
			count -= i
		i += 1
	print(count)
	```  
b. 使用 while 循环实现输出 1,2,3,4,5, 7,8,9, 11,12  

	```
	答:
	n1 = True
	n2 = 1
	while n1:
		if n2 == 12:
			print(n2)

			break

		if n2 == 6 or n2 == 10:
			n2 += 1

			continue

		print(n2)

		n2 += 1

	```  
c. 使用while 循环输出100-50，从大到小，如100，99，98...，到50时再从0循环输出到50，然后结束  

	```
	count =100
	while count > 50:
		print(count)
		count -=1
		if count==50:
			count=1
			while count<=50:
				print(count)
				count+=1
			break
	```    
d. 使用 while 循环实现输出 1-100 内的所有奇数  

	```
	count =0
	while count <=100:
		if count %2!=0:
			print(count)
		count +=1
	```  
e. 使用 while 循环实现输出 1-100 内的所有偶数  

	```
	count =0
	while count <=100:
		if count %2==0:
			print(count)
		count +=1
	```  1. 现有如下两个变量,请简述 n1 和 n2 是什么关系?  	```	n1 = 123456	n2 = n1	```  2. 制作趣味模板程序（编程题）  需求：等待用户输入名字、地点、爱好，根据用户的名字和爱好进行任意显示如：敬爱可爱的xxx，最喜欢在xxx地方干xxx  
    
    ```
	答案：
		name = input("请输入姓名：")
		address = input("请输入地点：")
		hobby = input("请输入爱好：")
		print("敬爱可爱的 %s, 最喜欢在%s地方干%s" % (name, address, hobby))
    ```   
3. 输入一年份，判断该年份是否是闰年并输出结果。（编程题）  注：凡符合下面两个条件之一的年份是闰年。 （1） 能被4整除但不能被100整除。 （2） 能被400整除。  
     
	```  
	答案：
	def get_year():
		year = int(input("请输入年份："))
		if year % 4 == 0 and year % 100 != 0 or year % 400 == 0:
			print("%s 年是闰年" % year)
		else:
			print("%s 年不是闰年" % year)

	get_year()
	```  

4. 假设一年期定期利率为3.25%，计算一下需要过多少年，一万元的一年定期存款连本带息能翻番？（编程题）  

	```  
		money = 10000
		rate = 0.0325
		years = 0
		while money <= 20000:
			years += 1
			money  = money*(1+rate)
		print(str(years))
	```  


5. 一球从100米高度自由落下，每次落地后反跳回原高度的一半；再落下，求它在第10次落地时，共经过多少米？第10次反弹多高？

```
	count = 0
	height = 100
	meter = 0
	
	while count < 10:
	
	    meter +=  height #下落
	    height /= 2
	    meter += height  #反弹
	    count +=1
	    print(meter,height)
```
