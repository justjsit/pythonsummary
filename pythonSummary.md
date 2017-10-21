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

函数式编程
-------
### 高阶函数
`map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回。  
练习  
利用map()函数，把用户输入的不规范的英文名字，变为首字母大写，其他小写的规范名字。输入：['adam', 'LISA', 'barT']，输出：['Adam', 'Lisa', 'Bart']：
```
def normalize(x):
    def f(x):
        return x.lower()
    w=map(f,x)
    z=[]
    for j,value in enumerate(w):
        print(j,value)
        if(j==0):
            value=value.upper()
            print(value)
        z.append(value)
    return ''.join(z)
    
print(list(map(normalize,['adam', 'LISA', 'barT'])))
```
`reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算，其效果就是：
```
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```
和`map()`类似，`filter()`也接收一个函数和一个序列。和`map()`不同的是，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。  
```
def is_odd(n):
    return n % 2 == 1

list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
# 结果: [1, 5, 9, 15]
```
`sorted()`函数也是一个高阶函数，它还可以接收一个`key`函数来实现自定义的排序，例如按绝对值大小排序：
```
>>> sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]
```
### 返回函数
如果不需要立刻求和，而是在后面的代码中，根据需要再计算怎么办？可以不返回求和的结果，而是返回求和的函数：
```
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum
```
当我们调用`lazy_sum()`时，返回的并不是求和结果，而是求和函数：
```
>>> f = lazy_sum(1, 3, 5, 7, 9)
>>> f
<function lazy_sum.<locals>.sum at 0x101c6ed90>
```
调用函数f时，才真正计算求和的结果：
```
>>> f()
25
```
**闭包**  
返回闭包时牢记的一点就是：返回函数不要引用任何循环变量，或者后续会发生变化的变量。
### 匿名函数
在Python中，对匿名函数提供了有限支持。还是以`map()`函数为例，计算`f(x)=x^2`时，除了定义一个`f(x)`的函数外，还可以直接传入匿名函数：
```
>>> list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```
### 装饰器
本质上，`decorator`就是一个返回函数的高阶函数。所以，我们要定义一个能打印日志的`decorator`，可以定义如下：
```
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```
观察上面的`log`，因为它是一个`decorator`，所以接受一个函数作为参数，并返回一个函数。我们要借助`Python`的`@`语法，把`decorator`置于函数的定义处：
```
@log
def now():
    print('2015-3-25')
```
调用`now()`函数，不仅会运行`now()`函数本身，还会在运行`now()`函数前打印一行日志：
```
>>> now()
call now():
2015-3-25
```
一个完整的`decorator`的写法如下：
```
import functools

def log(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```
针对带参数的`decorator`：
```
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```
### 偏函数
`functools.partial`就是帮助我们创建一个偏函数的
```
>>> import functools
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
```
面向对象编程
------
面向对象编程——`Object Oriented Programming`，简称`OOP`，是一种程序设计思想。`OOP`把对象作为程序的基本单元，一个对象包含了数据和操作数据的函数。  
面向对象的设计思想是抽象出`Class`，根据`Class`创建`Instance`。  
面向对象的抽象程度又比函数要高，因为一个`Class`既包含**数据**，又包含**操作数据的方法**。  
**数据封装、继承和多态**是面向对象的三大特点。
### 类和实例
面向对象最重要的概念就是类（`Class`）和实例（`Instance`），必须牢记类是抽象的模板，比如`Student`类，而实例是根据类创建出来的一个个具体的“对象”，每个对象都拥有相同的方法，但各自的数据可能不同。  
由于类可以起到模板的作用，因此，可以在创建实例的时候，把一些我们认为必须绑定的属性强制填写进去。通过定义一个特殊的`__init__`方法，在创建实例的时候，就把`name`，`score`等属性绑上去：
```
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
```
注意到`__init__`方法的第一个参数永远是`self`，表示创建的实例本身，因此，在`__init__`方法内部，就可以把各种属性绑定到`self`，因为`self`就指向创建的实例本身。  
**数据封装**
这些封装数据的函数是和`Student`类本身是关联起来的，我们称之为类的方法：
```
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score

    def print_score(self):
        print('%s: %s' % (self.name, self.score))
```
### 访问限制
如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线`__`，在`Python`中，实例的变量名如果以`__`开头，就变成了一个私有变量（`private`），只有内部可以访问，外部不能访问，所以，我们把`Student`类改一改：
```
class Student(object):

    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    def print_score(self):
        print('%s: %s' % (self.__name, self.__score))
```
改完后，对于外部代码来说，没什么变动，但是已经无法从外部访问实例变量`.__name`和实例变量`.__score`了。  
但是如果外部代码要获取`name`和`score`怎么办？可以给`Student`类增加`get_name`和`get_score`这样的方法：
```
class Student(object):
    ...

    def get_name(self):
        return self.__name

    def get_score(self):
        return self.__score
```
如果又要允许外部代码修改`score`怎么办？可以再给Student类增加`set_score`方法：
```
class Student(object):
    ...

    def set_score(self, score):
        self.__score = score
```
你也许会问，原先那种直接通过`bart.score = 59`也可以修改啊，为什么要定义一个方法大费周折？因为在方法中，可以对参数做检查，避免传入无效的参数：
```
class Student(object):
    ...

    def set_score(self, score):
        if 0 <= score <= 100:
            self.__score = score
        else:
            raise ValueError('bad score')

```
### 继承和多态
继承有什么好处？最大的好处是子类获得了父类的全部功能。继承的第二个好处需要我们对代码做一点改进。  
继承可以把父类的所有功能都直接拿过来，这样就不必重零做起，子类只需要新增自己特有的方法，也可以把父类不适合的方法覆盖重写。
### 获取对象信息
**使用type()**
```
>>> type(123)
<class 'int'>
>>> type('str')
<class 'str'>
>>> type(None)
<type(None) 'NoneType'>
>>> type(abs)
<class 'builtin_function_or_method'>
>>> type(a)
<class '__main__.Animal'>
```
如果要判断一个对象是否是函数怎么办？可以使用`types`模块中定义的常量：
```
>>> import types
>>> def fn():
...     pass
...
>>> type(fn)==types.FunctionType
True
>>> type(abs)==types.BuiltinFunctionType
True
>>> type(lambda x: x)==types.LambdaType
True
>>> type((x for x in range(10)))==types.GeneratorType
True
```
**使用isinstance()**  
对于`class`的继承关系来说，使用`type()`就很不方便。我们要判断`class`的类型，可以使用`isinstance()`函数。  
如果继承关系是：
```
object -> Animal -> Dog -> Husky
```
那么，`isinstance()`就可以告诉我们，一个对象是否是某种类型。先创建3种类型的对象：
```
>>> a = Animal()
>>> d = Dog()
>>> h = Husky()
>>> isinstance(h, Husky)
True
```
能用`type()`判断的基本类型也可以用`isinstance()`判断：
```
>>> isinstance('a', str)
True
>>> isinstance(123, int)
True
>>> isinstance(b'a', bytes)
True
```
并且还可以判断一个变量是否是某些类型中的一种，比如下面的代码就可以判断是否是`list`或者`tuple`：
```
>>> isinstance([1, 2, 3], (list, tuple))
True
>>> isinstance((1, 2, 3), (list, tuple))
True
```
**使用dir()**  
如果要获得一个对象的所有属性和方法，可以使用`dir()`函数，它返回一个包含字符串的`list`。
配合`getattr()`、`setattr()`以及`hasattr()`，我们可以直接操作一个对象的状态：
```
>>> class MyObject(object):
...     def __init__(self):
...         self.x = 9
...     def power(self):
...         return self.x * self.x
...
>>> obj = MyObject()
```
紧接着，可以测试该对象的属性：
```
>>> hasattr(obj, 'x') # 有属性'x'吗？
True
>>> obj.x
9
>>> hasattr(obj, 'y') # 有属性'y'吗？
False
>>> setattr(obj, 'y', 19) # 设置一个属性'y'
>>> hasattr(obj, 'y') # 有属性'y'吗？
True
>>> getattr(obj, 'y') # 获取属性'y'
19
>>> obj.y # 获取属性'y'
19
```
### 实例属性和类属性
给实例绑定属性的方法是通过实例变量，或者通过`self`变量：
```
class Student(object):
    def __init__(self, name):
        self.name = name

s = Student('Bob')
s.score = 90
```
在编写程序的时候，千万不要把实例属性和类属性使用相同的名字，因为相同名称的实例属性将屏蔽掉类属性，但是当你删除实例属性后，再使用相同的名称，访问到的将是类属性。
