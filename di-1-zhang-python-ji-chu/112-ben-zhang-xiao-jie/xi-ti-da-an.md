第一章,章节练习
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
 

	```
	 答:
	 1、./run.py.shell直接调用python脚本  

	2、python run.py 调用python 解释器来调用python脚本  
	```     


	```  
	 答:
	 1, 单行注释使用 # 号
	 2, 多行注释使用 “”“”“”  ‘’‘’‘’
	```   

	 
	```
	 答:
	 [] () {} 0 False
	```   


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
 
 
	```
	id
	```  


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


	```
	count =0
	while count <=100:
		if count %2!=0:
			print(count)
		count +=1
	```  


	```
	count =0
	while count <=100:
		if count %2==0:
			print(count)
		count +=1
	```  
    
    ```
	答案：
		name = input("请输入姓名：")
		address = input("请输入地点：")
		hobby = input("请输入爱好：")
		print("敬爱可爱的 %s, 最喜欢在%s地方干%s" % (name, address, hobby))
    ```   

     
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

