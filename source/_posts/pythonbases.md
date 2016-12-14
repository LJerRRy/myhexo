---
title: Python入门
date: 2016-11-05 13:52:05
tags: [Python]
categories: 学习笔记
---

## Python基本知识

1. 区分大小写，用`#`来注释
2. 用缩进（四个空格）来表示块
3. 变量的类型可以变，即不需要删除原始变量，直接进行赋值另一种类型
4. print，type函数，print为输出到终端，type查看类型
5. 常用数据类型有int,float,boolean(True/False),字符串
6. sequence序列是一组有序的元素集合，包括tuple（定值表，也叫元组，其中元素不能改变）和list（表，元素可以改变）
序列元素**下标从0开始**
基本样式 **[下限:上限:步长]**
```python
s1 = (2, 1.3, 'love', 5.6, 9, 12, False)         # s1是一个tuple,用括号来赋值
s2 = [True, 5, 'smile']                          # s2是一个list，用中括号来赋值
s3 = [1,[3,4,5]]                                 # 一个序列作为另一个序列的元素
print s1[:5]             # 从开始到下标4 （下标5的元素 不包括在内）
print s1[2:]             # 从下标2到最后
print s1[0:5:2]          # 从下标0到下标4 (下标5不包括在内)，每隔2取一个元素 （下标为0，2，4的元素）
print s1[2:0:-1]         # 从下标2到下标1
```

7. 字符串也是元组，所以也可以像序列一样进行相关操作
8. 逻辑运算符 and,or,not（与或非）
9. `if elif else` 选择语句，判断条件直接接在`if elif`后面，**不需要括号，但其末尾必须有个冒号**
10. `for while`循环， `for 元素 in 序列:`其中末尾有个冒号（while也是，判断条件不需要加括号），`range()`函数来帮助建表，`range(5) == [0,1,2,3,4]`
11. `break, continue`
12. `def`定义函数，可以用`return`返回函数值，可以返回多个

```python
def square_sum(a,b):
    c = a**2 + b**2
    return c
#可以return a,b,c多个返回值
```

13. 函数调用时，如果参数是表的话，然后对表进行操作，会改变表的值（引用传递），如果是整数的话，不会改变（按值传递）。
14. 类，用`class`定义类，都有一个原型（默认为object，但必须写）。属性和方法

```python
class Bird(object):
    have_feather = True #属性
    way_of_reproduction  = 'egg'
    def move(self, dx, dy): #方法，其中包括一个self（第一个参数必须是self），类似于java或者c++中的this
        position = [0,0]
        #self.have_feather = False #调用类属性
        position[0] = position[0] + dx
        position[1] = position[1] + dy
        return position
#类的继承
#子类
class Chicken(Bird):
    way_of_move = 'walk'
    possible_in_KFC = True

class Oriole(Bird):
    way_of_move = 'fly'
    possible_in_KFC = False

summer = Chicken()#创建一个对象
print summer.have_feather#调用对象的属性
print summer.move(5,8)
```

15. 类中有个**特殊方法（special method）**  `__init__()`方法 创建对象时自动调用这个方法，初始化对象的属性。

16. list是一个类，表的运算符，比如+, -, >, <, 以及下标引用[start:end]等等，从根本上都是定义在类内部的方法。

## Python中词典(dictionary)

一个新的类，词典 (dictionary)。与列表相似，词典也可以储存多个元素。这种储存多个元素的对象称为容器(container)

1. 词典和表类似的地方，是包含有多个元素，每个元素以逗号分隔。但词典的元素包含有两部分，**键**和**值**，常见的是以字符串来表示键，也可以使用数字或者真值来表示键（不可变的对象可以作为键）。值可以是任意对象。键和值两者一一对应。
2. 与表不同的是，词典的元素没有顺序。你不能通过下标引用元素。词典是通过键来引用。

```python
dic = {'tom':11, 'sam':57,'lily':100} #一个词典，词典可以为空
print type(dic)
dic['lilei'] = 99 #添加元素

for key in dic: #遍历词典
    print dic[key]

print dic.keys()           # 返回dic所有的键
print dic.values()         # 返回dic所有的值
print dic.items()          # 返回dic所有的元素（键值对）
dic.clear()                # 清空dic，dict变为{}
del dic['tom']             # 删除 dic 的‘tom’元素
#del是Python中保留的关键字，用于删除对象。
print len(dic)             # 返回dic元素个数
```

## Python进阶

### 文件操作
对象名 = open(文件名，模式)
最常用的模式有：

    r 打开只读文件，该文件必须存在。
    r+ 打开可读写的文件，该文件必须存在。
    w 打开只写文件，若文件存在则文件长度清为0，即该文件内容会消失。若文件不存在则建立该文件。
    w+ 打开可读写文件，若文件存在则文件长度清为零，即该文件内容会消失。若文件不存在则建立该文件。
    a 以附加的方式打开只写文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾，即文件原先的内容会被保留。
    a+ 以附加方式打开可读写的文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾后，即文件原先的内容会被保留。
    上述的形态字符串都可以再加一个b字符，如rb、w+b或ab＋等组合，加入b 字符用来告诉函数库打开的文件为二进制文件，而非纯文字文件。

