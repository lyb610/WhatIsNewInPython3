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

- print语句变为print()函数 ([FEP 3105](https://www.python.org/dev/peps/pep-3105))

- 返回视图和迭代而不是列表 (Views And Iterators Instead Of Lists)
    - dict的keys(), values(), items()返回视图
    - dict的iterkeys(), itervalues(), iteritems()被移除
    - map(),filter(),zip()返回迭代
    - range()替代了xrange(), xrange()被移除

- 排序比较 (Ordering Comparisons)
    - (<,<=,>=,>)不再支持无意义的操作数(operands), 而是返回TypeError异常
    - sorted()和list.sort()的cmp参数被移除, 应该用key参数
    - cmp()被移除, __cmp__()不再支持, 应该用__lt__(), __eq__(), __hash__()

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
    - 非ASCII符号不能做标识符(identifiers)
    - 参考: [Unicode HOWTO](https://docs.python.org/3/howto/unicode.html#unicode-howto)

## 语法变化
- 新语法
- 改变语法
- 移除语法

## 库变化

## 异常变化

## 其他变化

