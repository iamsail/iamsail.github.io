---
title: (python)文档字符串
date: 2018-05-30 12:19:00
categories: Python
---
### ** Preface **

看Google开源项目Python风格指南注释部分时,看到文档字符串这个概念,本文做下记录。

*********************

### ** 注释 **

Python中的注释有单行注释和多行注释：

单行注释以 # 开头

```Python
# 这是一个注释
print("Hello, World!") 
```

多行注释用三个单引号 ''' 或者三个双引号 """ 将注释括起来

```
'''
这是多行注释，用三个单引号
这是多行注释，用三个单引号 
'''
print("Hello, World!") 

"""
这是多行注释，用三个双引号
这是多行注释，用三个双引号 
"""
print("Hello, World!") 
```
*******************

### ** 文档字符串 **

Python有一种独一无二的的注释方式: 使用文档字符串(`DocStrings`). 文档字符串是包, 模块, 类或函数里的第一个语句. <span class="under0">**这些字符串可以通过对象的`__doc__`成员被自动提取, 并且被`pydoc`所用.**</span> (你可以在你的模块上运行pydoc试一把, 看看它长什么样). 我们对文档字符串的惯例是使用三重双引号”“”( PEP-257 ). 

<span class="under0">** 一个文档字符串应该这样组织: 首先是一行以句号, 问号或惊叹号结尾的概述(或者该文档字符串单纯只有一行). 接着是一个空行. 接着是文档字符串剩下的部分, 它应该与文档字符串的第一行的第一个引号对齐. **</span>

#### ** 函数和方法 **

下文所指的函数,包括函数, 方法, 以及生成器.

一个函数必须要有文档字符串, 除非它满足以下条件:
>外部不可见
 非常短小
 简单明了

关于函数的几个方面应该在特定的小节中进行描述记录， 这几个方面如下文所述. <span class="under0">**每节应该以一个标题行开始. 标题行以冒号结尾. 除标题行外, 节的其他内容应被缩进2个空格.**</span>

`Args:`
列出每个参数的名字, 并在名字后使用一个冒号和一个空格, 分隔对该参数的描述.如果描述太长超过了单行80字符,使用2或者4个空格的悬挂缩进(与文件其他部分保持一致). 描述应该包括所需的类型和含义. 如果一个函数接受*foo(可变长度参数列表)或者**bar (任意关键字参数), 应该详细列出*foo和**bar.

`Returns:` (或者 `Yields:` 用于生成器)
描述返回值的类型和语义. 如果函数返回None, 这一部分可以省略.

`Raises:`
列出与接口有关的所有异常.


```regexp
def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
    """Fetches rows from a Bigtable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by big_table.  Silly things may happen if
    other_silly_variable is not None.

    Args:
        big_table: An open Bigtable Table instance.
        keys: A sequence of strings representing the key of each table row
            to fetch.
        other_silly_variable: Another optional variable, that has a much
            longer name than the other args, and which does nothing.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    Raises:
        IOError: An error occurred accessing the bigtable.Table object.
    """
    pass
```
********************
#### ** 类 **

类应该在其定义下有一个用于描述该类的文档字符串. 如果你的类有公共属性(Attributes), 那么文档中应该有一个属性(Attributes)段. 并且应该遵守和函数参数相同的格式.

```regexp
class SampleClass(object):
    """Summary of class here.

    Longer class information....
    Longer class information....

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```
*******************

### ** DocStrings实践 **

文件`test.py`如下

```
def printMax(x, y):
    '''Prints the maximum of two numbers.

    The two values must be integers.'''
    x = int(x) # convert to integers, if possible
    y = int(y)

    if x > y:
        print x, 'is maximum'
    else:
        print y, 'is maximum'

printMax(3, 5)
print printMax.__doc__ 
```

使用`__doc__`（双下划线）调用`printMax`函数的文档字符串属性（属于函数的名称）。Python把 每一样东西 都作为对象，包括这个函数。

使用`help()`也可以,它所做的只是抓取函数的`__doc__`属性，

```
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import test
5 is maximum
Prints the maximum of two numbers.

    The two values must be integers.
>>> print(test.printMax.__doc__)
Prints the maximum of two numbers.

    The two values must be integers.
    
>>> help(test.printMax)    
    Help on function printMax in module test:
    
    printMax(x, y)
        Prints the maximum of two numbers.
        
        The two values must be integers.


```


*******************

###  ** Main **

上面的文件`test.py`,在导入时也会被执行

> 即使是一个打算被用作脚本的文件, 也应该是可导入的. 并且简单的导入不应该导致这个脚本的主功能(main functionality)被执行, 这是一种副作用. 主功能应该放在一个main()函数中.

在Python中, pydoc以及单元测试要求模块必须是可导入的. **<span class="under0">你的代码应该在执行主程序前总是检查 if __name__ == '__main__' , 这样当模块被导入时主程序就不会被执行.</span>**
 
```regexp
def main():
      ...

if __name__ == '__main__':
    main()
```

所有的顶级代码在模块导入时都会被执行. 要小心不要去调用函数, 创建对象, 或者执行那些不应该在使用pydoc时执行的操作.

修改后的`test.py`

```regexp
def printMax(x, y):
    '''Prints the maximum of two numbers.

    The two values must be integers.'''
    x = int(x) # convert to integers, if possible
    y = int(y)

    if x > y:
        print (x, 'is maximum')
    else:
        print (y, 'is maximum')

if __name__ == '__main__':
	printMax(3, 5)
	print (printMax.__doc__) 
```

这样在导入时不会被执行

*******************

### ** 参考 **

[Python3 注释](http://www.runoob.com/python3/python3-comment.html)
[Python 风格指南 - 内容目录](http://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/contents/)
[python中的文档字符串(docString)](http://www.cnblogs.com/jlsme/articles/1394003.html)
[python中文档字符串与注释有什么区别？](https://www.zhihu.com/question/263349308/answer/270927715)
[说说Python程序的执行过程](https://www.cnblogs.com/kym/archive/2012/05/14/2498728.html)
