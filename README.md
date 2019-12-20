# WhatIsNewInPython3

![GitHub](https://img.shields.io/github/license/lyb610/WhatIsNewInPython3)

What's New In Python 3.x - Python3.x新特性

链接: https://docs.python.org/3/whatsnew/index.html

# 3.8
# 3.7
# 3.6
# 3.5
# 3.4
# 3.3
# 3.2
# 3.1

# 3.0
链接: https://docs.python.org/3/whatsnew/3.0.html

## 不兼容的变化(绊脚石， Common Stumbling Blocks)

- print语句变为print()函数 ([PEP 3105](https://www.python.org/dev/peps/pep-3105))

- 返回视图和迭代而不是列表 (Views And Iterators Instead Of Lists)
    - dict的keys(), values(), items()返回视图
    - dict的iterkeys(), itervalues(), iteritems()被移除
    - map(),filter(),zip()返回迭代
    - range()替代了xrange(), xrange()被移除

- 排序比较 (Ordering Comparisons)
    - (<,<=,>=,>)不再支持无意义的操作数(operands), 而是返回TypeError异常
    - sorted()和list.sort()的cmp参数被移除, 应该用key参数
    - cmp()被移除, \_\_cmp__()不再支持, 应该用\_\_lt__(), \_\_eq__(), \_\_hash__()

- 整数
    - long改为int, 只有int
    - /返回浮点: 1/2返回浮点值, 1//2返回整除值
    - sys.maxint被移除, 整数无大小限制

- 文本 与 数据, 而不是 Unicode字符串 与 8位字符串
    - 全部文本都是Unicode(编码)用str表示, 数据使用bytes表示
    - Unicode不再需要u"..."表示, 但bytes就必须用b"..."表示
    - str和bytes不能混用, 必须显式转换
    - stdin/stdout/stderr都是Unicode的文件
    - 默认源代码编码为UTF-8
    - 参考: [Unicode HOWTO](https://docs.python.org/3/howto/unicode.html#unicode-howto)

## 语法变化
- 新语法
    - [PEP 3107](https://www.python.org/dev/peps/pep-3107): 函数参数和返回值的注解
    - [PEP 3102](https://www.python.org/dev/peps/pep-3102): 必须指定关键字的参数(Keyword-only arguments)
    
        星号可以以一个参数的形式出现在函数声明中的参数列表中，但星号之后的所有参数都必须有关键字（keyword），这样在函数调用时，星号*之后的所有参数都必须以keyword=value的形式调用，而不能以位置顺序调用。
        
        ```python
          def compare1(a, b, *, c):
              pass
          
          compare1(1, 2, 3)           # 报错
          compare1(1, 2, c=3)         # 正确
      
          def compare2(*, a, b, c):
              pass
      
          compare2(1, 2, c=3)         # 报错
          compare2(a=1, b=2, c=3)     # 正确
        ``` 
  
    - [PEP 3104](https://www.python.org/dev/peps/pep-3104): nonlocal
        - nonlocal关键字用来在内层函数或其他作用域中使用外层(非全局)变量
        - 如果在内层函数中只是仅仅读外部变量，可以不在此变量前加nonlocal
        - 如果在内层函数中进行修改外部变量，且外部变量为不可变类型，则需要在变量前加nonlocal
        
    - [PEP 3132](https://www.python.org/dev/peps/pep-3132): 更牛逼的变量拆解(Extended Iterable Unpacking)
        
        ```python
          a, *rest, b = range(5)      # a = 0, rest = [1,2,3], b = 4
          *rest, b = range(5)         # rest = [0, 1, 2, 3], b = 4
          a, b, *rest = range(5)      # a = 0, b = 1, rest=[2, 3, 4]
          *a, b, *rest = range(5)     # 报错: *不能使用两次以上
          
          # 右边不够用也行
          a, b, *c = 1, 2             # a = 1, b = 2, c = []
          a, *b, c = 1, 2             # a = 1, b = [], c = 2
          *a, b, c = 1, 2             # a = [], b = 1, c = 2
        ```
        
    - 字典推导: {k: v for k, v in stuff} 和 dict(stuff) 一样, 但更灵活
    - 集合写法(Set literals), 与字典同样使用{}. 
        
        例如: {1, 2}代表集合. 但是{}是空字典, set()才是空集合, {x for x in stuff}和set(stuff)一样, 但更灵活
    
    - 新的八进制写法, 例如: 0o720(从2.6开始)，之前的0720会报错
    - 新的二进制写法, 例如: 0b1010(从2.6开始), 并有一个对应的内置函数, bin()
    - Bytes写法必须用b或者B指定, 并有一个内置函数, bytes()
    
- 改变语法
    - as, with, True, False, None现在是保留字(从2.6开始)
    - 列表推导: [i for i in 1,2,3]不再支持, 应该使用[i for i in (1,2,3)]
    
- 移除语法
    - [PEP 3113](https://www.python.org/dev/peps/pep-3113): 移除元组(tuple)参数拆解
        
        ```python
          def foo(a, (b, c)):
              # ...
       
          # 不再支持, 应该改为: 
      
          def foo(a, b_c): 
              b, c = b_c
        ```
        
    - 移除反引号 `, 应该使用repr()
    - 移除<>, 应该使用!=
    - exec()不再是关键字, 而是函数
    - 移除整数写法尾部的l和L(因为没有long, 只有int了)
    - from module import * 只能在模块级别上用，函数里不能
    - 相对路径import: from .[module] import name, 不使用.的都属于绝对路径import

## 库变化

- md5用hashlib替代

- 自动使用纯python版本和C加速版本
    - 2.x有些库有纯python版本和C加速版本, 例如pickle和cPickle. 3.0开始, 加速版本属于纯python的实现细节, 应该直接使用标准版本，内部实现根据情况纯python版本或者C加速版本

- 相关的模块被分组合到包里, 例如:
    - dbm (anydbm, dbhash, dbm, gdbm, ...)
    - http (httplib, BaseHTTPServer, ...)
    - urllib (urllib, urllib2, urlparse, ...)

## [PEP 3101](https://www.python.org/dev/peps/pep-3101): 字符串格式化新方法, %字符串格式化操作符将被替代掉.

## 异常变化

- [PEP 3110](https://www.python.org/dev/peps/pep-3110): except Exception, var 改为 except Exception as var

- [PEP 3109](https://www.python.org/dev/peps/pep-3109): raise Exception(args) 替代 raise Exception, args

- [PEP 3109](https://www.python.org/dev/peps/pep-3109)和[PEP 3134](https://www.python.org/dev/peps/pep-3134): 新的链式raise语法: raise [expr [from expr]]
    - 表明两个异常相关有连续性, 例如:         
    ```python
      raise SecondaryException("oops!") from primary_exception_var
    ``` 
## 其他变化

- 内置函数
    - [PEP 3135](https://www.python.org/dev/peps/pep-3135): 新的super(), 不带参数时自动选择正确的类和实例, 带参数时保持和之前不变.
    - [PEP 3111](https://www.python.org/dev/peps/pep-3111): raw_input()改名为input()
    - 新的next()调用对象的\_\_next__()方法
    - round()默认不再4舍5入, 必须大于0.5才入, 不再返回浮点数.
        - 例如: round(2.5)返回2, 而不是3.0, 但是round(2.500001)返回3
    - 移除apply()
    - 移除execfile()
    - 移除reduce(), 应使用functools.reduce()
    - 移除reload(), 应使用imp.reload()
    - 移除dict.has_key(), 应使用in
 
 # 移植到3.0
 
 - 测试代码覆盖率要足够高
 
 - (如果连2.6都没有) 先移植到2.6上
 
 - (如果还在2.6上) 使用-3开关, 进行测试, 解决所有的警告⚠️ 测试都通过
 
 - (如果已经在2.7上) 执行2to3进行代码转换, 在3.0下运行代码并解决剩下问题，最后保证测试全部通过