```python
f = open("test.txt","r")
content = f.read(N)          # 读取N bytes的数据
content = f.readline()       # 读取一行
content = f.readlines()      # 读取所有行，储存在列表中，每个元素是一行。
f.write('I like apple!\n')      # 将'I like apple'写入文件并换行
f.close()   # 不要忘记关闭文件
```

### 模块

一个.py文件就构成**一个模块**。通过模块，你可以**调用**其它文件中的程序。

1. 引入模块，用`import + 文件名（不要加后缀名）`
引入模块后，可以通过 模块.对象 的方式来调用引入模块中的某个对象。

```python
#first.py文件
def laugh():
    print 'HaHaHaHa'
```

```python
import first   #将first文件引入

for i in range(10):
    first.laugh()#first为引入的模块，laugh()是我们所引入的对象。
```

```python
import a as b             # 引入模块a，并将模块a重命名为b

from a import function1   # 从模块a中引入function1对象。调用a中对象时，我们不用再说明模块，即直接使用function1，而不是a.function1。

from a import *           # 从模块a中引入所有对象。调用a中对象时，我们不用再说明模块，即直接使用对象，而不是a.对象。
```

2. Python会在以下路径中搜索它想要寻找的模块：
 -- 程序所在的文件夹
 -- 操作系统环境变量PYTHONPATH所包含的路径
 -- 标准库的安装路径

如果自定义的模块，或者下载的模块，可以根据情况放在相应的路径，以便Python可以找到。

3. 模块包,可以将功能相似的模块放在同一个文件夹（比如说this_dir）中，构成一个模块包。通过`import this_dir.module`
引入`this_dir`文件夹中的`module`模块。
该文件夹中必须包含一个` __init__.py` 的文件，提醒Python，该文件夹为一个模块包。`__init__.py` 可以是一个空文件。

### 函数的参数传递 
一般为位置传递，但比较死板。

1. 关键字(keyword)传递是根据每个参数的名字传递参数。关键字并不用遵守位置的对应关系。
2. 参数默认值，有的参数有默认值可以不需要传递
3. 包裹传递：在定义函数时，我们有时候并不知道调用的时候会传递多少个参数。这时候，包裹(packing)位置参数，或者包裹关键字参数，来进行参数传递，会非常有用。
Example 1:

```python
def func(*name):
    print type(name)
    print name

func(1,4,6)
func(5,6,7,1,2,3)
#两次调用，尽管参数个数不同，都基于同一个func定义。
#在func的参数表中，所有的参数被name收集，根据位置合并成一个元组(tuple)，这就是包裹位置传递。
```
Example 2:

```python
def func(**dict):
    print type(dict)
    print dict

func(a=1,b=9)
func(m=2,n=1,c=11)
#dict是一个字典，收集所有的关键字，传递给函数func。
#为了提醒Python，参数dict是包裹关键字传递所用的字典，在dict前加 * *。
```
4. 解包裹（unpacking）
\* 和 \*\*，也可以在调用的时候使用，即解包裹(unpacking).所谓的解包裹，就是在传递tuple时，让tuple的每一个元素对应一个位置参数。
Example :

```python
def func(a,b,c):
    print a,b,c

args = (1,3,4)
func(*args)

dict = {'a':1,'b':2,'c':3}
func(**dict)
```

5. 在定义或者调用参数时，参数的几种传递方式可以混合。但在过程中要小心前后顺序。基本原则是：**先位置，再关键字，再包裹位置，再包裹关键字**，并且根据上面所说的原理细细分辨。

### 循环设计 循环对象 函数对象
1. 循环设计
三个函数，`range(), enumerate(), zip()`
 --range() : 
 --enumerate() : 利用enumerate()函数，可以在每次循环中同时得到下标和元素，其返回的是一个包含两个元素的定值表(tuple)
 --zip() : 如果你多个等长的序列，然后想要每次循环时从各个序列分别取出一个元素，可以利用zip()方便地实现

```python
S = 'abcdefghijk'
for i in range(0,len(S),2):
    print S[i]
for (index,char) in enumerate(S):
    print index
    print char
ta = [1,2,3]
tb = [9,8,7]
tc = ['a','b','c']
for (a,b,c) in zip(ta,tb,tc):
    print(a,b,c)
```

2. **循环对象**：循环对象是这样一个对象，它包含有一个`next()`方法 ( `__next__()` 方法，在python 3x中 )， 这个方法的目的是进行到下一个结果，而在结束一系列结果之后，举出StopIteration错误。
当一个循环结构（比如for）调用循环对象时，**它就会每次循环的时候调用next()方法**，直到StopIteration出现，for循环接收到，就知道循环已经结束，停止调用next()。
**用循环对象的好处在于**：不用在循环还没有开始的时候，就生成好要使用的元素。所使用的元素可以在循环过程中逐次生成。这样，节省了空间，提高了效率，编程更灵活。

