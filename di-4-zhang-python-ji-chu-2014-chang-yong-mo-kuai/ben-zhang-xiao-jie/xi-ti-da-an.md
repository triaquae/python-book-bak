## 练习题答案

1. logging模块有几个日志级别？

  ```python
  答案
    logging模块共5个级别，它们分别是：
    DEBUG INFO WARNING ERROR CRITICAL
  ```

2. 请配置logging模块，使其在屏幕和文件里同时打印以下格式的日志

  ```log
  2017-10-18 15:56:26,613 - access - ERROR - account [1234] too many login attempts
  ```

  ```python

  ```

3. json、pickle、shelve三个区别是什么？

  ```python
  答案
    首先，这三个模块都是序列化工具。
    1. json是所有语言的序列化工具,优点跨语言、体积小.只能序列化一些基本的数据类型。int\str\list\tuple\dict
    pickle是python语言特有序列化工具，所有数据都能序列化。只能在python中使用，存储数据占空间大.
    shelve模块是一个简单的k,v将内存数据通过文件持久化的模块，可以持久化任何pickle可支持的python数据格式。
    2. 使用方式，json和pickle用法一样，shelve是f = shelve.open('shelve_test')
  ```

4. json的作用是什么？

  ```python
  答案：
    序列化是指把内存里的数据类型转变成字符串，以使其能存储到硬盘或通过网络传输到远程，因为硬盘或网络传输时只能接受bytes
  ```

5. subprocess执行命令方法有几种？

  ```python
  答案吧：有三种方法，他们分别是
    run()方法
    call()方法
    Popen()方法
  ```

6. 为什么要设计好目录结构？

  ```python
  答案：
  1.可读性高: 不熟悉这个项目的代码的人，一眼就能看懂目录结构，知道程序启动脚本是哪个，测试目录在哪儿，配置文件在哪儿等等。从而非常快速的了解这个项目。
  2.可维护性高: 定义好组织规则后，维护者就能很明确地知道，新增的哪个文件和代码应该放在什么目录之下。这个好处是，随着时间的推移，代码/配置的规模增加，项目结构不会混乱，仍然能够组织良好。
  ```

7. 打印出命令行的第一个参数。例如：

  ```shell
  python argument.py luffy
  打印出 luffy
  ```

  ```python
  答案：
  import sys
  print(sys.argv[1])
  ```

8. 代码如下：

  ```python
  '''
  Linux当前目录/usr/local/nginx/html/
  文件名：index.html
  '''
  import os
  BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath('index.html')))
  print(BASE_DIR)
  ```

1. 打印的内容是什么？

  ```python
  答案
  /usr/local/nginx
  ```
  
2. os.path.dirname和os.path.abspath含义是什么？

  ```python
  答案
  os.path.dirname：指定文件的目录
  os.path.abspath：指定文件的绝对路径
  ```

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

  ```python
  答案
  import configparser
  config = configparser.ConfigParser()
  config.read('my.cnf')
  config.set('mysqld','default-time-zone','+00:00')
  config.write(open('my.cnf', "w"))
  print(config['mysqld']['default-time-zone'] )
  ```

2. 删除 explicit\_defaults\_for\_timestamp = true

  ```python
  import configparser
  config = configparser.ConfigParser()
  config.read('my.cnf')
  config.remove_option('mysqld','explicit_defaults_for_timestamp')
  config.write(open('my.cnf', "w"))
  ```

3. 为DEFAULT增加一条 character-set-server = utf8

  ```python
  答案：
  import configparser
  config = configparser.ConfigParser()
  config.read('my.cnf')
  config.set('DEFAULT','character-set-server','utf8')
  config.write(open('my.cnf', "w"))
  ```

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

  ```python
  import re
  f = open('index.html','r',encoding='utf-8')
  data = f.read()
  print(re.findall('luffycity.com',data))
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
  │ ├── luffy.json
  │ └── tesla.json
  └── bin
  └── start.py
  ```

当执行start.py时，出现交互窗口

  ```
  ------- Luffy Bank ---------
  1. 账户信息
  2. 转账
  ```

* 选择1 账户信息 显示luffy的当前账户余额。
* 选择2 转账 直接扣掉75万和利息费用并且tesla账户增加75万

15. 对上题增加一个需求：提现。
目录结构如下

  ```
  .
  ├── account
  │ └── luffy.json
  ├── bin
  │ └── start.py
  └── core
  └── withdraw.py
  ```

当执行start.py时，出现交互窗口

  ```
  ------- Luffy Bank ---------
  1. 账户信息
  2. 提现
  ```

* 选择1 账户信息 显示luffy的当前账户余额和信用额度。
* 选择2 提现 提现金额应小于等于信用额度，利息为5%，提现金额为用户自定义。

16. 尝试把上一章的验证用户登陆的装饰器添加到提现和转账的功能上。

17. 对第15题的用户转账、登录、提现操作均通过logging模块记录日志,日志文件位置如下

  ```
  .
  ├── account
  │ └── luffy.json
  ├── bin
  │ └── start.py
  └── core
  | └── withdraw.py
  └── logs
  └── bank.log
  ```
