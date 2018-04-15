## **本章总结**

### 练习题

1. logging模块有几个日志级别？
2. 请配置logging模块，使其在屏幕和文件里同时打印以下格式的日志

   ```log
   2017-10-18 15:56:26,613 - access - ERROR - account [1234] too many login attempts
   ```

3. json、pickle、shelve三个区别是什么？
4. json的作用是什么？
5. subprocess执行命令方法有几种？
6. 为什么要设计好目录结构？
7. 打印出命令行的第一个参数。例如：

   ```shell
   python argument.py luffy
   打印出 luffy
   ```

8. 代码如下：

   ```python
   '''
   Linux当前目录/usr/local/nginx/html/
   文件名：index.html
   '''
   import os
   BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(index.html)))
   print(BASE_DIR)
   ```

   1. 打印的内容是什么？
   2. os.path.dirname和os.path.abspath含义是什么？

9. 通过configparser模块完成以下功能

   文件名my.cnf

   ```conf
   [DEFAULT]

   [client]
   port = 3306
   socket = /data/mysql_3306/mysql.sock

   [mysqld]
   explicit_defaults_for_timestamp = true
   port = 3306
   socket = /data/mysql_3306/mysql.sock
   back_log = 80
   basedir = /usr/local/mysql
   tmpdir = /tmp
   datadir = /data/mysql_3306
   default-time-zone = '+8:00'
   ```

   1. 修改时区 default-time-zone = '+8:00' 为 校准的全球时间 +00:00
   2. 删除 explicit\_defaults\_for\_timestamp = true
   3. 为DEFAULT增加一条 character-set-server = utf8

10. 写一个6位随机验证码程序（使用random模块\),要求验证码中至少包含一个数字、一个小写字母、一个大写字母.

11. 利用正则表达式提取到 luffycity.com ，内容如下

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
       <meta charset="UTF-8">
       <title>luffycity.com</title>
    </head>
    <body>
    </body>
    </html>
    ```

12. 写一个用户登录验证程序，文件如下  
    1234.json

    ```python
    {"expire_date": "2021-01-01", "id": 1234, "status": 0, "pay_day": 22, "password": "abc"}
    ```

    1. 用户名为json文件名，密码为 password。
    2. 判断是否过期，与expire\_date进行对比。
    3. 登陆成功后，打印“登陆成功”，三次登陆失败，status值改为1，并且锁定账号。

13. 把第12题三次验证的密码进行hashlib加密处理。即：json文件保存为md5的值，然后用md5的值进行验证。

14. 最近luffy买了个tesla，通过转账的形式，并且支付了5%的手续费，tesla价格为75万。文件为json，请用程序实现该转账行为。  
    需求如下：  
    1. 目录结构为

    ```
    .
    ├── account
    │   ├── luffy.json
    │   └── tesla.json
    └── bin
          └── start.py
    ```

    当执行start.py时，出现交互窗口

    ```
       ------- Luffy Bank ---------
      1.  账户信息
      2.  转账
    ```

    * 选择1 账户信息   显示luffy的当前账户余额。
    * 选择2 转账       直接扣掉75万和利息费用并且tesla账户增加75万

15. 对上题增加一个需求：提现。  
    目录结构如下

    ```
    .
    ├── account
    │   └── luffy.json
    ├── bin
    │   └── start.py
    └── core
       └── withdraw.py
    ```

    当执行start.py时，出现交互窗口

    ```
       ------- Luffy Bank ---------
    1.  账户信息
    2.  提现
    ```

    * 选择1 账户信息   显示luffy的当前账户余额和信用额度。
    * 选择2 提现      提现金额应小于等于信用额度，利息为5%，提现金额为用户自定义。

16. 尝试把上一章的验证用户登陆的装饰器添加到提现和转账的功能上。

17. 对第15题的用户转账、登录、提现操作均通过logging模块记录日志,日志文件位置如下
    ```
     .
     ├── account
     │   └── luffy.json
     ├── bin
     │   └── start.py
     └── core
     |   └── withdraw.py
     └── logs
         └── bank.log
    ```

### 

### 本章作业：

**模拟实现一个ATM + 购物商城程序**

1. 额度 15000或自定义
2. 实现购物商城，买东西加入 购物车，调用信用卡接口结账
3. 可以提现，手续费5%
4. 支持多账户登录
5. 支持账户间转账
6. 记录每月日常消费流水
7. 提供还款接口
8. ATM记录操作日志 
9. 提供管理接口，包括添加账户、用户额度，冻结账户等。。。
10. 用户认证用装饰器

示例代码 [https://github.com/triaquae/py3\_training/tree/master/atm](https://github.com/triaquae/py3_training/tree/master/atm)

简易流程图：[https://www.processon.com/view/link/589eb841e4b0999184934329](https://www.processon.com/view/link/589eb841e4b0999184934329)

