## 本节重点：

* 使学员掌握configparser模块的使用

> **本节时长需控制在15分钟内**



此模块用于生成和修改常见配置文档，当前模块的名称在 python 3.x 版本中变更为 configparser。

来看一个好多软件的常见配置文件格式如下

```
[DEFAULT]
ServerAliveInterval = 45
Compression = yes
CompressionLevel = 9
ForwardX11 = yes

[bitbucket.org]
User = hg

[topsecret.server.com]
Port = 50022
ForwardX11 = no
```

解析配置文件

```py
>>> import configparser
>>> config = configparser.ConfigParser()
>>> config.sections()
[]
>>> config.read('example.ini')
['example.ini']
>>> config.sections()
['bitbucket.org', 'topsecret.server.com']
>>> 'bitbucket.org' in config
True
>>> 'bytebong.com' in config
False
>>> config['bitbucket.org']['User']
'hg'
>>> config['DEFAULT']['Compression']
'yes'
>>> topsecret = config['topsecret.server.com']
>>> topsecret['ForwardX11']
'no'
>>> topsecret['Port']
'50022'
>>> for key in config['bitbucket.org']: print(key)
...
user
compressionlevel
serveraliveinterval
compression
forwardx11
>>> config['bitbucket.org']['ForwardX11']
'yes'
```

其它增删改查语法

```
[group1]
k1 = v1
k2:v2

[group2]
k1 = v1

import ConfigParser

config = ConfigParser.ConfigParser()
config.read('i.cfg')

# ########## 读 ##########
#secs = config.sections()
#print secs
#options = config.options('group2')
#print options

#item_list = config.items('group2')
#print item_list

#val = config.get('group1','key')
#val = config.getint('group1','key')

# ########## 改写 ##########
#sec = config.remove_section('group1')
#config.write(open('i.cfg', "w"))

#sec = config.has_section('wupeiqi')
#sec = config.add_section('wupeiqi')
#config.write(open('i.cfg', "w"))


#config.set('group2','k1',11111)
#config.write(open('i.cfg', "w"))

#config.remove_option('group2','age')
#config.write(open('i.cfg', "w"))
```



