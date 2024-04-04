---
layout: post
title: Python Programming Basis
date: 2024-04-04
categories: test
tags: programming courses 
---

### Quick Indexes
- [数据结构](#一python数据结构)
	- [列表类型](#列表类型-list)
	- [字符串类型](#字符串类型-str)
    - [元组类型](#元组类型-tuple)
    - [字典类型](#字典类型-dict)
    - [集合类型](#集合类型-set)
- [流程控制](#二python流程控制)
- [面向过程](#三python函数与面向过程)
    - [函数初步](#函数初步)
    - [搜索与问题求解](#搜索与问题求解)
    - [函数的执行环境与状态](#函数的执行环境与状态)
    - [高阶函数](#高阶函数)
    - [函数的运算与无名函数](#函数的运算与无名函数)
- [面向对象](#四python面向对象)
    - [类和对象](#类和对象)
    - [继承和多态](#继承和多态)
    - [动态类型和鸭子类型](#动态类型和duck-typing)
- [模块与异常处理](#五python模块与异常处理)
    - [模块](#模块)
    - [异常处理](#异常处理)

## 一、Python数据结构

* **Python是强类型语言**，每个值的类型都是确定的，不进行隐式的类型转换。同时，**Python是动态类型语言**，值和变量的类型是运行时确定的，值的类型无须指定（运行时确定，相对于编译时通过定义、申明确定）

* python的数值运算包括：乘方`**`，加法`+`，减法`-`，乘法`*`，除法`/`，整除`//`，取余`%`，按位取反`~`，按位与`&`，按位或`|`，按位异或`^`，按位左移`<<`，按位右移`>>`，大于`>`，小于`<`，小于等于`<=`，大于等于`>=`，等于`==`，不等于`!=`，逻辑非`not`，逻辑与`and`，逻辑或`or`。（优先级和结合性为：算术运算符 > 位运算符 > 关系运算符 > 逻辑运算符）

* python中可以把函数赋给变量，这是函数式编程的重要特点，比如：

```python
myfunc = print
myfunc("hello world")
```

* python中的表达式包括值、变量、运算符表达式和函数调用表达式。解释器确定表达式值的过程包括：
  * 值的求值结果是值本身
  * 变量的求值结果是变量引用的值
  * 表达式的求值结果是操作符与操作数作用的结果（分别求操作符、操作数的值，再按照操作符/函数的定义进行运算）
  * 函数的求值结果是其返回值表达式的运算结果
* python的数据类型包括**可变对象mutable**和**不可变对象immutable**。可变对象包括list、dict、set以及大部分自定义类型的对象，不可变对象包括int、book、float、tuple、str、frozenset等。注意**int也是immutable**，python里面其实无法改变一个int的值。immutable比mutable对象具有更高的效率和更少的空间，且immutable可以作为参数传递而不用担心被修改，在多线程、多对象共享环境下都有更好的安全性。
* 有时，immutable对象内也可以包含mutable元素，如（理解：元组是一种元素的组合，其中不可变的是每一个元组元素到实际对象（值）的引用或绑定关系，如果某个元组元素本身是可变的，则其值仍然可以发生变化）

```python
myTuple = ("test",[0,1])
myTuple[0] = 'Test'					# 报错
myTuple[1] = [1,2]					# 报错
myTuple[1][0] = 3					# ('test',[3,2]) 
```

#### 【列表类型 list】

* 列表是按照顺序排列的元素组成的数据类型，比如：
  * `ls = ['C', 'C++', 'Java', 'Python']`（直接创建）
  * `num = list(range(1,5))`（从range对象创建，range对象也有**切片**功能，类似于列表切片）
  * ` ls = list("Hello World")`（从字符串创建）
  * `num = list(reversed([3, 9, 1, 7]))`（从迭代器创建）。

可以按照次序访问对应的元素（下标、索引），每个元素也可以看做是一个变量，下标为负数表示列表结尾开始进行索引。注意：**列表中元素的类型不一定相同！**列表的元素可以仍然为列表（二维列表、高维列表）。

* **列表元素操作**：

```python
# 修改元素
languages[0] = 'Perl'			# 直接索引

# 添加元素
languages.append('Go')			# append函数
languages.insert(2,'Scheme')	# insert函数

# 删除元素
languages.pop()					# pop函数(默认删除最后一个)
del languages[1]				# del函数
languages.remove('Go')			# remove函数
```

* **列表整体操作**：

```python
# 列表比较(列表的值比较结果为其逐个元素值比较的结果)
x = [1,2,3,4]
y = [1,2,3,4]
z = [1,2,3,5]
x == y							# True
x is y							# False
x < z							# True
x < 5							# 报错(因为数据类型不同)

# 列表"开包"(unpacking，用*操作符实现)
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]
[1,*matrix,2]					# [1, [1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12], 2]

# 列表排序(sort或sorted，默认升序排序)
x = [3,9,1,7]
x.sort()						# [1,3,7,9]
sorted(x)						# [1,3,7,9]
x.sort(reverse=True)			# [9,7,3,1]
sorted(x,reverse=True)			# [9,7,3,1]

# 列表倒序(reversed，需要类型转换)
reversed([3,9,1,7])				# <list_reverseiterator object at 0x7fc961b154d0>
list(reversed([3,9,1,7]))		# [7,1,9,3]

# 列表过滤(filter，过滤掉不符合条件的元素)
ls = [1,2,3,4,5,6,7]			
filter(lambda x: x>2,ls)		# [3,4,5,6,7]

# 简单的数据统计(max, min, sum, len)
digits = [1,3,16,5,9]
min(digits)						# 1
max(digits)						# 16
sum(digits)						# 34
len(digits)						# 5
max(['c++','java','python'])	# 'python'
```

* 列表参与运算

```python
# 成员判断（in）
3 in [1,3,4]					# True

# 序列连接（+）
[2,8,6] + [1,3,4]				# [2,8,6,1,3,4]

# 序列重复（*）
[1,3,4] * 3						# [1,3,4,1,3,4,1,3,4]
```

* **列表解析（List Comprehension）**：通过对已有元素序列依次进行操作来创建一个新列表

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/image-20230621155346200.png?raw=true)

列表解析非常通用，可以有多个for语句（从左到右依次执行），也可以有复杂的条件判断表达式，还可以进行列表解析的嵌套，下面通过几个实例来说明：

```python
# 实例1：求一个列表各元素的完全平方数
[ value**2 for value in [1,2,3,4] ]					# [1,4,9,16]
[ value**2 for value in range(1,5) if value%2==0 ]	# [4,16]

# 实例2：组合打印两个列表[1,2,3]和[3,1,4]，且不打印相同元素
[ print(x,y) for x in [1,2,3] for y in [3,1,4] if x != y ]

# 实例3：二维矩阵的降维
matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
[ num for row in matrix for num in row ]			# [1,2,3,4,5,6,7,8,9,10,11,12]

# 实例4：奇偶交替打印
[ 'Even' if i%2==0 else 'Odd' for i in range(6) ]	# ['Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd']

# 实例5: 求100以内的既是2的倍数也是7的倍数的数
[ y for y in range(100) if y%2==0 if y%7==0 ]		# [0, 14, 28, 42, 56, 70, 84, 98]

# 实例6：二维矩阵转置的实现
matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
# 方法一：循环
transposed = []
for i in range(4):
    transposed_row = []
    for row in matrix:
        transposed_row.append(row[i])
    transposed.append(transposed_row)
# 方法二：列表解析
[ [ row[i] for row in matrix ] for i in range(4) ]	# [[1,5,9],[2,6,10],[3,7,11],[4,8,12]]
# 方法三：循环＋列表解析
transposed = []
for i in range(4):
    transposed.append([row[i] for row in matrix])
# 方法四：zip函数（不要求掌握）
list(zip(*matrix))									# [[1,5,9],[2,6,10],[3,7,11],[4,8,12]]
```

* **列表切片（Slice）**：按照下标从列表中取出多个元素，构成新的列表。

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/image-20230621161410805.png?raw=true)

注意：**结束位置元素不在结果列表中**！start、end 可以省略，分别表示从列表开始、直到列表结束；步长用于跳过部分元素，可以省略，表示默认步长为1；切片结果由start、end和step共同决定，若所选区域内无元素，则返回空列表。

```python
listA = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
listA[1:6]						# ['b', 'c', 'd', 'e', 'f']
listA[1:6:2]					# ['b', 'd', 'f']
listA[-2:]						# ['f', 'g']
listA[:-2]						# ['a', 'b', 'c', 'd', 'e’]
listA[::]						# ['a', 'b', 'c', 'd', 'e', 'f', 'g']
listA[::-1]						# ['g', 'f', 'e', 'd', 'c', 'b', 'a']
listA[-2::-1]					# ['f', 'e', 'd', 'c', 'b', 'a']
listA[-2:-5]					# []
listA[-2:-5:-1]					# ['f', 'e', 'd']
```

* **列表复制**：分为普通的copy和deepcopy。copy方法只复制列表本身，而deepcopy方法则递归地复制整个列表及其所有嵌套对象。

```python
a1 = [1,2,[3,4]]

# shallow copy(仅复制一层列表，修改b1[2][0]会影响a[2][0])
b1 = a1.copy()					# b1为[1,2,3]
b1 is a							# False
b1[2] is a[2]					# True

# deep copy(复制整个列表和其中包含的所有子对象，包括嵌套的对象，修改b2[2][0]的值不影响a[2][0]的值)
from copy import deepcopy
b2 = deepcopy(a2)
b2 is a							# False
b2[2] is a[2]					# False
```

#### 【字符串类型 str】

* 单引号/双引号可标识字符串，三引号的可以使字符串跨行。
* **列表是可变的！字符串是一种值不可以发生改变的对象！**字符串的值不能修改，诸如`"Hello"[0] = 'H'`的操作是非法的。
* 字符串可以看做是字符的列表，使用许多列表操作，比如下标访问、**切片**、循环访问元素、列表解析等。
* 字符串的常见函数（注：python中提供的常用字符串功能会返回**新的对象**，因为原有字符串的值不能修改）

```python
# 拼接(+和*)
("happy" + " ") * 3					# 'happy happy happy '

# 求长度
len('Guido van Rossum')				# 15

# 求值(只针对字符串是数字字符的)
eval("3")							# 3 (type: int)
eval("3.5")							# 3.5 (type: float)

# 大小写转换
"Guido van Rossum".upper()			# "GUIDO VAN ROSSUM"
"GUIDO VAN ROSSUM".lower()			# "guido van rossum"

# 分割(若不填入，默认按空格)
"Guido van Rossum".split()			# ['Guido','van','Rossum']
"Guido van Rossum".split('u')		# ['G','ido van Ross','m']

# 首字母大写
"guido van Rossum".caplitalize()	# "Guido van Rossum"

# 两端空格删除
" Guido ".lstrip()					# "Guido "
" Guido ".rstrip()					# " Guido"
" Guido ".strip()					# "Guido"
```

* format方法示例：

```python
"{} beat {} yesterday!".format("Lakers","Pacers")		#'Lakers beat Pacers yesterday!'
"{1} beat {0} yesterday!".format("Lakers","Pacers")		# 'Pacers beat Lakers yesterday!'
"Print float : {0:.0f}".format(3.1415)					# 'Print float : 3'
"Print float : {0:.2f}".format(3.1415)					# 'Print float : 3.14'
```

注：上面的示例中给出了**输出指定位小数**的方法，如`'{0:.2f}.format(3.1415)'`输出为3.14。

* find方法示例：

```python
s = 'What do you think of this saying "No pain, No gain"?'
index = s.find("\"")
index2 = s.rfind("\"")
s[index+1:index2]
# 输出为'No pain, No gain'
```

注：上面的示例的功能是**取出文本中的引用内容**，更简单地可表示为`s.split("\"")[1]`。

* 简便的字符串处理功能：

```python
# f-string(格式化字符串操作)
name = 'Python'
f'Hello, dear {name}'				# 'Hello, dear Python'

# 转义字符(表示缩进\t、换行\n、换页等)
'Hello, \t my friend, \n \t\t Greetings!'
# 若想阻止解释转义字符，用r-string
r'Hello, \t my friend, \n \t\t Greetings!'

# 直接使用ASCII码
"\x64 \x34"							# d 4
```

#### 【元组类型 tuple】

* 元组是一组具有序列关系的元素的组合，元组的元素可以不同（可以方便的利用元组将一组数据组合成一个对象（packing），也可以再吧元组赋值给多个变量（unpacking）），**元组的对象是不可变对象**，显式标识对象不应该再被修改。
* 因为元素具有序列关系，元组具有跟序列相关的操作（如下标访问、循环访问元素、用于列表解析、len、加乘拼接），也可以用切片、sorted、reversed等方式构建新的元组（**需要用tuple()转换**）。因为元组对象是immutable，所以不能增加、删除、修改其元素，即不能用append、pop、insert等函数。
* **元组对象的packing和unpacking**：

```python
# packing可以用于参数传递，如：
"{} beat {} yesterday!".format("Lakers","Pacers")	# 将多个元素组合成一个元素

# unpacking可以用于从控制台获取多个输入，如：
x, y = [ eval(t) for t in input().split() ]			# 将一个元素拆分成多个元素

# packing举例：
a, b = 1, 2						# a, b = (1,2)
a, b = b, a						# a, b = (2,1)
a, b = 1, 2, 3					# 报错（因为元素数量不匹配）
a, *b = 1, 2, 3					# a, b = (1,[2,3])
a, *b, c = [1, 2, 3, 4, 5, 6]	# a, b, c = (1,[2,3,4,5],6)
```

#### 【字典类型 dict】

* 字典是用于保存成对信息的一种数据结构，实际保存的是**Key到Value的映射关系**。**字典是可变对象**，可以修改其元素，创建方法为：

```python
# 从key value列表创建，如：
salaries = [3000, 4500, 8000]
names = ['Mayue', 'Lilin', 'Wuyun']
sd1 = dict(zip(names, salaries))					# {'Mayue': 3000, 'Lilin': 4500, 'Wuyun': 8000}

# 从tuple列表创建，如：
salariesList =  [('Mayue', 3000), ('Lilin', 4500), ('Wuyun', 8000)]
sd2 = dict(salariesList)							# {'Mayue': 3000, 'Lilin': 4500, 'Wuyun': 8000}

# 利用字典解析（格式如下）创建新字典，如：
sd3 = { chr(ord('a')+i): i+1 for i in range(5) }	# {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}
sd4 = { k:v*2 for (k,v) in sd3.items() }			# {'a': 2, 'b': 4, 'c': 6, 'd': 8, 'e': 10}
```

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/image-20230621171209431.png?raw=true)

* **从字典中获取元素信息**：可转换成元素序列（iterable），用于循环遍历等用途（注意：**由于用于索引value，所以keys中的值不能重复**）

```python
sd = {'Mayue': 3000, 'Lilin': 4500, 'Wuyun': 8000}

# 取出制定键的值
sd['Mayue']							# 3000

# 键的列表
sd1.keys()							# dict_keys(['Mayue', 'Lilin', 'Wuyun'])

# 值的列表
sd1.values()						# dict_values([3000, 4500, 8000])

# 键值对（即元素）的列表
sd1.items()							# dict_items([('Mayue', 3000), ('Lilin', 4500), ('Wuyun', 8000)])
```

#### 【集合类型 set】

* 集合用于描述一系列无序**不重复**的元素的组合，分为可变集合（set）和不可变集合（frozenset）。集合可以由列表创建，用大括号表示，如：

```python
names = ['Mayue', 'Lilin', 'Wanqi', 'Mayue', 'Lilin']
nameset = set(names)					# {'Mayue', 'Wanqi', 'Lilin'}
```

* 集合的基本操作有添加删除元素（set）、元素判断（in/not in）以及合交并补差等运算。也可以作集合解析，公式与列表解析完全相同，只是中括号变成了大括号而已，即：`newset = {expression for item in terable if condition == True}`。由于**集合的不重复性**，在创建集合时会只保留一个相同的元素。



## 二、Python流程控制

**Python流程控制包括顺序执行、分支语句和循环语句**。此处略去对基础语法（如if语句、for语句、while语句）的复习，只关注几个特殊的部分。

* 条件表达式：特殊的表达式语句，可以看做一种三元运算符，`<expression> if <expression> else <expression>`，类似于C++中的`a ? b : c`运算符。其中expression也可以是条件表达式（即可以多重嵌套）。条件表达式可用于普通语句中，多用于列表解析和lambda表达式中，如：`["Even" if i%2==0 else "Odd" for i in range(6)]` 输出为 `['Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd']`。
* 循环控制语句的终止：`break`用于终止当前循环语句执行，转而执行循环之后的语句；`continue`用于终止当前子句执行，转而执行循环的header。
* **可迭代对象和迭代器对象**：可迭代对象是含有多个元素的对象，如列表、元组、字典、集合等。通过`iter()`函数返回一个迭代器。迭代器对象指向可迭代对象（中的某个位置，通过`next()`函数访问器下一个位置的元素，知道无更多元素为止。如：

```python
myList = [1,2,3]
x = iter(myList)			# <list_iterator object at 0x7fce9e757950>
next(x)						# 1
next(x)						# 2
next(x)						# 3
next(x)						# 报错（因为没有下一个对象了

tuple(myList)				# (1,2,3)
tuple(mylist)				# (1,2,3)
y = iter(mylist)
tuple(y)					# (1,2,3)
tuple(y)					# ()
```

* **面向控制台的输入输出**：输入为`input()`函数，返回值为str类型，因此可以通过split()、eval()等函数对结果进行类型转换，得到列表、元组、整数等类型；输出为`print()`函数，可以连续输出多个对象（类似于tuple packing），配合字符串处理的format函数、f-string，可以得到不同格式的输出结果。
* **面向文件的输入输出**：`open()、read()、write()、seek()、readline()、readlines()、writelines()、close()`。（通常会导入`os`模块进行辅助文件操作）

```python
# 打开文件: 
f = open('textfile.txt')

# 读写操作(作为可迭代对象): 
f.read()				# 读第一段
f.read()				# 读第二段
f.seek(0)				# 查找文件中0的个数
[line for line in f]	# 构成一个列表，每一个元素是一个字符串，代表一行的文本

# 关闭文件:
f.close(0)

# 上下文管理器(context manager)用于自动负责对象的执行和收尾工作，如文件的打开和关闭等。
with open ("textfile.txt") as f:
    [line.strip() for line in f]
    ......								# 关于f的若干操作
```



## 三、Python函数与面向过程

* **面向过程**是一种编程思想，它将程序流程作为主要关注点，自顶向下、逐步求精地设计程序。而函数是一段可重用的代码块，能够完成特定的任务，可以提高代码的复用性和可维护性。函数的基本语法为：

```python
def func(x):		# 声明（可以没有操作数）
    ......			# 具体功能
    return ...		# 返回（可以没有）
```

* **函数是程序设计的基本单元**，是抽象的基本单位，强调功能的简洁明确以便于复用；函数可以作为参数和返回值，便于处理功能差异；同时，使用更加通用的计算框架，便于复用通用计算过程。后面分几个部分分析函数。

#### 【函数初步】

* 函数名与函数的绑定关系：**函数可以被绑定到新的变量，也可以通过赋值解除绑定**，如

```python
def add_by_3(x):
    ......
func = add_by_3						# type(func) = <class 'function'>
func = 5							# type(func) = <class 'int'>
func(1)								# 报错（因为func此时是一个数）
```

* 函数执行过程，将参数argument与函数的形参formal parameter进行绑定，依次执行函数定义子句中的操作语句，执行return语句时结束子句执行，并将return表达式的计算结果返回（**return表达式可以返回一个或多个对象，返回多个对象时进行元组的packing**）。参数传递有以下五种形式：位置参数（默认的参数传递方式）、关键字参数、默认参数、元组参数`*args`和字典参数`**kwargs`。举例如下（**注意，参数传递时不进行类型匹配！**）：

```python
# 按位置逐一匹配形参和实参（即位置参数，是默认的参数传递方式）
def dividing_op(num, denom):
	return num/denom
dividing_op(3,1)					# 3.0
dividing_op(1,3)					# 0.33333333333333333

# 按名进行参数传递（即关键字参数，指定与某个形参绑定）
def dividing_op(num, denom):
	return num/denom
dividing_op(num=3,denom=1)			# 3.0
dividing_op(denom=3,num=1)			# 0.33333333333333333

# 定义函数时指定参数的默认值（即默认参数，存在默认绑定对象）
def dividing_op(num, denom=1):
    return num/denom
dividing_op(3)						# 3.0

# 可变长位置参数（即元组参数，事先不确定个数的参数）
def myprint(first, *args):
    print(first, args)
myprint(1,2)						# 1,(2,)
myprint(1,2,3,4)					# 1,(2,3,4)

# 可变长关键字参数（即字典参数key+value，事先不确定个数的参数对）
def myprint(**kwargs):
    for (k,v) in kwargs.items():
        print(type(k),":",k,type(v),":",v)
myprint(a=1,b=2)					# <class 'str'> : a <class 'int'> : 1
									# <class 'str'> : b <class 'int'> : 2
```

* 函数之间可以进行嵌套调用，进而形成“函数中调用函数”或者“**递归函数（recursive function）**”。递归函数是指函数执行过程中直接或者间接调用其本身，体现了“分而治之”的思想，将复杂问题分解为一个或多个相对简单的同构问题。

```python
# 实例：求一元人民币换成一分、两分和五分的所有兑换方案数(541)
# 方法一：循环函数
def split_cirlulation(x):
    count = 0
    for i in range(x//5+1):
        for j in range(x//2+1):
            k = x - 5*i - 2*j
            if k >= 0:
                count += 1
                print("5"*i, "2"*j, "1"*k)
    return count
split_circulation(100)

# 方法二：递归函数
def split_recursion(x, current=[], piece=5):
    if x < 0:
        return 0
    if x == 0:
        print("".join(current))
        return 1
    elif piece == 5:
        return split_recursion(x - 1, current + ['1'], 1) \
    		+ split_recursion(x - 2, current + ['2'], 2) \
			+ split_recursion(x - 5, current + ['5'], 5)
    elif piece == 2:
        return split_recursion(x - 1, current + ['1'], 1) \
			+ split_recursion(x - 2, current + ['2'], 2)
    elif piece == 1:
        return split_recursion(x - 1, current + ['1'], 1)
split_recursion(100)

# 方法三：动态规划
def split_dynamics(count):
    table = [0] * (count + 1)
    table[0] = 1
    for coin in [1, 2, 5]:
        for i in range(coin, count + 1):
            table[i] += table[i - coin]
    return table[count]
split_dynamic(100)
```

* 函数作为更高层的抽象：行为的抽象 → **行为作为参数传递**。下面探讨迭代函数的抽象（update为迭代更新函数，accurate是条件判断的逻辑函数），核心函数是：

```python
def improve(update, accurate, guess):	# 声明
    while not accurate(guess):			# 条件
        guess = update(guess)			# 迭代
    return guess						# 返回
```

* 下面用几个例子来说明用抽象的函数可以实现具体的功能：

```python
# 实例1：用黄金分割方程 x=1/(1+x) 求黄金分割比i
def golden_update(guess):
    return 1 / (guess + 1)
def golden_accurate(guess):
	return abs(guess * guess + guess - 1) < 1e-10
output_golden = improve(golden_update, golden_accurate, guess=1)

# 实例2：用Fibnacci数列求黄金分割比i
def fibnacci_update(guess):
    return (guess[1], guess[0]+guess[1])
def fibnacci_accurate(guess):
    value = guess[0] / guess[1]
    return abs(value * value + value - 1) < 1e-10
output_fabnacci = improve(fibnacci_update, fibnacci_accurate, (1,1))

# 实例3：用二分法求2的平方根
def sqrt_update(guess):
    average = (guess[0] + guess[1]) / 2
    if average * average > 2:
        return (average, guess[1])
    else:
        return (average, guess[0])
def sqrt_accurate(guess):
    average = (guess[0] + guess[1]) / 2
    return abs(average * average - 2) < 1e-10
output_sqrt = improve(sqrt_update, sqrt_accurate, (0,2))
```

#### 【搜索与问题求解】

* 对于简单的搜索问题，直接通过循环/递归对问题进行遍历，即可找到最优解。但是对于相对复杂的搜索问题，搜索空间复杂、难以直接遍历（比如包含多个动作构成的序列，每个动作都对结果产生影响），则需要去构造一个搜索问题，基本步骤为：
  * **初始状态**（initial state）
  * **动作**（action），需要判断动作是否可行（applicable）
  * **状态转换**（state transmission）：
* 搜索问题主要分为两种：动作搜索和状态搜索。
  * **动作搜索**：一般情况下，存在一个或多个合法的动作。动作空间一般相对较小，可以通过穷举方式进行搜索，动作合法性可以通过知识/规则进行条件判断。
  * **状态搜索**：从初始状态出发。当前状态下，执行某合法动作，状态发生改变（不同问题有影响动作和合法性的状态，影响终局形势的状态（代价cost/奖赏reward））。重复上条步骤，直到达到终止状态结束（搜索结果为所有经过的状态/动作构成的序列）。如果存在多条到达终止状态的路径，根据条件进行选择（比如最短移动路径、最少移动步数、最多剩余棋子数等）。最通用的情形为在一个树形结构中进行搜索（称作**状态搜索树**）：A为初始状态，某一个或多个状态为终止状态。每个状态可执行不同的动作，执行动作后状态发生相应的变化。
* 搜索的基本方法：有策略搜索和无策略搜索。
  * **有策略搜索（Informed Search）**：特点是每次选择当前看来最好的解（贪心搜索，Greedy Search），或者保证最优选择的方法（A* Search）。
  * **无策略搜索（Uninformed Search, Blind Search）**：如果能够高效便利所有可能，则可以穷举得到确定的结，重点是不重复、不遗漏。

#### 【函数的执行环境与状态】

* Python使用**一系列frame**来描述Python代码的执行环境，每个frame中包含**独立的绑定关系**（变量、函数等）。程序执行的第一个frame为**global frame**（全局作用域）。
  * 函数定义时，创建了一个global frame中的绑定关系（但并不执行）。
  * 函数调用发生时，为被调用函数创建**local frame**（局部作用域），来记录形参和实参的绑定关系、以及函数执行过程中发生的新的绑定。**函数执行的环境包含global frame和该函数的local frame**，函数执行时依次在local frame、global frame中寻找绑定。
  * 函数的返回值也记录在当前函数的local frame中，用于返回给函数的调用者。
  * 函数的每次调用（包括多个函数的之间的调用和递归函数本身的调用）都会创建**新的local frame**作为该调用环境的一部分。因而环境保证了递归函数的正确执行。
* **函数中的形参和变量的作用域（scope）仅限于当前函数**。因为，其仅存于当前函数的local frame中。因此，不同函数的局部变量互相不会影响。
* **函数中的形参和变量的作用域（scope）仅限于当前调用**。因为，每次调用创建一个独立的local frame。因此，同一个函数的多次不同调用互相不产生影响。

* **纯函数（Pure-Function）执行过程不影响函数外部的状态**：根据输入（实参），完成指定计算，并返回结果。相对的，Non-Pure-Function函数执行过程中回怼外部状态产生影响，称为**函数副作用**。程序状态包括：非局部变量、生成器函数、其他程序状态（控制台输出、文件写入等）。
* Python中**Immutable参数是避免函数副作用的一种机制**，而Mutable参数可能潜在的影响程序运行。（但是Immutable对象中仍然可以有Mutable元素，可能带来副作用）。如：

```python
def printID(x):
    print(x, ":", id(x))
def work_print(x):
    x += 5
    printID(x)
def change_print(x):
    x[0] = 5
    printID(x)
# 若为Immutable对象（以int型为例）
x = 3
printID(x)						# 3 : 4332774608
work_print(x)					# 8 : 4332774768
printID(x)						# 3 : 4332774608
# 若为Mutable对象（以list型为例）
y = [0,1,2,3]
printID(y)						# [0, 1, 2, 3] : 140350183780832
change_print(y)					# [5, 1, 2, 3] : 140350183780832
printID(y)						# [5, 1, 2, 3] : 140350183780832
```

* 一个函数的同一个变量的绑定一定在同一个frame中，因而global frame中的x和local frame中的x的地址是不同的。如果要在函数中修改环境中的值（绑定关系），需要**显示声明需要修改的绑定关系（global）**，如`global x`，使得当前frame中不再创建x的绑定关系，而是使用global frame中的绑定关系。在函数中改变外部环境的状态是一种**传递信息**的方法，但在函数中改变外部环境的状态可能使程序调试变得困难。
* **算法正确性**是对任意一个合法的输入经过有限步执行之后算法应给出正确的结果（functional correctness）。包括**partial correctness**（算法返回结果时，结果是正确的）和**total correctness**（算法必须停止）。因此需要编写**测试函数**（使用**assert**语句），来保证函数的正确性，语法为：`assert <expression>, <string>`（当expression为false时，输出string）。举例如下，如果违背assert，则会引发异常并输出对应提示：

```python
def compute(x, y):
	return x + y, x - y
def compute_test():
    assert compute(3, 5) == (8,-2), 'wrong computing for 3, 5'
    assert compute(5, 3) == (8, 2), 'wrong computing for 5, 3'
```

#### 【高阶函数】

* **嵌套的函数定义**，即在函数中定义函数（如工具函数）。这是由于部分函数的定义仅用于某些特定的计算，在global frame中绑定容易与其他函数名发生冲突。
  * 包含嵌套定义的函数在执行时，嵌套定义语句被执行。嵌套定义的函数的绑定关系记录在定义发生的frame中。
  * 调用嵌套定义的函数时，同样创造新的local frame。此时，**frame之间发生的嵌套关系**，绑定关系按照**current local frame → parent frame → global frame**的顺序依次进行查找（parent frame是嵌套函数的上一层函数，不包含嵌套的函数的parent frame是global frame）。
  * **内层的嵌套函数能使用外层的绑定**，即嵌套函数中可以引用外部变量。

```python
# 实例1：用嵌套函数修改之前求黄金分割比（运行的底层逻辑如下图所示）
def improve(update, accurate, guess):
    while not accurate(guess):
        guess = update(guess)
    return guess
def appr_equal(x, y, epsilon = 1e-10):
    return abs(x - y) < epsilon
def golden_ratio():
    def update(guess):
        return 1 / (guess + 1)
    def accurate(guess):
        return appr_equal(guess * guess, 1 - guess)
    return improve(update, accurate, guess = 1)
golden_ratio()
```

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/image-20230320172836245.png?raw=true)
```python
# 实例2：用嵌套函数修改之前的求2的平方根（运行的底层逻辑如下图所示）
def improve(update, accurate, guess):
    while not accurate(guess):
        guess = update(guess)
    return guess
def my_sqrt(x):
    def average(tup):
    	return (tup[0] + tup[1]) / 2
	def sqrt_update(guess):
   		mid = average(guess)
    	if mid * mid > x:
        	return guess[0], mid
    	else:
        	return mid, guess[1]
	def sqrt_accurate(guess):
    	return abs(average(guess) * average(guess) - x) < 1e-10
    return average(improve(sqrt_update, sqrt_accurate, guess = (0, x)))
my_sqrt(2)
```

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/image-20230320175030283.png?raw=true)
* 在嵌套定义的函数中，如果在函数中需要修改环境中的值（绑定关系），亦需要**显示声明需要修改的绑定关系**，此时的代码是`nonlocal x`，使得当前frame中不再创建x的绑定关系，而是使用parent frame（global除外）中的绑定关系。（注意：函数运行过程中**可以改变parent frame中的状态**，这也是一种函数的副作用）
* 函数作为返回值可以使得程序具有更大的灵活性，对nonlocal的使用使得函数具有外部状态，如下面的实例中，每次调用make_withdraw函数都会创造一个包含balance变量的frame，后续的withdraw调用将会使用这个frame中的balance状态（称作**闭包**）：

```python
# 实例：设计一个银行账户函数，需要返回一个提款函数withdraw，每次调用都进行“提款”（运行的底层逻辑见下）
def make_withdraw(balance):
    def withdraw(amount):
        nonlocal balance		# Declare the name 'balance' nonlocal
        print(balance)
        if amount > balance:
            return 'Insufficient funds'
        x = balance - amount	# Re-bind the existing balance name
        balance = x
        return balance
    return withdraw
```

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/image-20230621205344889.png?raw=true)

* **总结一下**：Non-pure functions具有可以改变的状态和环境，可以通过mutable参数或显式声明修改**全局状态**（global frame，即C++中的全局变量）和**外层函数的状态**（parent frame，即C++中的静态变量）。因而同样的函数代码，在不同的状态下可能执行不同的功能，同样的函数的多次调用也可能返回不同的结果，这使得程序状态和正确性的维护变得复杂。

#### 【函数的运算与无名函数】

* **函数复合**也是高阶函数的一种表现形式，将多个函数组合在一起形成一个新的函数，这个新的函数可以依次调用各个复合函数来完成相应的任务。如：

```python
def compose(f, g):
    def h(x):
        return f(g(x))
	return h
# 函数compose调用时，发生形参f、g和实参的绑定，并定义h（绑定关系记录在该函数的local frame中）。当函数h被调用时，实参与形参绑定，同时利用parent frame中的f、g完成函数调用。（注意：如果存在child frame，则对应的parent frame不能删除）调用示例如：
def square(x):
    return x * x
def successor(x):
    return x + 1
square_successor = compose(square, successor)
result = square_successor(12)
```

* **函数的柯里化（Currying）**：因为使用等原因，将多个参数放进一个接受许多参数的函数，形成一个新的函数接受余下的参数，并返回结果（**将有多个参数的函数转换为单个参数的函数**）。Currying可以有多种方法实现，如：

```python
def add_print(x,y):
    print("fst:",x)
    print("sec:",y)
    print("res:",x+y,"\n")
add_print(3,5)

# 方法一
def add_3_print(x):
    print("fst:",x)
    print("sec:",3)
    print("res:",x+3,"\n")
add_print(7)

# 方法二
def add_3_print_cur(x):
    return add_print(x,3)
add_3_print_cur(3)

# 方法三
def add_print_cur(x):
    def f(y):
        return add_print(x,y)
    return f
add3 = add_print_cur(3)
print(add3)
add3(7)
```

* **装饰器（function decorator）**：用于扩展（装饰）给定函数的行为。装饰器使得我们可以**将代码逻辑封装在一个函数中**，并在其他函数中使用。装饰器本质上是**一个接受函数作为参数的可调用对象**，它可以修改函数的上下文或行为，或者对函数进行增强。装饰器可以在不修改函数本身的情况下为其添加额外的功能。如：

```python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")
    
say_hello()
# 运行结果为：Something is happening before the function is called.
#			Hello!
#			Something is happening after the function is called.
```

注：上面的代码实现了在每一次调用say_hello()函数之前和之后都打印一条语句，体现函数调用的过程信息。装饰器还可以应用去获得函数调用的状态信息，比如可以设计如下面的一个计数器函数得到某函数调用的次数：

```python
def count_calls(func):
    def wrapper(*args, **kwargs):
        wrapper.count += 1
        print(f"Function {func.__name__} called {wrapper.count} times.")
        return func(*args, **kwargs)
    wrapper.count = 0
    return wrapper

@count_calls
def func(n):
    ...... 			# 通常为递归函数
    
# 运行结果为：Function my_function called 1 times.
#			Function my_function called 2 times.
#			Function my_function called 3 times.
#			......
```

* **无名函数（lambda表达式）**：lambda函数是指简单的代码片段，通常认为是不值得命名的函数，它不能重复使用，能方便程序员使用，增强代码可读性，降低代码出错概率。语法为：`lambda <formal parameters> : <expression>`。lambda表达式实际上也是定义函数，其parent frame取决于定义的位置，只不过**lambda函数无需定义的标识符（函数名）**，类似于C++中的inline内联函数，可以接收任意多个参数（包括可选参数）并且返回单个表达式的值，因而更加简便。如：

```python
# 实例1: 使用lambda表达式将字符串转换为大写
string = "hello world"
upper_string = lambda x: x.upper()
print(upper_string(string))							# "HELLO WORLD"

# 实例2: 使用Lambda表达式将两个数相加
add_numbers = lambda x, y: x + y
result = add_numbers(3, 5)
print(result)										# "8"

# 实例3: 使用Lambda表达式过滤列表中的元素：
num = [5, 2, 8, 1, 9]
filtered_numbers = filter(lambda x: x <= 5, num)	
print(list(filtered_numbers))						# [5,2,1]
```

* **Map函数**：**根据提供的函数对制定序列作映射**。将函数作用于单个序列中的每个元素，返回元素结果组成的序列。基本语法为：`map(function, iterable, ...)`，此处序列以可迭代对象的形式抽象，返回值是一个map对象，也是一个迭代器对象。如：

```python
def square(x):
	return x * x
map(square, [1,2,3,4,5])									# [1,4,9,16,25]

# 结合lambda函数和map函数
map(lambda x: x*x, [1,2,3,4,5])								# [1,4,9,16,25]

# 针对多个序列的map函数
map(lambda x,y: x*y, [1,2,3,4,5],[1,3,5,7,9])				# [1,6,15,28,45]

# 结合map和filter函数
map(lambda x: x*x, filter(lambda x: x%2==1, range(10)))		# [1,9,25,49,81]
```



## 四、Python面向对象

* Python是良好的面向对象语言，整数、浮点型、字符串值是对象，liast、map、set、tuple是对象，迭代器是对象，函数是对象……**类和对象是面向对象程序设计中对数据进行抽象和封装的方式**。（注意：**类≠类型**！类型描述了数据以及对数据所能做的操作，C中的结构、C++中的类都是自定义数据类型的方法）

* 抽象与封装是两个重要的程序设计手段，主要是用来驾驭程序的复杂度，便于大型程序的设计、理解与维护。对于一个程序实体而言，
  * **抽象**是指该程序实体的**外部**可观察到的行为，不考虑该程序实体的内部是如何实现的；
  * **封装**是指把该程序实体的具体实现细节**对使用者隐藏**起来的一种机制。
* 主要的程序抽象和封装的基质包括：**过程抽象与封装**（以过程为核心，数据作为过程的操作内容）和**数据抽象与封装**（以数据为核心，过程作为数据的功能属性）。

* **面向对象程序设计（Object-Oriented Programming, OOP）**具有以下几个特征：
  * 程序由若干**对象**组成，每个对象是由数据以及对这些数据所能实施的**操作**所构成的封装体；
  * 对象的特征由相应的**类**来描述；
  * 对数据的使用是通过向包含数据的对象发送**消息**来实现的；
  * 一个类所描述的对象特征可以从其它的类**继承**获得；
  * 相同消息可以被发送给不同对象，可能引发不同的程序行为，这是面向对象特有的**多态**。

#### 【类和对象】

* 类用于描述一系列对象具有的共有的特征，定义语法为：`class <name>:`，属性是在`<suite>`中描述的绑定关系，包括变量属性和函数属性。变量属性（**成员变量**）描述了对象的**状态（数据）**，函数属性（**成员函数**）描述了对对象**可以进行的操作**。如：

```python
# 实例：设计定义一个账户类，描述银行账户相关的信息
class Account:
    def __init__(self, account_holder):
        self.balance = 0
        self.holder = account_holder
    # __init__是在创建对象时由python自动调用的函数，用于完成属性绑定和对象的初始化操作（即C++中的构造函数）
    # self用于描述当前对象
    # self.balance和self.holder是当前对象的数据成员
    
    def deposit(self, amount):
        self.balance += amount
    def withdraw(self, amount):
        self.balance -= amount
    # deposit和withdraw是Account类的成员函数，是Account类的对象可以进行的操作
```

* 类的定义描述了一系列对象具有的共有的特征，程序中通过创建类的实例（即对象）来进行是会用。**创建对象一般通过对构造函数的调用进行。**一个类可以创建多个对象。如`b = Account("Li")`，`c = Account("Li")`，但是b和c的地址是不同的。**每个对象都拥有独立的状态，即拥有独立的绑定关系记录！而且每个对象的绑定关系还可以在程序中继续变化。**
* 与全局或者局部的变量或函数不同，类中定义的属性进存在当前类中，通过对象进行访问。每个对象实例都拥有类中定义的属性，可以直接访问成员变量（数据），可以通过方法调用完成所需功能。因而**对象是数据和操作的集合**，**数据描述对象的改变**，每个对象可以拥有独立的状态，而**操作对状态进行改变**。
* **成员函数的访问**有两种方式，一是通过对象访问，访问改变当前的状态（**bound method**，通过self参数实现，python解释器自动传入self参数）；二是通过类进行访问和调用（**function**），应自行制定需要传入的参数，此时也会改变相应对象状态。

```python
# 访问方式1: 通过对象访问
a = Account("Li")
a.deposit(100)				
print(a.deposit)			# <bound method Account.deposit of <__main__.Account object at 0x7f8afc9d9c10>>

# 访问方式2: 通过类访问
b = Account("Li")
Account.deposit(b, 100)
print(b.deposit)			# <function Account.deposit at 0x7fe3e306c0e0>
```

* Python中类的属性默认公开访问权限（相当于C++中的public访问控制），在程序中通过对象即可进行访问。存在部分数据其访问需要受到一定限制，可使用**命名约定**的方法进行：
  * `__xxx__`命名**以双下划线开头和结尾**的成员一般为**python解释器专用标识**，如构造函数`__init__`、析构函数`__del__`、迭代器函数`__iter__`、系统内嵌属性字典`__dict__`等，在duck-typing中有很多的应用。
  * `__xxx`命名**以双下划线开头**的成员**仅由类对象自身访问**，相当于C++中的private访问控制。
  * `_xxx`命名以**以单下划线开头**的成员**仅由类对象与其派生类对象访问**，相当于C++中的protected访问控制。
* 使用私有数据成员可以更好的保护内部数据和计算过程（**封装**），则对数据的访问使用公开的接口进行，如：

```python
class Account:
	def __init__(self, account_holder):
		self.__balance = 0
    	self.__holder = account_holder
	def deposit(self, amount):
    	self.__balance += amount
	def print(self):
        print(self.__holder, self.__balance)
```

* **类成员**：分为**对象的类成员**和**类的类成员**，是同一个类的不同对象之间共享数据的方式，相当于C++中的static成员，如：

```python
class Account:
    interest = 0.2
    ......
# 下面通过实例说明对象的类成员和类的类成员之间的不同(底层逻辑见下图):
a = Account("Huang")
b = Account("Li")
print(a.interest)					# 0.2
print(b.interest)					# 0.2
print(Account.interest)				# 0.2
a.interest = 0.3
print(a.interest)					# 0.3
print(b.interest)					# 0.2
print(Account.interest)				# 0.2
Account.interest = 0.4
print(a.interest)					# 0.3
print(b.interest)					# 0.4
print(Account.interest)				# 0.4
```

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/image-20230621224131477.png?raw=true)

* **成员访问**（dot expression）：`<expr>.<name>` 是成员访问的一般语法，其中expr的计算结果是一个对象，name是一个可能的绑定关系。**成员访问是访问结果对象的指定成员。**如果赋值操作符在左边，直接对`<expr>`结果的成员进行查找：若结果为对象，则绑定对象成员；若结果为类，则绑定类成员。如果操作符在右边，计算`<expr>`的结果对象，再**依次**查找绑定关系：在对象的实例成员列表中查找`<name>`的绑定关系，在对象的类成员列表中查找`<name>`的绑定关系。则可以**利用类成员进行类级别的操作**，如：

```python
# 对类的对象进行计数
class CountedAccount:
    __count = 0								# 对count进行封装，防止在外部的访问造成程序错误
   	def __init__(self, account_holder):
        self.holder = account_holder
        CountedAccount.__count += 1			# 利用类成员进行类级别的操作
    def __del__(self):
        CountedAccount.__count -= 1
    # __del__函数是对象消亡时由python自动调用的函数，一般用于完成对象的消亡前处理操作（相当于C++中的析构函数）

    def printCount():
        print(CountedAccount.__count)
    def getCount():
        return CountedAccount.__count
    # printCount和getCount用于操作类成员，因此没有self属性
```

#### 【继承和多态】

* 一个类所描述的对象特征可以从其他的类**继承**获得，即**派生类**（子类）继承**基类**（父类）的内容。派生类的对象拥有基类中定义的属性，也可以拥有新定义的属性。进行成员访问的名绑定关系查找时，**优先查找本类中的成员**，若在派生类中找不到的名绑定关系，会在其基类中继续寻找。语法为：`class Derived(Base):`。如：

```python
class CheckingAccount(Account):
    def withdraw_charge(self, amount):
        self.balance -= (amount + 1)
        self.withdraw(amount + 1)
        Account.withdraw(self, amount + 1)		# 通过调用基类方法实现相应功能以保持一致性
        # 等价于: super().withdraw(amount + 1)
```

* 如果在派生类中需要对现有功能进行改变或扩充，可以**重新进行成员函数的定义**。保持函数名称一致有利于保持接口的一致性，同时新取代了原先的方法，防止了调用错误的发生、在派生类的对象发生成员函数调用时，根据成员访问规则，将**优先访问派生类中**定义的成员函数。
* `__init__`函数的继承和重写：若派生类中不定义`__init__`构造函数，则继承基类；若发生重写，则派生类应该负责**全部数据**的初始化（或可以显式调用基类的初始化函数，或通过super函数找到该类的基类），如：

```python
class CheckingAccount(Account):
	def __init__(self, acc_holder, balance):
		self.balance = balance
		self.holder = ac_holder
# 显示调用基类的构造函数       
class CheckingAccount(Account):
	def __init__(self, acc_holder, balance):
		Account.__init__(self, acc_holder)
		self.balance = balance
# 通过super函数找基类
class CheckingAccount(Account):
    def __init__(self, acc_holder, balance)
    	super().__init__(acc_holder)
        self.balance = balance
```

* **多态性（Inheritance Polymorphism）**：继承中的多态是指同一个方法在不同子类中具有不同的实现方式。实现多态的必要条件是：必须要有继承；子类必须重写父类的方法；调用方法时必须通过父类的引用调用。主要的情形有：
  * **类型的多态**：同一个对象既是基类对象，也可以是派生类的对象。这是由于派生类可以看做是对基类的一种扩展，因而类型的多态性具有**基类公开属性的实现**（虽然可能会被重写）。基类的对象只能是基类的，而派生类的对象既可以是基类的也可以是派生类的。
  * **消息的多态**：可以用通用的操作（相同的消息）来操作不同的对象。不同的对象可能进行不同的响应，即：**外部操作是一致的，但对象的实际行为可能不同**。Python的消息多态性体现在成员和操作始终是**动态绑定**，这与C++不同（C++中默认是静态绑定，只有对显示声明的虚函数进行动态绑定）。如：

```python
# 消息的多态（同样的外部操作withdraw，但对象的实际行为不同）
def withdraw(account, amount):
    account.withdraw(amount)
    print(account.balance)

accounts = [Account("Bob"), Account("Lily"), CheckingAccount("Jack")]
for acc in accounts:
    withdraw(acc, 10)						# 90, 90, 89
```

* **开闭原则（the open-cloased principle）**：software entities(classes, modules, functions, etc.) should be **open for extension**, but **closed for modification**. 开闭原则告诉我们，在利用继承的多态进行程序设计时，可以通过继承引入新的类、保持或者更新原有的功能（open），而对对象进行的代码（高层代码）可以保持不变（closed）。因而多态性的管理可以通过**命名约定**（即以双下划线开头或以单下划线开头）进行实现。
* Python规定，**所有的类（包括自带的数据类型）都直接或间接地继承自object**，下面是object的一些基本的对象属性：`['__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', __sizeof__', '__str__', '__subclasshook__']`，可以通过调用函数`dir(object)`实现。
* 继承分为单继承和多继承，**多继承**指从多个类中同时获得属性（即`class Derived(Base1, Base2, ...):`，派生类可以获得所有基类的全部属性。但是**多继承会带来属性冲突的问题**，即不同的基类之间可能存在同名属性。属性冲突的调用关系确定：
  * 按照**派生类-基类**的顺序依次查询绑定关系。
  * 申明多个基类时，**按照基类的声明顺序**依次进行查找（多个基类的声明顺序会影响程序的运行结果）。一个类的声明顺序称作该类的**MRO（method resolution order）**，super()函数按照MRO的顺序依次寻找基类。
  * 如需调用特定类的属性，可以用**类名限定**。

```python
class Account:
    def function(self):
        print("1")
    
class CheckingAccount(Account):
    def function(self):
        print("2")
        
class SavingsAccount(Account):
    def function(self):
        print("3")
        
class NewAccount(CheckingAccount,SavingsAccount):
    pass		# 该类同时拥有了CheckingAccount类和SavingsAccount类的所有特征
# 此处的声明顺序：NewAccount, CheckingAccount,SavingsAccount,Account,object

obj = NewAccount()
print(obj.function())			# 2
print(NewAccount.mro())			# [<class '__main__.NewAccount'>, <class '__main__.CheckingAccount'>, <class '__main__.SavingsAccount'>, <class '__main__.Account'>, <class 'object'>]

# 通过类名限定解决属性冲突的问题，如：
CheckingAccount.function(obj)	# 2
SavingsAccount.function(obj)	# 3
Account.function(obj)			# 1
```

#### 【动态类型和Duck Typing】

* 在C++等静态类型语言中，**对象的类型决定了它能进行的操作**；而在Python等动态类型语言中，**是否进行操作取决于某些属性的实现**。Python程序的类型匹配问题为按位置匹配或按名匹配，引入了“Duck Typing"的概念：
  * **The Duck Test**：If it looks like a duck, swims like a duck, and quacks like a duck, then it probably is a duck.
  * **Duck Typing**: With normal typing, suitability is determined by an object's type. In duck typing, an object's suitability is determined by the presence of certain methods and properties, rather than the type of the object itself.
  * Pythonic programming style that determines an object's type **by inspection of its method or attribute signature** rather than by explicit relationship to some type object.（比如：具有`__next__()`方法的对象为迭代器，具有`__iter__()`方法的对象是可迭代对象）
  * By emphasizing interfaces rather than specific types, well-designed code improves its flexibility by allowing polymorphic substitution. Duck-typing avoids tests using type() or isinstance(). Instead, it typically employs the **EAFP** (Easier to Ask Forgiveness than Permission) style of programming.

```python
# 实例：Range对象的一种实现
class MyRange(object):
    def __init__(self, end):
        self.start = 0
        self.end = end
    def __iter__(self):				# 具有__iter__()方法，标明是可迭代对象
        return self
    def __next__(self):				# 具有__next__()方法，表明是迭代器
        if self.start < self.end:
            ret = self.start
            self.start += 1
            return ret
        else:
            raise StopIteration		# 以抛出异常的方式表示遍历结束
```

* Python动态类型中的部分特殊功能函数（**magic functions**）举例，需要知道大部分的magic functions以更好地设计相应的类：

```python
__new__			# 对象创建函数，在创建对象时自动调用
__init__		# 构造函数，在创建对象后自动调用
__del__ 		# 析构函数，在释放对象时自动调用
__repr__		# 当repr()调用时被自动调用
__str__			# 当str()调用时被自动调用
__len__			# 当len()调用时被自动调用
__bool__		# 当bool()调用时被自动调用
__setitem__		# 按照索引[]赋值时被调用
__getitem__		# 按照索引[]获取值时被调用

# 关于基本操作的特殊方法（类似于C++中的操作符重载）
__cmp__			# 返回比较的结果
__eq__			# ==
__ne__			# !=
__lt__			# <
__gt__			# >=
__add__			# +
__sub__			# -
__mul__			# *
__truediv__		# \
__mod__			# %
__pow__			# **

# 实例：定义一个数类，可以实现加法运算和打印值
class MyNumber():
    def __init__(self value):
        self.value = value
    def __add__(self, other):
        return MyNumber(self.value + other.value)
    def __str__(self):
        return str(self.value)
n1 = MyNumber(10)
n2 = MyNumber(15)
print(n1 + n2)					# 25
```

* **可调用的对象（callable objects）**：通过magic function `__call__()`在对象出现在函数调用语句中时自动被调用。这是因为**函数是对象，对象可以被当做函数使用**，类似于C++中的函数对象（重载函数调用操作符）。如：

```python
Class Adder():
    def __init__(self, n):
        self.n = n
    def __call__(self, k):
        return self.n + k

add_three_obj = Adder(3)
add_three_obj(4)				# 7
```

* **静态类型语言**通过编译时的类型检查确定程序中可能的错误，编译代价较大但运行效率更高；而**动态类型语言**通过运行时的检查报告可能的类型错误，运行时自由度更高、开发更为便捷灵活、开发束缚相对小。Python中可以通过**类型注解（type hint）**，以标记的形式知名类型（如：函数的参数和返回值），但**Python本身不处理注解**。如：

```python
def greeting(name: str) -> str:
    return 'Hello ' + name

# 可以用Union表示可以接受的多个类型
from typing import Union
def greeting(name: Union[str, int]) -> str:
    return 'Hello ' + name

# Any表示任意类型（相当于无类型注解）
def greeting(name: Any) -> Any:
    return 'Hello ' + name

# Callable表示函数类型
from collections.abc import Callable
def feeder(get_next_item: Callable[[], str]) -> None:
    pass
```



## 五、Python模块与异常处理

#### 【模块】

* Python中组织更大规模的代码，可以通过复合语句控制程序流程，或者通过函数进行过程抽象、类和对象进行数据抽象。进一步，可以用更大规模的模块、包、库等。在Python中，**模块是单个文件**，**包是单个目录（包含若干模块或者子包）**，**库是相关的若干包的组合**。
* 每一个单独的文件被看做是一个Python模块（module），每个模块包含自己的变量、函数、可执行代码等。内建函数`dir()`可以用于查看**模块中的绑定关系**，变量`__name__`存储当前模块的名字以区分不同模块，当文件做脚本运行时，可以通过sys.argv获取控制台的参数。模块的导入和相关操作如：

```python
# 模块导入
import test_print			# 类似于C++中的 #include "test_print.h"

# 执行模块中的代码
test_print.work_print(x)
```

* 对于引入模块中的执行代码，使用`__name__`区分模块引入和执行。当前模块被直接执行的值为`__main__`，否则为模块名。此时，文件**既能被Import也能被当做脚本**。模块内部实现的封装，向外提供某种函数或类的定义与实现。
* **包**组织多个文件/模块，一个包是一个目录，由多个模块或者子包组成。如：

```python
# 引入包
import numpy as np				# as可以在当前frame中创建新的名绑定

# 引入包中指定模块
from matplotlib import pyplot

# 引入包的全部内容
from sympy import *
```

#### 【异常处理】

* 程序执行过程是程序状态改变的过程。程序中的错误主要由以下几种：
  * **逻辑错误**：程序因为设计不当等原因不能完成预期的功能，程序状态与预期不一致。例如把两个数相加写成了相乘，排序功能未能正确排序等等。可以通过**静态分析和动态测试**发现，如assert、doctest等。
  * **语法错误**：程序的书写不符合语言的语法规则，如括号不匹配、漏写复合语句的冒号、缩减不一致等等，可以通过**编译器的静态检查**发现。
  * **运行时异常**：程序运行过程中产生的错误，例如除数为0、文件不存在、语法不正确、找不到名字、类型错误、值错误等。运行时的异常往往由程序运行过程中的**环境状态**导致，环境状态与预期不一致（EAFP），运行时的异常并不总是发生、**往往无法避免**。
* **结构化异常处理机制**：**`raise <exception>`**语句来发现异常，将异常发现与异常处理进行分离（类似于C++中的throw）。辅以逻辑判断进行状态检查，通过**返回值标识错误**、**全局变量标识**、**对象和函数的状态标识**进行处理预期和状态的不一致。如：

```python
def funcDiv(x, y):
    if y != 0:
        return x/y
    else:
        raise Exception("Div-zero")
        
def data_processing(x, y, comp):		# 过程抽象
    return comp(x, y)

def compute(x, y):
    return funcDiv(y, x) + funcDiv(x, y)

data_processing(1, 0, compute)

# 结果：发现异常，并按照调用链依次输出信息
'''Traceback (most recent call last):
File ".py", line 26, in <module>
data_processing(1, 0, compute)
File ".py", line 21, in data_processing
return compute(x, y)
File "n.py", line 24, in compute
funcDiv(y, x) + funcDiv(x, y)
File "n.py", line 16, in funcDiv
raise Exception("div-zero")
Exception: div-zero'''
```

* 异常对象：被抛出的异常可以用类型进行区别，主要的类型由**NameError**（变量名未绑定）、**TypeError**（类型错误）、**ValueError**（值错误）、**AttributeError**（对象没有指定的属性）。根据不同类型的异常可能可以采取不同的操作。Python解释器内定义了诸多异常（**built-in异常**），都**是Exception类的派生类**，对于可能出现异常的语句（如 `x/y` ）解释器会自动返回计算中的异常（即自动发现异常），抛出异常如`ZeroDivisionError`、`StopIteration`、`KeyError`等等。
* 通过复合语句进行异常处理代码声明，即**try-except**语句，基本的用法和语法如下：
  * try子句：声明可能出现异常的语句；
  * except子句：用于**按类型捕获**可能出现的异常，声明对特定异常进行处理的操作，可以为捕获的异常对象建立绑定（如`except <eclass> as <name>`）；
  * else子句：没有发生异常时执行的操作；
  * finally子句：无论是否发生异常都执行的操作，特别用于资源清理（如关闭文件）等场合。

```python
try:
    <try suite>
except <exception class>:
    <except suite>
else:
    <else suite>
finally:
    <finally suite>
```

```python
# 实例: 对上面的除法程序进行复合结构化语句完善
def funcDiv(x , y):
	return x / y
def data_processing(x, y, comp):
	return comp(x, y)
def compute(x, y):
	return funcDiv(y, x) + funcDiv(x, y)

def randfunc():
    try:
        data_processing(1, 0. compute)
    except ZeroDivisionError:
        print("handling zero-division")
try:
    randfunc()
except:
    print("handling other errors")
else:
    print("Results: ", x)
finally:
    exit()
```

* 用户自定义异常，可以通过**继承Exception类或其派生类**，存储相关的异常信息，如：

```python
class DividingError(Exception):
    def __init__(self, str, x, y):
        self.x = x
        self.y = y
        super().__init__(str)
try:
    x = data_processing(1, 0, compute)
    print("Results: ", x)
except DividingError as de:
    print(de)
    print("Dividing {} by {}".format(de.x, de.y))
except:
    print("unhandled error!")
```

* **上下文管理器（context manager）**：是一种描述运行时状态（上下文）的对象。该对象处理进入和退出上述运行时状态（上下文）的代码块，通常使用 with 语句调用，也可直接调用其方法来使用。常用于保存和恢复各种全局状态、锁定和解锁资源、打开关闭文件等。**with表达式**的用法为：`with <expr> as <name>:`
  * 计算`<expr>`的结果对象，并将结果与`<name>`绑定；
  * 在进入`<suite>`时执行开始特定操作，由`__enter__`约定；
  * 在结束`<suite>`时执行退出特定操作，由`__exit__`约定（注意：退出函数是否处理成功会影响程序的行为）。

```python
# 实例: 设计一个上下文管理器来执行相应的操作
class MyContextManager:
	def __init__(self, name):
		self.name = name
		print("in the constructor of", self.name)
	def __del__(self):
		print("in the destructor of", self.name)
	def __enter__(self):
		print("entering the process of", self.name)
	def __exit__(self, type, value, trace):
		print("leaving the process of", self.name)
		return True
    
with MyContextManager("myObj") as tc:
    print("during processing")
    raise Exception("Some Error")
print("Period")
```