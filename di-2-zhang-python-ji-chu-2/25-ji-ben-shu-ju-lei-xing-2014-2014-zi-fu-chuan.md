## 本节重点

1.让学员理解字符串数据类型出现的意义

2.让学员掌握字符串的定义和特性

3.学员能熟练掌握字符串常用操作，并了解其他工厂方法

4.教会学生看源码技能

## 字符串的定义与创建

字符串是一个有序的字符的集合，用于存储和表示基本的文本信息，' '或'' ''或''' '''中间包含的内容称之为字符串

**创建：**

```py
 s = 'Hello,Eva！How are you?'
```

## 字符串的特性与常用操作

特性：

1.按照从左到右的顺序定义字符集合，下标从0开始顺序访问，有序

![](/assets/str索引图.png)

补充：

1.字符串的单引号和双引号都无法取消特殊字符的含义，如果想让引号内所有字符均取消特殊意义，在引号前面加r，如name＝r'l\thf'

2.unicode字符串与r连用必需在r前面，如name＝ur'l\thf'

**常用操作：**

```py
#索引
s = 'hello'
>>> s[1]
'e'
>>> s[-1]
'o'


>>> s.index('e')
1


#查找
>>> s.find('e')
1
>>> s.find('i')
-1


#移除空白
s = '  hello,world!  '
s.strip()
s.lstrip()
s.rstrip()
s2 = '***hello,world!***'
s2.strip('*')

#长度
>>> s = 'hello,world'
>>> len(s)
11

#替换
>>> s = 'hello world'
>>> s.replace('h','H')
'Hello world'
>>> s2 = 'hi，how are you？'
>>> s2.replace('h','H')
'Hi，How are you？'

#切片
>>> s = 'abcdefghigklmn'
>>> s[0:7]
'abcdefg'
>>> s[7:14]
'higklmn'
>>> s[:7]
'abcdefg'
>>> s[7:]
'higklmn'
>>> s[:]
'abcdefghigklmn'
>>> s[0:7:2]
'aceg'
>>> s[7:14:3]
'hkn'
>>> s[::2]
'acegikm'
>>> s[::-1]
'nmlkgihgfedcba'
```

## 字符串的工厂函数

> 教会学员看源码

