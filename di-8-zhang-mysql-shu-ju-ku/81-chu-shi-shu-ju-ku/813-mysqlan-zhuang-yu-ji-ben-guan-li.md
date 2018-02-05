## 本节重点

* 掌握mysql的安装、启动、破解密码、统一字符编码

> **本节时长需控制在15分钟内**

### 一、MySQL介绍

MySQL是一个关系型数据库管理系统，由瑞典MySQL AB 公司开发，目前属于 Oracle 旗下公司。MySQL 最流行的关系型数据库管理系统，在 WEB 应用方面MySQL是最好的 RDBMS \(Relational Database Management System，关系数据库管理系统\) 应用软件之一。

**mysql是什么**

```
mysql就是一个基于socket编写的C/S架构的软件

客户端软件
　　mysql自带：如mysql命令，mysqldump命令等
　　python模块：如pymysql
```

**数据库管理软件分类**

```
分两大类：
　　关系型：如sqllite，db2，oracle，access，sql server，MySQL，注意：sql语句通用
　　非关系型：mongodb，redis，memcache

可以简单的理解为：
    关系型数据库需要有表结构
    非关系型数据库是key-value存储的，没有表结构
```

### 二、下载安装

**Linux版本**

```
#二进制rpm包安装
yum -y install mysql-server mysql
```

