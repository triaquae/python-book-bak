### 从代码级别看面向对象

数据与专门操作该数据的功能组合到一起

```py
#1、在没有学习类这个概念时，数据与功能是分离的
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


#2、我们能想到的解决方法是，把这些变量都定义成全局变量
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


#3、但是2的解决方法也是有问题的，按照2的思路，我们将会定义一大堆全局变量，这些全局变量并没有做任何区分，即能够被所有功能使用，
然而事实上只有HOST，PORT，DB，CHARSET是给exc1和exc2这两个功能用的。
言外之意：我们必须找出一种能够将数据与操作数据的方法组合到一起的解决方法，这就是我们说的类了
class MySQLHandler:
    def __init__(self,host,port,db,charset='utf8'):
        self.host=host
        self.port=port
        self.db=db
        self.charset=charset
    def exc1(self,sql):
        conn=connect(self.host,self.port,self.db,self.charset)
        res=conn.execute(sql)
        return res


    def exc2(self,sql):
        conn=connect(self.host,self.port,self.db,self.charset)
        res=conn.call_proc(sql)
        return res


obj=MySQLHandler('127.0.0.1',3306,'db1')
obj.exc1('select * from tb1;')
obj.exc2('存储过程的名字')


#改进
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