```python
for line in open('test.txt'):
    print line
#open()返回的实际上是一个循环对象，包含有next()方法。
#而该next()方法每次返回的就是新的一行的内容，到达文件结尾时举出StopIteration。这样，我们相当于手工进行了循环。
```

**迭代器**：从技术上来说，循环对象和for循环调用之间还有一个中间层，就是要将循环对象转换成迭代器(iterator)。这一转换是通过使用iter()函数实现的。但从逻辑层面上，常常可以忽略这一层，所以循环对象和迭代器常常相互指代对方。
**生成器**(generator)的主要目的是构成一个用户自定义的循环对象。
生成器的编写方法和函数定义类似，只是在return的地方**改为yield**。生成器中可以有多个yield。当生成器遇到一个yield时，会暂停运行生成器，返回yield后面的值。当再次调用生成器的时候，会从刚才暂停的地方继续运行，直到下一个yield。生成器自身又构成一个循环器，每次循环使用一个yield返回的值。
Example 1：

```python
def gen():
    a = 100
    yield a
    a = a*8
    yield a
    yield 1000
#该生成器共有三个yield， 如果用作循环器时，会进行三次循环。
for i in gen():
    print i
```

Example 2:

```python
def gen():
    for i in range(4):
        yield i
#它又可以写成生成器表达式(Generator Expression)：
G = (x for x in range(4))
```
**表推导**是快速生成表的方法。它的语法简单，很有实用价值。
假设生成表 L ：

```python
L = []
for x in range(10):
    L.append(x**2)
#快捷的写法，也就是表推导的方式:
L = [x**2 for x in range(10)]

xl = [1,3,5]
yl = [9,12,13]
L  = [ x**2 for (x,y) in zip(xl,yl) if y > 10]
```

3. 函数对象
一切皆对象，函数也是一个对象，具有属性（可以使用dir()查询）。作为对象，它还可以赋值给其它对象名，或者作为参数传递。即函数也可以作为参数进行传递。

**lambda()函数**：用来**定义函数**

```python
func = lambda x,y: x + y
print func(3,4)
#lambda生成一个函数对象。该函数参数为x,y，返回值为x+y。
#函数对象赋给func。
#func的调用与正常函数无异。
#等价于下面这个函数定义
def func(x, y):
    return x + y
```

**函数作为参数**

```python
def test(f, a, b):
    #print 'test'
    print f(a, b)

test(func, 3, 5)
#上面等价于下面一行
test((lambda x,y: x**2 + y), 6, 9)
```
**map()函数**
map()是Python的内置函数。它的第一个参数是一个函数对象。map()的功能是将函数对象依次作用于表的每一个元素，每次作用的结果储存于返回的表re中。例如`re = map((lambda x: x+3),[1,3,5,6])`，map通过读入的函数(这里是lambda函数)来操作数据（这里“数据”是表中的每一个元素，“操作”是对每个数据加3）。
在Python 3.X中，map()的返回值是一个循环对象。可以利用list()函数，将该循环对象转换成表。

```python
#如果作为参数的函数对象有多个参数，可使用下面的方式，向map()传递函数参数的多个参数：
re = map((lambda x,y: x+y),[1,2,3],[6,7,9])
#map()将每次从两个表中分别取出一个元素，带入lambda所定义的函数。
```
**filter()函数**
filter函数的第一个参数也是一个函数对象。它也是将作为参数的函数对象作用于多个元素。**如果函数对象返回的是True，则该次的元素被储存于返回的表中**。 filter通过读入的函数来筛选数据。同样，在Python 3.X中，filter返回的不是表，而是循环对象。

```python
def func(a):
    if a > 100:
        return True
    else:
        return False
print filter(func,[10,56,101,500])
```
**reduce函数**
reduce函数的第一个参数也是函数，但有一个要求，就是这个函数自身能接收两个参数。reduce可以累进地将函数作用于各个参数。如下例：

`print reduce((lambda x,y: x+y),[1,2,5,7,9])`
reduce的第一个参数是lambda函数，它接收两个参数x,y, 返回x+y。

reduce将表中的前两个元素(1和2)传递给lambda函数，得到3。该返回值(3)将作为lambda函数的第一个参数，而表中的下一个元素(5)作为lambda函数的第二个参数，进行下一次的对lambda函数的调用，得到8。依次调用lambda函数，每次lambda函数的第一个参数是上一次运算结果，而第二个参数为表中的下一个元素，直到表中没有剩余元素。

上面例子，相当于(((1+2)+5)+7)+9

*提醒： reduce()函数在3.0里面不能直接用的，它被定义在了functools包里面，需要引入包。*
