## 本节重点

* 掌握封装，封装与扩展性
* 掌握property

> **本节时长需控制在15分钟内**

### **类中定义的函数分成两大类**

**一：绑定方法（绑定给谁，谁来调用就自动将它本身当作第一个参数传入）：**

1. 绑定到类的方法：用classmethod装饰器装饰的方法。

   ```
        为类量身定制

        类.boud_method(),自动将类当作第一个参数传入

      （其实对象也可调用，但仍将类当作第一个参数传入）
   ```

2. 绑定到对象的方法：没有被任何装饰器装饰的方法。

   ```
       为对象量身定制

       对象.boud_method(),自动将对象当作第一个参数传入

     （属于类的函数，类可以调用，但是必须按照函数的规则来，没有自动传值那么一说）
   ```

**二：非绑定方法：用staticmethod装饰器装饰的方法**

1. 不与类或对象绑定，类和对象都可以调用，但是没有自动传值那么一说。就是一个普通工具而已

注意：与绑定到对象方法区分开，在类中直接定义的函数，没有被任何装饰器装饰的，都是绑定到对象的方法，可不是普通函数，对象调用该方法会自动传值，而staticmethod装饰的方法，不管谁来调用，都没有自动传值一说

### 绑定方法

绑定给对象的方法（略）

绑定给类的方法（classmethod）

classmehtod是给类用的，即绑定到类，类在使用时会将类本身当做参数传给类方法的第一个参数（即便是对象来调用也会将类当作第一个参数传入），python为我们内置了函数classmethod来把类中的函数定义成类方法

```
#settings.py
HOST='127.0.0.1'
PORT=3306
DB_PATH=r'C:\Users\Administrator\PycharmProjects\test\面向对象编程\test1\db'

#test.py
import settings
class MySQL:
    def __init__(self,host,port):
        self.host=host
        self.port=port

    @classmethod
    def from_conf(cls):
        print(cls)
        return cls(settings.HOST,settings.PORT)

print(MySQL.from_conf) #<bound method MySQL.from_conf of <class '__main__.MySQL'>>
conn=MySQL.from_conf()

conn.from_conf() #对象也可以调用，但是默认传的第一个参数仍然是类
```

### 非绑定方法

在类内部用staticmethod装饰的函数即非绑定方法，就是普通函数

statimethod不与类或对象绑定，谁都可以调用，没有自动传值效果

```py
import hashlib
import time
class MySQL:
    def __init__(self,host,port):
        self.id=self.create_id()
        self.host=host
        self.port=port
    @staticmethod
    def create_id(): #就是一个普通工具
        m=hashlib.md5(str(time.time()).encode('utf-8'))
        return m.hexdigest()


print(MySQL.create_id) #<function MySQL.create_id at 0x0000000001E6B9D8> #查看结果为普通函数
conn=MySQL('127.0.0.1',3306)
print(conn.create_id) #<function MySQL.create_id at 0x00000000026FB9D8> #查看结果为普通函数
```

### classmethod与staticmethod的对比

```py
import settings
class MySQL:
    def __init__(self,host,port):
        self.host=host
        self.port=port

    @staticmethod
    def from_conf():
        return MySQL(settings.HOST,settings.PORT)

    # @classmethod #哪个类来调用,就将哪个类当做第一个参数传入
    # def from_conf(cls):
    #     return cls(settings.HOST,settings.PORT)

    def __str__(self):
        return '就不告诉你'

class Mariadb(MySQL):
    def __str__(self):
        return '<%s:%s>' %(self.host,self.port)


m=Mariadb.from_conf()
print(m) #我们的意图是想触发Mariadb.__str__,但是结果触发了MySQL.__str__的执行，打印就不告诉你：
```

### 练习

**练习1：定义MySQL类**

要求：

1.对象有id、host、port三个属性

2.定义工具create\_id，在实例化时为每个对象随机生成id，保证id唯一

3.提供两种实例化方式，方式一：用户传入host和port 方式二：从配置文件中读取host和port进行实例化

4.为对象定制方法，save和get\_obj\_by\_id，save能自动将对象序列化到文件中，文件路径为配置文件中DB\_PATH,文件名为id号，保存之前验证对象是否已经存在，若存在则抛出异常，;get\_obj\_by\_id方法用来从文件中反序列化出对象

