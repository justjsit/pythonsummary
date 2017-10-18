廖雪峰Python教程学习笔记
======================
Python基础
-----------------------
输出：`print()`  
输入：`input()`  
### 数据类型和变量  
1、整数  
2、浮点数  
3、字符串  
4、布尔值`Ture`跟`False`  
5、空值`None`  
6、变量  
7、常量（用大写字母表示，事实上仍然是一个变量） 
### 编码
Python 3的字符串使用Unicode，直接支持多语言。  
### list和tuple  
list是一种有序的集合，用`len()`函数可以获得list元素的个数。还可以用-1做索引，直接获取最后一个元素：  
`classmates = ['Michael', 'Bob', 'Tracy']`  
`  
classmates[-1]
`可得到Tracy  
`append()`可以往list中追加元素到末尾  
`classmates.insert(1, 'Jack')`把元素插入到指定的位置  
`pop()`删除list末尾的元素  
tuple和list非常类似，但是tuple一旦初始化就不能修改  
list和tuple是Python内置的有序集合，一个可变，一个不可变。根据需要来选择使用它们。
### 条件判断  
`if...elif...else`
### 循环  
Python的循环有两种，一种是`for...in`循环，第二种循环是`while`循环，只要条件满足，就不断循环，条件不满足时退出循环。
`break`语句可以在循环过程中直接退出循环，而`continue`语句可以提前结束本轮循环，并直接开始下一轮循环。这两个语句通常都必须配合`if`语句使用。  
### dict和set
dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。  
`d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}`  
和list比较，dict有以下几个特点：
>查找和插入的速度极快，不会随着key的增加而变慢；
需要占用大量的内存，内存浪费多。  

而list相反：  
>查找和插入的时间随着元素的增加而增加；
占用空间小，浪费内存很少。  

set和dict类似，也是一组key的集合，但不存储value。  
`s = set([1, 2, 3])`  
**str是不变对象，而list是可变对象。** 

函数
------
### 定义函数  
在Python中，定义一个函数要使用`def`语句，依次写出函数名、括号、括号中的参数和冒号`:`，然后，在缩进块中编写函数体，函数的返回值用`return`语句返回。  
```
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```
定义函数时，需要确定函数名和参数个数；

如果有必要，可以先对参数的数据类型做检查；

函数体内部可以用return随时返回函数结果；

函数执行完毕也没有return语句时，自动return None。

函数可以同时返回多个值，但其实就是一个tuple。
### 函数的参数  
1、位置参数  
```
def power(x, n):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```
`power(x, n)`函数有两个参数：`x`和`n`，这两个参数都是位置参数，调用函数时，传入的两个值按照位置顺序依次赋给参数`x`和`n`。  
2、默认参数  
```
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```
默认参数可以简化函数的调用。设置默认参数时，有几点要注意：

一是必选参数在前，默认参数在后，否则Python的解释器会报错（思考一下为什么默认参数不能放在必选参数前面）；

二是如何设置默认参数。  
3、可变参数  
```
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```
4、关键字参数  
可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。请看示例：  
```
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```
5、命名关键字参数  
如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接收city和job作为关键字参数。这种方式定义的函数如下：  
```
def person(name, age, *, city, job):
    print(name, age, city, job)
```
和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。  

调用方式如下： 
```
>>> person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer
```
如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了：  
```
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```
6、参数组合  
在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。  

高级特性  
-------

### 切片
```
>>> L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
>>> L[:3]
['Michael', 'Sarah', 'Tracy']
```
在很多编程语言中，针对字符串提供了很多各种截取函数（例如，substring），其实目的就是对字符串切片。Python没有针对字符串的截取函数，只需要切片一个操作就可以完成，非常简单。
### 迭代
如果给定一个list或tuple，我们可以通过`for`循环来遍历这个list或tuple，这种遍历我们称为迭代（Iteration）。  
`dict`迭代的是`key`。如果要迭代`value`，可以用`for value in d.values()`，如果要同时迭代`key`和`value`，可以用`for k, v in d.items()`。  
如何判断一个对象是可迭代对象呢？方法是通过collections模块的Iterable类型判断：  
```
>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
False
```
Python内置的`enumerate`函数可以把一个`list`变成索引-元素对，这样就可以在`for`循环中同时迭代索引和元素本身：
```
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C
```
### 列表生成式
要生成`list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`可以用`list(range(1, 11))`。生成`[1x1, 2x2, 3x3, ..., 10x10]`:
```
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
筛选出仅偶数的平方：
```
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
```
还可以使用两层循环，可以生成全排列：
```
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```
列出当前目录下的所有文件和目录名，可以通过一行代码实现：
```
>>> import os # 导入os模块，模块的概念后面讲到
>>> [d for d in os.listdir('.')] # os.listdir可以列出文件和目录
['.emacs.d', '.ssh', '.Trash', 'Adlm', 'Applications', 'Desktop', 'Documents', 'Downloads', 'Library', 'Movies', 'Music', 'Pictures', 'Public', 'VirtualBox VMs', 'Workspace', 'XCode']
```
### 生成器
在Python中，这种一边循环一边计算的机制，称为生成器：generator。  
要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：  
```
>>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>
```
如果一个函数定义中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator：
```
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```
这里，最难理解的就是`generator`和函数的执行流程不一样。函数是顺序执行，遇到`return`语句或者最后一行函数语句就返回。而变成`generator`的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次返回的`yield`语句处继续执行。  
用`for`循环调用`generator`时，发现拿不到`generator`的`return`语句的返回值。如果想要拿到返回值，必须捕获`StopIteration`错误，返回值包含在`StopIteration`的`value`中：
```
>>> g = fib(6)
>>> while True:
...     try:
...         x = next(g)
...         print('g:', x)
...     except StopIteration as e:
...         print('Generator return value:', e.value)
...         break
...
g: 1
g: 1
g: 2
g: 3
g: 5
g: 8
Generator return value: done
```
### 迭代器
可以直接作用于`for`循环的数据类型有以下几种：

一类是集合数据类型，如`list、tuple、dict、set、str`等；

一类是`generator`，包括生成器和带`yield`的`generator function`。

这些可以直接作用于`for`循环的对象统称为可迭代对象：`Iterable`。