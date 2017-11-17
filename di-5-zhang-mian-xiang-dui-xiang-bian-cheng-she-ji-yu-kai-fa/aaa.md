## 本节重点

* 总结面向对象的优点

> **本节时长需控制在10分钟内**

### 从代码级别看面向对象

1、在没有学习类这个概念时，数据与功能是分离的

```py
def exc1(host,port,db,charset):
    conn=connect(host,port,db,charset)
    conn.execute(sql)
    return xxx


def exc2(host,port,db,charset,proc_name)
    conn=connect(host,port,db,charset)
    conn.call_proc(sql)
    return xxx

#每次调用都需要重复传入一堆参数
exc1('127.0.0.1',3306,'db1','utf8','select * from tb1;')
exc2('127.0.0.1',3306,'db1','utf8','存储过程的名字')
```

2、我们能想到的解决方法是，把这些变量都定义成全局变量

```py
HOST=‘127.0.0.1’
PORT=3306
DB=‘db1’
CHARSET=‘utf8’

def exc1(host,port,db,charset):
    conn=connect(host,port,db,charset)
    conn.execute(sql)
    return xxx


def exc2(host,port,db,charset,proc_name)
    conn=connect(host,port,db,charset)
    conn.call_proc(sql)
    return xxx

exc1(HOST,PORT,DB,CHARSET,'select * from tb1;')
exc2(HOST,PORT,DB,CHARSET,'存储过程的名字')
```

3、但是2的解决方法也是有问题的，按照2的思路，我们将会定义一大堆全局变量，这些全局变量并没有做任何区分，即能够被所有功能使用，然而事实上只有HOST，PORT，DB，CHARSET是给exc1和exc2这两个功能用的。言外之意：我们必须找出一种能够将数据与操作数据的方法组合到一起的解决方法，这就是我们说的类了

```py
class MySQLHandler:
    def __init__(self,host,port,db,charset='utf8'):
        self.host=host
        self.port=port
        self.db=db
        self.charset=charset
        self.conn=connect(self.host,self.port,self.db,self.charset)
    def exc1(self,sql):
        return self.conn.execute(sql)

    def exc2(self,sql):
        return self.conn.call_proc(sql)


obj=MySQLHandler('127.0.0.1',3306,'db1')
obj.exc1('select * from tb1;')
obj.exc2('存储过程的名字')
```

总结使用类可以：

```
 将数据与专门操作该数据的功能整合到一起。
```

## 可扩展性高

定义类并产生三个对象

```py
class Chinese:
    def __init__(self,name,age,sex):
        self.name=name
        self.age=age
        self.sex=sex


p1=Chinese('egon',18,'male')
p2=Chinese('alex',38,'female')
p3=Chinese('wpq',48,'female')
```

如果我们新增一个类属性，将会立刻反映给所有对象，而对象却无需修改

```py
class Chinese:
    country='China'
    def __init__(self,name,age,sex):
        self.name=name
        self.age=age
        self.sex=sex
    def tell_info(self):
        info='''
        国籍:%s
        姓名:%s
        年龄:%s
        性别:%s
        ''' %(self.country,self.name,self.age,self.sex)
        print(info)


p1=Chinese('egon',18,'male')
p2=Chinese('alex',38,'female')
p3=Chinese('wpq',48,'female')

print(p1.country)
p1.tell_info()
```