```py
class str(object):
    """
    str(object='') -> str
    str(bytes_or_buffer[, encoding[, errors]]) -> str

    Create a new string object from the given object. If encoding or
    errors is specified, then the object must expose a data buffer
    that will be decoded using the given encoding and error handler.
    Otherwise, returns the result of object.__str__() (if defined)
    or repr(object).
    encoding defaults to sys.getdefaultencoding().
    errors defaults to 'strict'.
    """
    def capitalize(self): # real signature unknown; restored from __doc__
        """
        首字母变大写
        S.capitalize() -> str

        Return a capitalized version of S, i.e. make the first character
        have upper case and the rest lower case.
        """
        return ""

    def casefold(self): # real signature unknown; restored from __doc__
        """
        S.casefold() -> str

        Return a version of S suitable for caseless comparisons.
        """
        return ""

    def center(self, width, fillchar=None): # real signature unknown; restored from __doc__
        """
        原来字符居中，不够用空格补全
        S.center(width[, fillchar]) -> str

        Return S centered in a string of length width. Padding is
        done using the specified fill character (default is a space)
        """
        return ""

    def count(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
         从一个范围内的统计某str出现次数
        S.count(sub[, start[, end]]) -> int

        Return the number of non-overlapping occurrences of substring sub in
        string S[start:end].  Optional arguments start and end are
        interpreted as in slice notation.
        """
        return 0

    def encode(self, encoding='utf-8', errors='strict'): # real signature unknown; restored from __doc__
        """
        encode(encoding='utf-8',errors='strict')
        以encoding指定编码格式编码，如果出错默认报一个ValueError，除非errors指定的是
        ignore或replace

        S.encode(encoding='utf-8', errors='strict') -> bytes

        Encode S using the codec registered for encoding. Default encoding
        is 'utf-8'. errors may be given to set a different error
        handling scheme. Default is 'strict' meaning that encoding errors raise
        a UnicodeEncodeError. Other possible values are 'ignore', 'replace' and
        'xmlcharrefreplace' as well as any other name registered with
        codecs.register_error that can handle UnicodeEncodeErrors.
        """
        return b""

    def endswith(self, suffix, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.endswith(suffix[, start[, end]]) -> bool

        Return True if S ends with the specified suffix, False otherwise.
        With optional start, test S beginning at that position.
        With optional end, stop comparing S at that position.
        suffix can also be a tuple of strings to try.
        """
        return False

    def expandtabs(self, tabsize=8): # real signature unknown; restored from __doc__
        """
        将字符串中包含的\t转换成tabsize个空格
        S.expandtabs(tabsize=8) -> str

        Return a copy of S where all tab characters are expanded using spaces.
        If tabsize is not given, a tab size of 8 characters is assumed.
        """
        return ""

    def find(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.find(sub[, start[, end]]) -> int

        Return the lowest index in S where substring sub is found,
        such that sub is contained within S[start:end].  Optional
        arguments start and end are interpreted as in slice notation.

        Return -1 on failure.
        """
        return 0

    def format(self, *args, **kwargs): # known special case of str.format
        """
        格式化输出
        三种形式：
        形式一.
        >>> print('{0}{1}{0}'.format('a','b'))
        aba

        形式二：（必须一一对应）
        >>> print('{}{}{}'.format('a','b'))
        Traceback (most recent call last):
          File "<input>", line 1, in <module>
        IndexError: tuple index out of range
        >>> print('{}{}'.format('a','b'))
        ab

        形式三：
        >>> print('{name} {age}'.format(age=12,name='lhf'))
        lhf 12

        S.format(*args, **kwargs) -> str

        Return a formatted version of S, using substitutions from args and kwargs.
        The substitutions are identified by braces ('{' and '}').
        """
        pass

    def format_map(self, mapping): # real signature unknown; restored from __doc__
        """
        与format区别
        '{name}'.format(**dict(name='alex'))
        '{name}'.format_map(dict(name='alex'))

        S.format_map(mapping) -> str

        Return a formatted version of S, using substitutions from mapping.
        The substitutions are identified by braces ('{' and '}').
        """
        return ""

    def index(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.index(sub[, start[, end]]) -> int

        Like S.find() but raise ValueError when the substring is not found.
        """
        return 0

    def isalnum(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是字母或数字才返回True

        S.isalnum() -> bool

        Return True if all characters in S are alphanumeric
        and there is at least one character in S, False otherwise.
        """
        return False

    def isalpha(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是字母才返回True
        S.isalpha() -> bool

        Return True if all characters in S are alphabetic
        and there is at least one character in S, False otherwise.
        """
        return False

    def isdecimal(self): # real signature unknown; restored from __doc__
        """
        S.isdecimal() -> bool

        Return True if there are only decimal characters in S,
        False otherwise.
        """
        return False

    def isdigit(self): # real signature unknown; restored from __doc__
        """
        S.isdigit() -> bool

        Return True if all characters in S are digits
        and there is at least one character in S, False otherwise.
        """
        return False

    def isidentifier(self): # real signature unknown; restored from __doc__
        """
        字符串为关键字返回True

        S.isidentifier() -> bool

        Return True if S is a valid identifier according
        to the language definition.

        Use keyword.iskeyword() to test for reserved identifiers
        such as "def" and "class".
        """
        return False

    def islower(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是小写字母才返回True
        S.islower() -> bool

        Return True if all cased characters in S are lowercase and there is
        at least one cased character in S, False otherwise.
        """
        return False

    def isnumeric(self): # real signature unknown; restored from __doc__
        """
        S.isnumeric() -> bool

        Return True if there are only numeric characters in S,
        False otherwise.
        """
        return False

    def isprintable(self): # real signature unknown; restored from __doc__
        """
        S.isprintable() -> bool

        Return True if all characters in S are considered
        printable in repr() or S is empty, False otherwise.
        """
        return False

    def isspace(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是空格才返回True
        S.isspace() -> bool

        Return True if all characters in S are whitespace
        and there is at least one character in S, False otherwise.
        """
        return False

    def istitle(self): # real signature unknown; restored from __doc__
        """
        >>> a='Hello'
        >>> a.istitle()
        True
        >>> a='HellP'
        >>> a.istitle()
        False

        S.istitle() -> bool

        Return True if S is a titlecased string and there is at least one
        character in S, i.e. upper- and titlecase characters may only
        follow uncased characters and lowercase characters only cased ones.
        Return False otherwise.
        """
        return False

    def isupper(self): # real signature unknown; restored from __doc__
        """
        S.isupper() -> bool

        Return True if all cased characters in S are uppercase and there is
        at least one cased character in S, False otherwise.
        """
        return False

    def join(self, iterable): # real signature unknown; restored from __doc__
        """
        #对序列进行操作（分别使用' '与':'作为分隔符）
        >>> seq1 = ['hello','good','boy','doiido']
        >>> print ' '.join(seq1)
        hello good boy doiido
        >>> print ':'.join(seq1)
        hello:good:boy:doiido


        #对字符串进行操作

        >>> seq2 = "hello good boy doiido"
        >>> print ':'.join(seq2)
        h:e:l:l:o: :g:o:o:d: :b:o:y: :d:o:i:i:d:o


        #对元组进行操作

        >>> seq3 = ('hello','good','boy','doiido')
        >>> print ':'.join(seq3)
        hello:good:boy:doiido


        #对字典进行操作

        >>> seq4 = {'hello':1,'good':2,'boy':3,'doiido':4}
        >>> print ':'.join(seq4)
        boy:good:doiido:hello


        #合并目录

        >>> import os
        >>> os.path.join('/hello/','good/boy/','doiido')
        '/hello/good/boy/doiido'


        S.join(iterable) -> str

        Return a string which is the concatenation of the strings in the
        iterable.  The separator between elements is S.
        """
        return ""

    def ljust(self, width, fillchar=None): # real signature unknown; restored from __doc__
        """
        S.ljust(width[, fillchar]) -> str

        Return S left-justified in a Unicode string of length width. Padding is
        done using the specified fill character (default is a space).
        """
        return ""

    def lower(self): # real signature unknown; restored from __doc__
        """
        S.lower() -> str

        Return a copy of the string S converted to lowercase.
        """
        return ""

    def lstrip(self, chars=None): # real signature unknown; restored from __doc__
        """
        S.lstrip([chars]) -> str

        Return a copy of the string S with leading whitespace removed.
        If chars is given and not None, remove characters in chars instead.
        """
        return ""

    def maketrans(self, *args, **kwargs): # real signature unknown
        """
        Return a translation table usable for str.translate().

        If there is only one argument, it must be a dictionary mapping Unicode
        ordinals (integers) or characters to Unicode ordinals, strings or None.
        Character keys will be then converted to ordinals.
        If there are two arguments, they must be strings of equal length, and
        in the resulting dictionary, each character in x will be mapped to the
        character at the same position in y. If there is a third argument, it
        must be a string, whose characters will be mapped to None in the result.
        """
        pass

    def partition(self, sep): # real signature unknown; restored from __doc__
        """
        以sep为分割，将S分成head,sep,tail三部分

        S.partition(sep) -> (head, sep, tail)

        Search for the separator sep in S, and return the part before it,
        the separator itself, and the part after it.  If the separator is not
        found, return S and two empty strings.
        """
        pass

    def replace(self, old, new, count=None): # real signature unknown; restored from __doc__
        """
        S.replace(old, new[, count]) -> str

        Return a copy of S with all occurrences of substring
        old replaced by new.  If the optional argument count is
        given, only the first count occurrences are replaced.
        """
        return ""

    def rfind(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.rfind(sub[, start[, end]]) -> int

        Return the highest index in S where substring sub is found,
        such that sub is contained within S[start:end].  Optional
        arguments start and end are interpreted as in slice notation.

        Return -1 on failure.
        """
        return 0

    def rindex(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.rindex(sub[, start[, end]]) -> int

        Like S.rfind() but raise ValueError when the substring is not found.
        """
        return 0

    def rjust(self, width, fillchar=None): # real signature unknown; restored from __doc__
        """
        S.rjust(width[, fillchar]) -> str

        Return S right-justified in a string of length width. Padding is
        done using the specified fill character (default is a space).
        """
        return ""

    def rpartition(self, sep): # real signature unknown; restored from __doc__
        """
        S.rpartition(sep) -> (head, sep, tail)

        Search for the separator sep in S, starting at the end of S, and return
        the part before it, the separator itself, and the part after it.  If the
        separator is not found, return two empty strings and S.
        """
        pass

    def rsplit(self, sep=None, maxsplit=-1): # real signature unknown; restored from __doc__
        """
        S.rsplit(sep=None, maxsplit=-1) -> list of strings

        Return a list of the words in S, using sep as the
        delimiter string, starting at the end of the string and
        working to the front.  If maxsplit is given, at most maxsplit
        splits are done. If sep is not specified, any whitespace string
        is a separator.
        """
        return []

    def rstrip(self, chars=None): # real signature unknown; restored from __doc__
        """
        S.rstrip([chars]) -> str

        Return a copy of the string S with trailing whitespace removed.
        If chars is given and not None, remove characters in chars instead.
        """
        return ""

    def split(self, sep=None, maxsplit=-1): # real signature unknown; restored from __doc__
        """
        以sep为分割，将S切分成列表，与partition的区别在于切分结果不包含sep，
        如果一个字符串中包含多个sep那么maxsplit为最多切分成几部分
        >>> a='a,b c\nd\te'
        >>> a.split()
        ['a,b', 'c', 'd', 'e']
        S.split(sep=None, maxsplit=-1) -> list of strings

        Return a list of the words in S, using sep as the
        delimiter string.  If maxsplit is given, at most maxsplit
        splits are done. If sep is not specified or is None, any
        whitespace string is a separator and empty strings are
        removed from the result.
        """
        return []

    def splitlines(self, keepends=None): # real signature unknown; restored from __doc__
        """
        Python splitlines() 按照行('\r', '\r\n', \n')分隔，
        返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如        果为 True，则保留换行符。
        >>> x
        'adsfasdf\nsadf\nasdf\nadf'
        >>> x.splitlines()
        ['adsfasdf', 'sadf', 'asdf', 'adf']
        >>> x.splitlines(True)
        ['adsfasdf\n', 'sadf\n', 'asdf\n', 'adf']

        S.splitlines([keepends]) -> list of strings

        Return a list of the lines in S, breaking at line boundaries.
        Line breaks are not included in the resulting list unless keepends
        is given and true.
        """
        return []

    def startswith(self, prefix, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.startswith(prefix[, start[, end]]) -> bool

        Return True if S starts with the specified prefix, False otherwise.
        With optional start, test S beginning at that position.
        With optional end, stop comparing S at that position.
        prefix can also be a tuple of strings to try.
        """
        return False

    def strip(self, chars=None): # real signature unknown; restored from __doc__
        """
        S.strip([chars]) -> str

        Return a copy of the string S with leading and trailing
        whitespace removed.
        If chars is given and not None, remove characters in chars instead.
        """
        return ""

    def swapcase(self): # real signature unknown; restored from __doc__
        """
        大小写反转
        S.swapcase() -> str

        Return a copy of S with uppercase characters converted to lowercase
        and vice versa.
        """
        return ""

    def title(self): # real signature unknown; restored from __doc__
        """
        S.title() -> str

        Return a titlecased version of S, i.e. words start with title case
        characters, all remaining cased characters have lower case.
        """
        return ""

    def translate(self, table): # real signature unknown; restored from __doc__
        """
        table=str.maketrans('alex','big SB')

        a='hello abc'
        print(a.translate(table))

        S.translate(table) -> str

        Return a copy of the string S in which each character has been mapped
        through the given translation table. The table must implement
        lookup/indexing via __getitem__, for instance a dictionary or list,
        mapping Unicode ordinals to Unicode ordinals, strings, or None. If
        this operation raises LookupError, the character is left untouched.
        Characters mapped to None are deleted.
        """
        return ""

    def upper(self): # real signature unknown; restored from __doc__
        """
        S.upper() -> str

        Return a copy of S converted to uppercase.
        """
        return ""

    def zfill(self, width): # real signature unknown; restored from __doc__
        """
        原来字符右对齐，不够用0补齐

        S.zfill(width) -> str

        Pad a numeric string S with zeros on the left, to fill a field
        of the specified width. The string S is never truncated.
        """
        return ""

     ...略...
```



