## 本节重点：

* 使学员掌握configparser模块的使用

> **本节时长需控制在15分钟内**



此模块用于生成和修改常见配置文档，当前模块的名称在 python 3.x 版本中变更为 configparser。

来看一个好多软件的常见配置文件格式如下

    ```cnf
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
    >>> import configparser # 导入模块
    >>> config = configparser.ConfigParser()  #实例化(生成对象)
    >>> config.sections()  #调用sections方法
    []
    >>> config.read('example.ini')  # 读配置文件(注意文件路径)
    ['example.ini']
    >>> config.sections() #调用sections方法(默认不会读取default)
    ['bitbucket.org', 'topsecret.server.com']
    >>> 'bitbucket.org' in config #判断元素是否在sections列表内
    True
    >>> 'bytebong.com' in config
    False
    >>> config['bitbucket.org']['User'] # 通过字典的形式取值
    'hg'
    >>> config['DEFAULT']['Compression']
    'yes'
    >>> topsecret = config['topsecret.server.com']
    >>> topsecret['ForwardX11']
    'no'
    >>> topsecret['Port']
    '50022'
    >>> for key in config['bitbucket.org']: print(key) # for循环 bitbucket.org 字典的key
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

    ```python
    [group1] # 支持的两种分隔符“=”, “:”
    k1 = v1
    k2:v2
    
    [group2]
    k1 = v1
    
    import ConfigParser
    
    config = ConfigParser.ConfigParser()
    config.read('i.cfg')
    
    # ########## 读 ##########
    #secs = config.sections()
    #print(secs)
    #options = config.options('group2') # 获取指定section的keys
    #print(options)
    
    #item_list = config.items('group2') # 获取指定 section 的 keys & values ,key value 以元组的形式
    #print(item_list)
    
    #val = config.get('group1','key') # 获取指定的key 的value
    #val = config.getint('group1','key')
    
    # ########## 改写 ##########
    #sec = config.remove_section('group1') # 删除section 并返回状态(true, false)
    #config.write(open('i.cfg', "w")) # 对应的删除操作要写入文件才会生效
    
    #sec = config.has_section('wupeiqi')
    #sec = config.add_section('wupeiqi')
    #config.write(open('i.cfg', "w")) # 
    
    
    #config.set('group2','k1',11111)
    #config.write(open('i.cfg', "w"))
    
    #config.remove_option('group2','age')
    #config.write(open('i.cfg', "w"))
    ```


