## 本节重点：

* 使学员掌握hashlib模块的使用

> **本节时长需控制在15分钟内**



用于加密相关的操作，3.x里代替了md5模块和sha模块，主要提供 SHA1, SHA224, SHA256, SHA384, SHA512 ，MD5 算法

```py
import hashlib
 
m = hashlib.md5()
m.update(b"Hello")
m.update(b"It's me")
print(m.digest())
m.update(b"It's been a long time since last time we ...")
 
print(m.digest()) #2进制格式hash
print(len(m.hexdigest())) #16进制格式hash
'''
def digest(self, *args, **kwargs): # real signature unknown
    """ Return the digest value as a string of binary data. """
    pass
 
def hexdigest(self, *args, **kwargs): # real signature unknown
    """ Return the digest value as a string of hexadecimal digits. """
    pass
 
'''
import hashlib
 
# ######## md5 ########
 
hash = hashlib.md5()
hash.update('admin')
print(hash.hexdigest())
 
# ######## sha1 ########
 
hash = hashlib.sha1()
hash.update('admin')
print(hash.hexdigest())
 
# ######## sha256 ########
 
hash = hashlib.sha256()
hash.update('admin')
print(hash.hexdigest())
 
 
# ######## sha384 ########
 
hash = hashlib.sha384()
hash.update('admin')
print(hash.hexdigest())
 
# ######## sha512 ########
 
hash = hashlib.sha512()
hash.update('admin')
print(hash.hexdigest())
```