源码安装见：[http://www.cnblogs.com/linhaifeng/articles/7126847.html](http://www.cnblogs.com/linhaifeng/articles/7126847.html)

**Window版本**

```
#1、下载：MySQL Community Server 5.7.16
http://dev.mysql.com/downloads/mysql/

#2、解压
如果想要让MySQL安装在指定目录，那么就将解压后的文件夹移动到指定目录，如：C:\mysql-5.7.16-winx64

#3、添加环境变量
【右键计算机】--》【属性】--》【高级系统设置】--》【高级】--》【环境变量】--》【在第二个内容框中找到 变量名为Path 的一行，双击】 --> 【将MySQL的bin目录路径追加到变值值中，用 ； 分割】

#4、初始化
mysqld --initialize-insecure

#5、启动MySQL服务
mysqld # 启动MySQL服务

#6、启动MySQL客户端并连接MySQL服务
mysql -u root -p # 连接MySQL服务器
```

上一步解决了一些问题，但不够彻底，因为在执行【mysqd】启动MySQL服务器时，当前终端会被hang住，那么做一下设置即可解决此问题,即将MySQL服务制作成windows服务

```
注意：--install前，必须用mysql启动命令的绝对路径
# 制作MySQL的Windows服务，在终端执行此命令：
"c:\mysql-5.7.16-winx64\bin\mysqld" --install

# 移除MySQL的Windows服务，在终端执行此命令：
"c:\mysql-5.7.16-winx64\bin\mysqld" --remove


注册成服务之后，以后再启动和关闭MySQL服务时，仅需执行如下命令：
# 启动MySQL服务
net start mysql

# 关闭MySQL服务
net stop mysql
```

### 三、MySQL启动与查看

linux平台下查看

```
[root@egon ~]# systemctl start mariadb #启动
[root@egon ~]# systemctl enable mariadb #设置开机自启动
Created symlink from /etc/systemd/system/multi-user.target.wants/mariadb.service to /usr/lib/systemd/system/mariadb.service.
[root@egon ~]# ps aux |grep mysqld |grep -v grep #查看进程，mysqld_safe为启动mysql的脚本文件，内部调用mysqld命令
mysql     3329  0.0  0.0 113252  1592 ?        Ss   16:19   0:00 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
mysql     3488  0.0  2.3 839276 90380 ?        Sl   16:19   0:00 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --log-error=/var/log/mariadb/mariadb.log --pid-file=/var/run/mariadb/mariadb.pid --socket=/var/lib/mysql/mysql.sock
[root@egon ~]# netstat -an |grep 3306 #查看端口
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN  
[root@egon ~]# ll -d /var/lib/mysql #权限不对，启动不成功，注意user和group
drwxr-xr-x 5 mysql mysql 4096 Jul 20 16:28 /var/lib/mysql
```

You must reset your password using ALTER USER statement before executing this statement.

```
安装完mysql 之后，登陆以后，不管运行任何命令，总是提示这个
mac mysql error You must reset your password using ALTER USER statement before executing this statement.
解决方法：
step 1: SET PASSWORD = PASSWORD('your new password');
step 2: ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
step 3: flush privileges;
```

windows平台到服务中查看即可

### 三、登录设置密码

```
初始状态下，管理员root，密码为空，默认只允许从本机登录localhost
设置密码
[root@egon ~]# mysqladmin -uroot password "123"        设置初始密码 由于原密码为空，因此-p可以不用
[root@egon ~]# mysqladmin -uroot -p"123" password "456"        修改mysql密码,因为已经有密码了，所以必须输入原密码才能设置新密码

命令格式:
[root@egon ~]# mysql -h172.31.0.2 -uroot -p456
[root@egon ~]# mysql -uroot -p
[root@egon ~]# mysql                    以root用户登录本机，密码为空
```

### 三、破解密码

**linux平台下，破解密码的两种方式**

方法一：删除授权库mysql，重新初始化

```
[root@egon ~]# rm -rf /var/lib/mysql/mysql #所有授权信息全部丢失！！！
[root@egon ~]# systemctl restart mariadb
[root@egon ~]# mysql
```

方法二：启动时，跳过授权库

```
[root@egon ~]# vim /etc/my.cnf    #mysql主配置文件
[mysqld]
skip-grant-table
[root@egon ~]# systemctl restart mariadb
[root@egon ~]# mysql
MariaDB [(none)]> update mysql.user set password=password("123") where user="root" and host="localhost";
MariaDB [(none)]> flush privileges;
MariaDB [(none)]> \q
[root@egon ~]# #打开/etc/my.cnf去掉skip-grant-table,然后重启
[root@egon ~]# systemctl restart mariadb
[root@egon ~]# mysql -u root -p123 #以新密码登录
```

**windows平台下，5.7版本mysql，破解密码的两种方式：**

方式一

```
#1 关闭mysql
#2 在cmd中执行：mysqld --skip-grant-tables
#3 在cmd中执行：mysql
#4 执行如下sql：
update mysql.user set authentication_string=password('') where user = 'root';
flush privileges;

#5 tskill mysqld #或taskkill -f /PID 7832
#6 重新启动mysql
```

 方式二

```
#1. 关闭mysql，可以用tskill mysqld将其杀死
#2. 在解压目录下，新建mysql配置文件my.ini
#3. my.ini内容,指定
[mysqld]
skip-grant-tables

#4.启动mysqld
#5.在cmd里直接输入mysql登录，然后操作
update mysql.user set authentication_string=password('') where user='root and host='localhost';

flush privileges;

#6.注释my.ini中的skip-grant-tables，然后启动myqsld，然后就可以以新密码登录了
```

### 四、统一字符编码

**强调：配置文件中的注释可以有中文，但是配置项中不能出现中文**

```
#在mysql的解压目录下，新建my.ini,然后配置
#1. 在执行mysqld命令时，下列配置会生效，即mysql服务启动时生效
[mysqld]
;skip-grant-tables
port=3306
character_set_server=utf8
default-storage-engine=innodb
innodb_file_per_table=1


#解压的目录
basedir=E:\mysql-5.7.19-winx64
#data目录
datadir=E:\my_data #在mysqld --initialize时，就会将初始数据存入此处指定的目录，在初始化之后，启动mysql时，就会去这个目录里找数据



#2. 针对客户端命令的全局配置，当mysql客户端命令执行时，下列配置生效
[client]
port=3306
default-character-set=utf8
user=root
password=123

#3. 只针对mysql这个客户端的配置，2中的是全局配置，而此处的则是只针对mysql这个命令的局部配置
[mysql]
;port=3306
;default-character-set=utf8
user=egon
password=4573


#！！！如果没有[mysql],则用户在执行mysql命令时的配置以[client]为准
```

**统一字符编码**

```
#1. 修改配置文件
[mysqld]
default-character-set=utf8 
[client]
default-character-set=utf8 
[mysql]
default-character-set=utf8

#mysql5.5以上：修改方式有所改动
[mysqld]
character-set-server=utf8
collation-server=utf8_general_ci
[client]
default-character-set=utf8
[mysql]
default-character-set=utf8

#2. 重启服务
#3. 查看修改结果：
\s
show variables like '%char%'
```



