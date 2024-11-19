# python

## python基础

### 常见函数

title()以首字母大写的方式显示每个单词，即将每个单词的首字母都改为大写。

剔除字符串开头的空白，或同时剔除字符串两端的空白。为此，可分别使用方法lstrip()和strip()：

python中的/（除）保留小数，而整除是 //

```python
3 / 2  # 1.5
3.0 / 2 # 1.5
3 // 1 # 1
3.0 // 2 # 1.5
```

###  列表

列表由一系列按特定顺序排列的元素组成。你可以创建包含字母表中所有字母、数字0~9或所有家庭成员姓名的列表；也可以将任何东西加入列表中，其中的元素之间可以没有任何关系。

```python
classmates = ['Michael', 'Bob', 'Tracy']
# 在列表中添加新元素时，最简单的方式是将元素附加到列表末尾。
classmates.append('Adam')

classmates.insert(1, 'Jack')

# 要删除list末尾的元素
classmates.pop() 

print(classmates.pop(1))#弹出指定位置的元素

del classmates[0]#删除指定位置元素

classmates.remove('Bob')#根据值删除元素

classmates[1] = 'Sarah' #要把某个元素替换成别的元素，可以直接赋值给对应的索引位置

#list里面的元素的数据类型也可以不同，比如：
L = ['Apple', 123, True]
```

Python为访问最后一个列表元素提供了一种特殊语法。通过将索引指定为-1，可让Python返回最后一个列表元素： 索引-2返回倒数第二个列表元素，索引-3返回倒数第三个列表元素，以此类推。

```python
# 访问列表最后一个元素
classmates[-1]
```

使用方法insert()可在列表的任何位置添加新元素。

```python
motorcycles = ['honda', 'yamaha', 'suzuki'] 

motorcycles.insert(0, 'ducati') 
```

#### 列表排序

sort()函数永久性地修改了列表元素的排列顺序，而sorted()函数只是对序列进行临时排序。

```python
classmates.sort()#对列表进行排序

classmates.sort(reverse=True)#对列表进行反向排序

classmates.reverse()#列表反转

cars = ['bmw', 'audi', 'toyota', 'subaru'] 

print(sorted(cars)) # ['audi', 'bmw', 'subaru', 'toyota']

cars  # ['bmw', 'audi', 'toyota', 'subaru']
```

倒着打印列表

```
cars.reverse()
```

方法reverse()永久性地修改列表元素的排列顺序，但可随时恢复到原来的排列顺序，为此只需对列表再次调用reverse()即可。

#### 使用range()创建数字列表 

```python
# 函数range()从2开始数，然后不断地加2，直到达到或超过终值（11）
even_numbers = list(range(2,11,2))
```

#### 列表解析

列表解析将for循环和创建新元素的代码合并成一行，并自动附加新元素

```python
squares = [value**2 for value in range(1,11)]
print(squares)
```

#### 切片 

```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
# 打印前三个元素
print(players[0:3])
# 提取列表的第2~4个元素
print(players[1:4])
# 没有指定第一个索引，Python将自动从列表开头开始：
print(players[:4])
# Python将返回从第3个元素到列表末尾的所有元素：
print(players[2:])
# Python将返回最后3个元素
print(players[-3:])
# 要复制列表，可创建一个包含整个列表的切片，方法是同时省略起始索引和终止索引（[:]）
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods[:]
```

### 元组

列表非常适合用于存储在程序运行期间可能变化的数据集。列表是可以修改的，这对处理网站的用户列表或游戏中的角色列表至关重要。然而，有时候你需要创建一系列不可修改的元素，元组可以满足这种需求。Python将不能修改的值称为不可变的，而不可变的列表被称为元组。 

```python
classmates = ('Michael', 'Bob', 'Tracy')
t = (1) #表示一个数字1
t=(1,) #表示一个元组
>>> t = ('a', 'b', ['A', 'B'])
>>> t[2][0]
'A'
>>> t[2][0]='X'
>>> t
('a', 'b', ['X', 'B'])
```

虽然不能修改元组的元素，但可以给存储元组的变量赋值。因此，如果要修改前述矩形的尺寸，可重新定义整个元组：

### 循环和匹配

#### 1.input

`input()`读取用户的输入，·input()`返回的数据类型是`str`，`str`不能直接和整数比较，必须先把`str`转换成整数。Python提供了`int()函数来完成这件事情

```python
birth = input('birth: ')
birth = int(birth)
if birth < 2000:
    print('00前')
else:
    print('00后')
```

#### 2.模式匹配

当我们用`if ... elif ... elif ... else ...`判断时，会写很长一串代码，可读性较差。如果要针对某个变量匹配若干种情况，可以使用`match`语句。l类似于java中的switch语句

```python
score = input('请输入你的选择：')
match score:
    case 'A':
        print("score is A")
    case 'B':
        print("score is B")
    case _:
        print("你输入的是什么鬼???")
```

`match`语句除了可以匹配简单的单个值外，还可以匹配多个值、匹配一定范围，并且把匹配后的值绑定到变量：

```python
age = 15
match age:
    case x if x < 10:
        print(f'< 10 years old: {x}')
    case 10:
        print('10 years old.')
    case 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18:
        print('11~18 years old.')
    case 19:
        print('19 years old.')
    case _:
        print('not sure.')
```

`match`语句还可以匹配列表，功能非常强大

```python
args = ['gcc', 'hello.c', 'world.c']
# args = ['clean']
# args = ['gcc']
match args:
    # 如果仅出现gcc，报错:
    case ['gcc']:
        print('gcc: missing source file(s).')
    # 出现gcc，且至少指定了一个文件:
    case ['gcc', file1, *files]:
        print('gcc compile: ' + file1 + ', ' + ', '.join(files))
    # 仅出现clean:
    case ['clean']:
        print('clean')
    case _:
        print('invalid command.')
```

#### 3.break和continue

在循环中，`break`语句可以提前退出循环。

```python
n=1
while n<100:
    n+=1
    print(n)
    if n>30:
        print("今天只打印30个")
        break
print("结束了，回去吧")
```

在循环过程中，也可以通过`continue`语句，跳过当前的这次循环，直接开始下一次循环。

*要特别注意*，**不要滥用`break`和`continue`语句**。`break`和`continue`会造成代码执行逻辑分叉过多，容易出错。大多数循环并不需要用到`break`和`continue`语句

### 使用字典和集合

Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。

```python
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
print(d['Michael']) #95
#通过in判断key是否存在
print('tom' in d) #false
#取得key对应的value值
print(d.get('Michael'))
#删除一个key，用pop(key)方法，对应的value也会从dict中删除
print(d.pop('Bob'))
```

注意：**dict内部存放的顺序和key放入的顺序是没有关系的**。

#### 添加键—值对 

字典是一种动态结构，可随时在其中添加键—值对。要添加键—值对，可依次指定字典名、用方括号括起的键和相关联的值。 

```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)
alien_0['x_point'] = 0
alien_0['y_point'] = 10
print(alien_0)
```

#### 删除键—值对 

对于字典中不再需要的信息，可使用del语句将相应的键—值对彻底删除。使用del语句时，必须指定字典名和要删除的键。

```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)
del alien_0['color']
print(alien_0)
```

#### 遍历字典

```python
user_0 = 
	{ 'username': 'efermi', 
 		'first': 'enrico',
 		'last': 'fermi',
	}
# 遍历键和值    
for key, value in user_0.items():    
    print("key:"+key)    
    print("value:"+value)
# 遍历建
for k in user_0.keys():
    print(k)
# 遍历值
for value in user_0.values():
    print(value)
```

遍历字典时，会默认遍历所有的键，因此，如果将上述代码中的`for k in user_0.keys():`替换为`for k in user_0:`，输出将不变。

#### 按顺序遍历字典中的所有键 

要以特定的顺序返回元素，一种办法是在for循环中对返回的键进行排序。为此，可使用函数sorted()来获得按特定顺序排列的键列表的副本： 

```python
for key in sorted(user_0):    
    print(key)
```

#### 嵌套

有时候，需要将一系列字典存储在列表中，或将列表作为值存储在字典中，这称为嵌套。

```python
# 在列表中嵌套字典
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'yellow', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}
aliens = [alien_2, alien_1, alien_0]
for alien in aliens:    
    print(alien)
# 在字典中嵌套列表    
pizza = {
 'crust': 'thick',
 'toppings': ['mushrooms', 'extra cheese'],
}

for topping in pizza['toppings']:
    print("\t" + topping) # mushrooms extra cheese    
```

注意: 列表和字典的嵌套层级不应太多,如果嵌套层级比前面的示例多得多,很可能有更简单的解决问题的方案。

```python
# 在字典中存储字典
users = {    
	'aeinstein': {        
		'first': 'albert',        
		'last': 'einstein',        
		'location': 'princeton',    
	},    
	'mcurie': {        
		'first': 'marie',        
		'last': 'curie',       
		'location': 'paris',    
	},
}
for username, userinfo in users.items():    
	print(username)    
	print(userinfo)
```

和list比较，dict有以下几个特点：

1. 查找和插入的速度极快，不会随着key的增加而变慢；
2. 需要占用大量的内存，内存浪费多。

而list相反：

1. 查找和插入的时间随着元素的增加而增加；
2. 占用空间小，浪费内存很少。

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

- 要创建一个set，需要提供一个list作为输入集合：
- 重复元素在set中自动被过滤：
- `add(key)`方法可以添加元素到set中，可以重复添加，但不会有效果
- `remove(key)`方法可以删除元素：

```python
s = set([1, 1, 2, 2, 3, 3])
print(s) #{1, 2, 3}
s.add(23)
print(s) #{1, 2, 3, 23}
```

set和dict的唯一区别仅在于没有存储对应的value，但是，set的原理和dict一样，所以，同样不可以放入可变对象，因为无法判断两个可变对象是否相等，也就无法保证set内部"不会有重复元素"。

#### 数据容器的特点

基于各类数据容器的特点，它们的应用场景如下：

- 列表：一批数据，可修改、可重复的存储场景
- 元组：一批数据，不可修改、可重复的存储场景
- 字符串：一串字符串的存储场景
- 集合：一批数据，去重存储场景
- 字典：一批数据，可用Key检索Value的存储场景


#### 字符串的常用方法

```python
str.title()#字符串首字母大写
language.lstrip()#删除左边空格
language.rstrip()#删除右边空格
language.strip()#删除两边空格
age=23
strs=str(age)#整数转换为字符串
```

### 函数

#### 数据类型转换

Python内置的常用函数还包括数据类型转换函数，比如`int()`函数可以把其他数据类型转换为整数

```python
str='345'
print(int(str)) #345
print(float(str)) #345.0
```

#### 定义函数

```python
def my_bas(x):
    if x>=0:
        return x
    else:
        return -x
#函数调用
print(my_bas(-908)) #908
```

#### 空函数

如果想定义一个什么事也不做的空函数，可以用`pass`语句：

```python
def nop():
    pass
```

`pass`可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个`pass`，让代码能运行起来。

函数可以返回多个值,但其实这只是一种假象，Python函数返回的仍然是单一值。原来返回值是一个元组！但是，在语法上，返回一个元组可以省略括号，而多个变量可以同时接收一个元组，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个元组，但写起来更方便。

```python
import math
def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
```

#### 可变参数

```python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
print(calc(1,23,5,5,6))
```

定义可变参数和定义一个list或元组参数相比，仅仅在参数前面加了一个`*`号。在函数内部，参数`numbers`接收到的是一个元组，因此，函数代码完全不变。但是，调用该函数时，**可以传入任意个参数，包括0个参数**：

注意： 传进的所有参数都会被args变量收集，它会根据传进参数的位置合并为一个元组，args是元组类型，这就是位置传递

#### 关键字参数

**参数是"键=值"形式的形式的情况下**, 所有的"键=值"都会被kwargs接受, 同时会根据"键=值"组成字典.

```python
def person(name,age,**kw):
    print('name:',name,'age:',age,'other:',kw)
person('Adam', 45, gender='M', job='Engineer')
extra = {'city': 'Beijing', 'job': 'Engineer'}
person('Jack', 24, city=extra['city'], job=extra['job'])
#name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
#以上参数传递方式的简易写法
person('Jack', 24, **extra)
#name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
```

#### 命名关键字参数

命名关键字参数需要一个特殊分隔符`*`，`*`**后面的参数被视为命名关键字参数**。命名关键字参数必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错：

```python
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

命名关键字参数可以有缺省值，从而简化调用，由于命名关键字参数`city`具有默认值，调用时，可不传入`city`参数：

```python
def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
def person(name, age, city, job):
    # 缺少 *，city和job被视为位置参数
    pass
"""
city 参数是一个命名关键字参数，这意味着在调用函数时必须使用关键字 city 来指定其值，而不能省略。job 是一个普通的关键字参数，可以在调用时使用关键字指定，也可以省略，如果省略了 job，则它将不会被传递给函数。
"""
person("tom", 12, city="上海", job="程序员")
```

#### 递归函数

如果一个函数在内部调用自身本身，这个函数就是递归函数。

```python
def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)
```

递归函数的优点是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。使用递归函数需要注意防止栈溢出。

##### **尾递归**优化

尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

上面的`fact(n)`函数由于`return n * fact(n - 1)`引入了乘法表达式，所以就不是尾递归了。要改成尾递归方式，需要多一点代码，主要是要把每一步的乘积传入到递归函数中：

```python
def fact_iter(num, product):
    if num == 1:
        return product
    return fact_iter(num - 1, num * product)
```

#### lambda匿名函数 

- def关键字，可以定义带有名称的函数 
- lambda关键字，可以定义匿名函数（无名称） 
- 有名称的函数，可以基于名称重复使用;无名称的匿名函数，**只可临时使用一次**。

```python
lambal 传入参数:函数体
```

lambda 是关键字，表示定义匿名函数 ，传入参数表示匿名函数的形式参数，如：x, y 表示接收2个形式参数 ，函数体，就是函数的执行逻辑，要注意：**只能写一行**，无法写多行代码

```python
def test_func(compute):
    result = compute(1, 2)
    print(f"结果是:{result}")
# 通过lambda匿名函数的形式，将匿名函数作为参数传入
def add(x, y):
    return x + y
test_func(add)
test_func(lambda x, y: x + y)
```

#### 将函数存储在模块中

函数的优点之一是，使用它们可将代码块与主程序分离。可以将函数存储在被称为模块的独立文件中，再将模块导入到主程序中。import语句允许在当前运行的程序文件中使用模块中的代码。

```python
import pizza
pizza.make_pizza(16, '蘑菇')
pizza.make_pizza(12, '蘑菇', '辣椒', '茄子')
```

还可以导入模块中的特定函数，这种导入方法的语法如下： 

```python
from module_name import function_name 

# 通过用逗号分隔函数名，可根据需要从模块中导入任意数量的函数：
from module_name import function_0, function_1, function_2
```

##### 函数指定别名

如果要导入的函数的名称可能与程序中现有的名称冲突，或者函数的名称太长，可指定简短而独一无二的别名

```python
from pizza import make_pizza as mp

mp(16, 'pepperoni')
mp(12, 'mushrooms', 'green peppers', 'extra cheese') 

# 使用星号（*）运算符可让Python导入模块中的所有函数
from pizza import * 
```

## 高级语法

### 高级特性

#### 切片

`L[0:3]`表示，从索引`0`开始取，直到索引`3`为止，但不包括索引`3`。即索引`0`，`1`，`2`，正好是3个元素。

```python
L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
print(L[0:3]) #['Michael', 'Sarah', 'Tracy']
print(L[2:4])#['Tracy', 'Bob']
#最后两个值
print(L[-2:])#['Bob', 'Jack']
#前5个数每两个去一个
print(L[:4:2])
#甚至什么都不写，只写[:]就可以原样复制一个list：
print(L[:])
```

#### 列表生成式

Python内置的非常简单却强大的可以用来创建list的生成式。如果要生成`[1x1, 2x2, 3x3, ..., 10x10]`方法一：循环

```python
L = []
for x in range(1,11):
    L.append(x * x)
print(L) # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

但是循环太繁琐，而**列表生成式**则可以用一行语句代替循环生成上面的list：

```python
print([x*x for x in range(1,11)]) # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]、
print([m + n for m in 'abc' for n in 'xyz']) # ['ax', 'ay', 'az', 'bx', 'by', 'bz', 'cx', 'cy', 'cz']
```

注意：列表生成式不能在最后的`if`加上`else`：

```python
print([x*x for x in range(1,11) if x%2==0]) # [4, 16, 36, 64, 100]
[x for x in range(1, 11) if x % 2 == 0 else 0]
#  File "<stdin>", line 1
#    [x for x in range(1, 11) if x % 2 == 0 else 0]
```

判断变量的数据类型

```python
x ='123'
y = 123
isinstance(x ,str) # True
isinstance(y , str) # false
```

#### 生成器

创建`L`和`g`的区别仅在于最外层的`[]`和`()`，`L`是一个list，而`g`是一个generator。

```python
L = [x * x for x in range(10)] # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
g = (x * x for x in range(10)) # <generator object <genexpr> at 0x000001F790B26AC0>
```

在Python中，这种**一边循环一边计算**的机制，称为生成器：generator

generator保存的是算法，每次调用`next(g)`，就计算出`g`的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出`StopIteration`的错误。

我们创建了一个generator后，基本上永远不会调用`next()`，而是通过`for`循环来迭代它

```python
g=(x*x for x in range(10))#定义一个生成器
for n in g:
    print(n) #  0 1 4 9 16 25 36 49 64 81
```

generator函数和普通函数的执行流程不一样。

- 普通函数是顺序执行，遇到`return`语句或者最后一行函数语句就返回。
- 而变成generator的函数，**在每次调用`next()`的时候执行，遇到`yield`语句返回**，再次执行时从上次返回的`yield`语句处继续执行。

如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator函数，调用一个generator函数将返回一个generator：

```python
def _feibo(max):
    n,a,b=0,0,1
    while n<max:
        a,b=b,a+b #相当于t=(a,a+b),a=t[0],b=t[1]
        n=n+1
        yield b 
        # print(b)
    return 'done'
print(_feibo(10))
```

### 函数式编程

函数本身也可以赋值给变量，即:**变量可以指向函数**，如果一个变量指向了一个函数，那么，可通过该变量来调用这个函数

```python
f=abs
# 直接调用abs()函数和调用变量f()完全相同
f(-10) #10,
```

把`abs`指向`10`后，就无法通过`abs(-10)`调用该函数了！因为`abs`这个变量已经不指向求绝对值函数而是指向一个整数`10`

```python
abs=10
print(abs(-10))
#Traceback (most recent call last):
 # File "E:\code\pythonCode\test\Test02.py", line 20, in <module>
 # print(abs(-10))
#TypeError: 'int' object is not callable**
```

#### 高阶函数

既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为**高阶函数**

```python
def add(x, y, f):
    return f(x,y) + f(y,y)
print(add(-5, 6, abs)) # 11
```

##### map

`map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回。

```python
def f(x):
    return x+x
r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
print(list(r))#[2, 4, 6, 8, 10, 12, 14, 16, 18]
```

##### reduce

reduce把一个函数作用在一个序列$[x_1, x_2, x_3, ...]$上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算，其效果就是：

```python
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
# 示例
from functools import reduce
def add(x,y):
    return x+y
print(reduce(add,[1,2,3,4,5,6,7,8])) # 36
```

##### filter

$filter()$函数用于过滤序列。和`map()`类似，$filter()$也接收一个函数和一个序列

和`map()`不同的是，$filter()$把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素。

```python
def is_odd(n):
    return n % 2 == 1
list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
# 结果: [1, 5, 9, 15]
```

##### sorted

`sorted()`函数就可以对list进行排序

#### 返回函数

高阶函数除了可以接受函数作为参数外，还可以把函数作为结果值返回。

```python
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum
print(lazy_sum(1,2,3,4)) # 返回的不是求和结果，而是求和函数sum
sums =lazy_sum(1,2,3,4)
print(sums()) # 调用函数sums时，才真正计算求和的结果：
```

在这个例子中，我们在函数`lazy_sum`中又定义了函数`sum`，并且，内部函数`sum`可以引用外部函数`lazy_sum`的参数和局部变量，当`lazy_sum`返回函数`sum`时，相关参数和变量都保存在返回的函数中，这种称为"闭包（Closure）"的程序结构拥有极大的威力

注意：当我们调用`lazy_sum()`时，每次调用都会返回一个新的函数，即使传入相同的参数：

```python
sums =lazy_sum(1,2,3,4)
sums2=lazy_sum(1,2,3)
print(sums == sums2) # false
```

#### 闭包

```python
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs
f1, f2, f3 = count()
print(f1()) # 9
print(f2()) # 9
print(f3()) # 9
```

在上面的例子中，每次循环，都创建了一个新的函数，然后，把创建的3个函数都返回了。实际结果是三个9，原因就在于返回的函数引用了变量`i`，但它并非立刻执行。等到3个函数都返回时，它们所引用的变量`i`已经变成了`3`，因此最终结果为`9`

**返回闭包时牢记一点：返回函数不要引用任何循环变量，或者后续会发生变化的变量。**

如果一定要引用循环变量怎么办？方法是再创建一个函数，用该函数的参数绑定循环变量当前的值，无论该循环变量后续如何更改，已绑定到函数参数的值不变：

```python
def count2():
    def f(j):
        def g():
            return j*j
        return g
    fs = []
    for i in range(1, 4):
        fs.append(f(i)) # f(i)立刻被执行，因此i的当前值被传入f()
    return fs
f4, f5, f6 = count2()
print(f4()) # 1
print(f5()) # 4
print(f6()) # 9
```

#### nonlocal

使用闭包，就是内层函数引用了外层函数的局部变量。如果只是读外层变量的值，我们会发现返回的闭包函数调用一切正常：

```python
def inc():
    x = 0
    def fn():
        # 仅读取x的值:
        return x + 1
    return fn
f = inc()
print(f()) # 1
print(f()) # 1
```

但是，如果修改外部变量的值会报错

```python
def inc1():
    x = 0
    def fn():
        # nonlocal x
        x = x + 1
        return x
    return fn
f = inc1()
print(f()) # 1
print(f()) # 2
"""
UnboundLocalError: local variable 'x' referenced before assignment
"""
```

原因是`x`作为局部变量并没有初始化，直接计算`x+1`是不行的。但我们其实是想引用`inc()`函数内部的`x`，所以需要在`fn()`函数内部加一个`nonlocal x`的声明。加上这个声明后，解释器把`fn()`的`x`看作外层函数的局部变量，它已经被初始化了，可以正确计算`x+1`。

**注意：使用闭包时，对外层变量赋值前，需要先使用nonlocal声明该变量不是当前函数的局部变量。**

#### 匿名函数

当我们在传入函数时，有些时候，不需要显式地定义函数，直接传入匿名函数更方便。

```python
print(list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9])))
"""
匿名函数lambda x: x * x实际上就是：
def f(x):
    return x * x
"""
```

关键字`lambda`表示匿名函数，冒号前面的`x`表示函数参数。匿名函数有个限制，就是只能有一个表达式，不用写`return`，返回值就是该表达式的结果。

用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量，再利用变量来调用该函数：

同样，也可以把匿名函数作为返回值返回

```python
def build(x, y):
    return lambda: x * x + y * y
```

#### 装饰器

由于函数也是一个对象，而且函数对象可以被赋值给变量，所以，通过变量也能调用该函数。

```python
def now():
    print('20240423')
f = now
print(now.__name__) # 打印函数名
print(f.__name__) # 打印函数名
```

假设我们要增强`now()`函数的功能，比如，在函数调用前后自动打印日志，但又不希望修改`now()`函数的定义，这种在代码运行期间动态增加功能的方式，称之为"装饰器"

#### 偏函数

### 文件操作

#### 文件的读取

使用open函数，可以打开一个已经存在的文件，或者创建一个新文件

- name：是要打开的目标文件名的字符串(可以包含文件所在的具体路径)。 

- mode：设置打开文件的模式(访问模式)：只读、写入、追加等。 

- encoding:编码格式（推荐使用UTF-8） 


```python
f = open("D:/ruanjian/LICENSE.txt", "r", encoding="UTF-8")
```

##### read()方法

```python
f.read(num)
```

num表示要从文件中读取的数据的长度（字节）,如果没有传入num，那么就表示读取文件中所有的数据。

##### readlines()

readlines可以按照行的方式把整个文件中的内容进行一次性读取，并且返回的是一个**列表**，其中每一行的数据为一个元素。

```python
f = open('python.txt')
content = f.readlines()
# ['hello world\n', 'abcdefg\n', 'aaa\n', 'bbb\n', 'ccc']
print(content)
# 关闭文件
f.close()
```

##### readline()

一次读取一行内容

```python
line=f.readline()
```

循环读取行

```python
n=1
for line in f:
    n=n+1
    print("第",n,"行是:",line)
```

**close()关闭文件对象**

最后通过close，关闭对文件的占用 ， 如果不调用close,同时程序没有停止运行，那么这个文件将一直被Python程序占用。

**注意：使用with open语法打开文件，可以自动关闭**

##### 二进制文件

要读取二进制文件，比如图片、视频等等，用`'rb'`模式打开文件即可：

```python
f = open('data/image.png', 'rb')
f.read()
```

##### 字符编码

要读取非UTF-8编码的文本文件，需要给`open()`函数传入`encoding`参数，例如，读取GBK编码的文件

```python
f = open('data/翻译语料zh.txt', 'r',encoding='gbk')
f.read()
```

在文本文件中可能夹杂了一些非法编码的字符。影响文件的读取，遇到这种情况，`open()`函数还接收一个`errors`参数，表示如果遇到编码错误后如何处理。最简单的方式是直接忽略：

```python
f = open('data/翻译语料zh.txt', 'r',encoding='gbk', errors='ignore')
f.read()
```

#### 文件的写入 

传入标识符`'w'`或者`'wb'`表示写文本文件或写二进制文件：

```python
f = open('E:\code\\test.txt', 'w')
f.write('hello world,张三')
f.flush()
```

- 以`'w'`模式写入文件时，如果文件已存在，会直接覆盖（相当于删掉后新写入一个文件）。如果我们希望追加到文件末尾时，可以传入`'a'`以追加（append）模式写入。
- 当我们写文件时，操作系统往往不会立刻把数据写入磁盘，而是放到内存缓存起来，空闲的时候再慢慢写入。只有调用`close()`方法时，操作系统才保证把没有写入的数据全部写入磁盘。忘记调用`close()`的后果是数据可能只写了一部分到磁盘，剩下的丢失了。所以，还是用`with`语句比较好：

```python
with open('data/翻译语料zh.txt', 'w') as f:
	f.write('Hello, world!')
```

#### 文件的追加

```python
f = open('E:\code\\test.txt', 'a')
f.write('hello world,你好啊')
f.flush()
```

- w模式，文件不存在会创建文件 

- a模式，文件存在会在最后，追加写入文件

#### StringIO和BytesIO

`StringIO`顾名思义就是在内存中读写`str`。要把`str`写入`StringIO`，我们需要先创建一个`StringIO`，然后，像文件一样写入即可：

```python
from io import StringIO
f = StringIO()
f.write('hello world')
# getvalue()方法用于获得写入后的str。
print(f.getvalue())
```

##### BytesIO

`StringIO`操作的只能是`str`，如果要操作二进制数据，就需要使用`BytesIO`。

`BytesIO`实现了在内存中读写`bytes`，我们创建一个``Bytes`IO`，然后写入一些bytes：

```python
from io import BytesIO
f = BytesIO()
f.write('中文'.encode('utf-8'))
print(f.getvalue())
```

#### 操作文件和目录

使用`os`模块的基本功能

```python
import os 
print(os.name) # 操作系统类型
print(os.environ) # 查看环境变量
# 要获取某个环境变量的值
print(os.environ.get('PATH'))
# 查看当前文件的绝对路径
print( os.path.abspath('.'))
```

操作文件夹

```python
# 在某个目录下创建一个新目录，首先把新目录的完整路径表示出来
os.path.join('./','test')
# 然后创建目录
os.mkdir('./test')
# 删除目录
os.rmdir('test')
```

把两个路径合成一个时，不要直接拼字符串，而要通过`os.path.join()`函数，这样可以正确处理不同操作系统的路径分隔符。

同样的道理，要拆分路径时，也不要直接去拆字符串，而要通过`os.path.split()`函数，这样可以把一个路径拆分为两部分，后一部分总是最后级别的目录或文件名

```python
# ('/Users/michael/testdir', 'file.txt')
os.path.split('/Users/michael/testdir/file.txt')
# 文件重命名
os.rename('test.txt', 'test.py')
# 删除文件
os.remove('test.py')
```

`shutil`模块提供了`copyfile()`的函数，你还可以在`shutil`模块中找到很多实用函数，它们可以看做是`os`模块的补充。

```python
# 列出当前目录下的所有文件和目录
[x for x in os.listdir('.') if os.path.isdir(x)]
# 列出所有的py文件
[x for x in os.listdir('.') if os.path.isfile(x) and os.path.splitext(x)[1]=='.py']
```

#### 序列化和反序列化

把变量从内存中变成可存储或传输的过程称之为序列化，在Python中叫pickling

- 序列化之后，就可以把序列化后的内容写入磁盘，或者通过网络传输到别的机器上。
- 反过来，把变量内容从序列化的对象重新读到内存里称之为反序列化，即unpickling。

把一个对象序列化并写入文件：

`pickle.dumps()`方法把任意对象序列化成一个`bytes`，然后，就可以把这个`bytes`写入文件。或者用另一个方法`pickle.dump()`直接把对象序列化后写入一个文件：

```python
import pickle
d = dict(name='Bob', age=20, score=88)
# print(pickle.dumps(d))
f = open('dump.txt','wb')
pickle.dump(d,f)
f.close()
```

当我们要把对象从磁盘读到内存时，可以先把内容读到一个`bytes`，然后用`pickle.loads()`方法反序列化出对象，也可以直接用`pickle.load()`方法从一个`file-like Object`中直接反序列化出对象。我们打开另一个Python命令行来反序列化刚才保存的对象：

```python
f = open('dump.txt', 'rb')
d = pickle.load(f)
print(d)
f.close()
```

#### JSON

我们可以使用json对象，保存序列化后的数据，我们可以将字典转换为json对象，也可以将json对象反序列化

```python
dict = dict(name='Bob', age=20, score=88)
# Python对象变成一个JSON
print(json.dumps(dict))

jsons = '{"name": "Bob", "age": 20, "score": 88}'
# 用loads()或者对应的load()方法，前者把JSON的字符串反序列化
print(json.loads(jsons))
```

json对python对象进行处理的时候有一个问题，对象不是一个可序列化为JSON的对象。为了解决这个问题，可选参数的`default`就是把任意一个对象变成一个可序列为JSON的对象，我们只需要为`Student`专门写一个转换函数，再把函数传进去即可：

```python
class Student(object):
    def __init__(self, name, age, score):
        self.name = name
        self.age = age
        self.score = score
def student2dict(std):
    return {
        'name': std.name,
        'age': std.age,
        'score': std.score
    }
s = Student('Bob', 20, 88)
print(json.dumps(s,default=student2dict))
```

### Python异常、模块与包

#### 异常处理

捕获异常的作用在于：提前假设某处会出现异常，做好提前准备，当真的出现异常的时候，可以有后续手段。

基本语法

```python
try: 
    可能发生错误的代码 
except: 
    如果出现异常执行的代码
```

##### 捕获指定异常

```python
try: 
    print(name) 
except NameError as e: 
    print('name变量名称未定义错误')
```

注意：

- 如果尝试执行的代码的异常类型和要捕获的异常类型不一致，则无法捕获异常。

- 一般try下方只放一行尝试执行的代码。


##### 捕获多个异常

当捕获多个异常时，可以把要捕获的异常类型的名字，放到except 后，并使用元组的方式进行书写。

```python
try:
    print(1/0)
except (NameError, ZeroDivisionError):
    print('ZeroDivision错误...')
```

##### 捕获异常并输出描述信息

```python
try:
    print(num)
except (NameError, ZeroDivisionError) as e:
    print(e)
```

##### 捕获所有异常

```python
try:
    print(name)
except Exception as e:
    print(e)
```

##### 异常else

else表示的是如果没有异常要执行的代码。

```python
try:
    print(1)
except Exception as e:
    print(e)
else:
    print('我是else，是没有异常的时候执行的代码')
```

##### 异常finally

finally表示的是无论是否异常都要执行的代码，例如关闭文件。 

```python
try:
    f = open('test.txt', 'r')
except Exception as e:
    f = open('test.txt', 'w')
else:
    print('没有异常，真开心')
finally:
    f.close()
```

#### 异常的传递

异常是具有传递性的 

当函数$func01$中发生异常, 并且没有捕获处理这个异常的时候, 异常会传递到函数$func02$, 当$func02$也没有捕获处理这个异常的时候 main函数会捕获这个异常

提示: **当所有函数都没有捕获异常的时候, 程序就会报错**

#### Python模块

以内建的`sys`模块为例，编写一个`hello`的模块：

```python
#!/usr/bin/env python3		 # 可以让这个hello.py文件直接在Unix/Linux/Mac上运行
# -*- coding: utf-8 -*-		 # .py文件本身使用标准UTF-8编码
' a test module '		     # 模块的文档注释，任何模块代码的第一个字符串都被视为模块的文档注释；
__author__ = 'Michael Liao'	  # __author__变量把作者写进去

import sys
def test():
    args = sys.argv
    if len(args)==1:
        print('Hello, world!')
    elif len(args)==2:
        print('Hello, %s!' % args[1])
    else:
        print('Too many arguments!')

if __name__=='__main__':
    test()
```

模块就是一个Python文件，里面有类、函数、变量等，我们可以 拿过来用（导入模块去使用）导入模块的语法

```python
from 模块名 import 模块|类|函数|变量|*  as 别名
```

常用的组合形式如： 

- import 模块名 

- from 模块名 import 类、变量、方法等 

- from 模块名 import * 

- import 模块名 as 别名 

- from 模块名 import 功能名 as 别名


```python
# 导入时间模块
import time
print("开始")
# 让程序睡眠1秒(阻塞)
time.sleep(1)
print("结束")
```

from 模块名 import 功能名

```python
from time import sleep
print("开始")
sleep(10)
print("结束")
```

from 模块名 import *

```python
from time import *
print("开始")
sleep(3)
print("结束")
```

as定义别名

```python
# 模块定义别名
import 模块名 as 别名
# 功能定义别名
from 模块名 import 功能 as 别名
```

```python
# 功能别名
from time import sleep as sl
print("开始")
sl(10)
print("结束")
# 模块别名
import time as tt
tt.sleep(2)
print('hello')
```

##### 自定义模块

 每个Python文件都可以作为一个模块，模块的名字就是文件的名字. 也就是说自定义模块名必须要符合标识符命名规则

定义一个module模块	MyModule.py

```python
def test(a, b):
    print(a + b)
```

```python
#在其他模块里面引用
import MyModule
MyModule.test(10,23)
```

注意事项：当导入多个模块的时候，且模块内有同名功能. 当调用这个同名功能的时候，调用到的是后面导入的模块的功能

自定义模块

```python
__all__=['testA']
def testA():
    print('这是testa')

def testB():
    print("this is test b")
```

测试模块

```python
from MyModule import *
testA()
testB()#不能调用b
#NameError: name 'testB' is not defined
```

#### Python包

基于Python模块，我们可以在编写代码的时候，导入许多外部代码来丰富功能。 但是，如果Python的模块太多了，就可能造成一定的混乱

使用方式：

- 新建包`my_package` 

- 新建包内模块：`my_module1` 和 `my_module2` 

- 模块内代码如下


```python
#模块一 my_module1.py
def testModuleOne(a, b):
    print(a + b)
    print("我是模块1")
#模块2 my_module2.py
def testModuleTwo(a, b):
    print(a - b)
    print("我是模块2")
```

在其他python文件中引入

```python
from my_package import my_module1
from my_package import my_module2
my_module1.testModuleOne(12,23)
my_module2.testModuleTwo(12,234)
```

引入方式二： 

注意：必须在`__init__.py`文件中添加`__all__ = []`，控制允许导入的模块列表

init文件

```python
__all__=['my_module2']
```

测试文件

```python
from my_package import *
my_module2.testModuleTwo(12,23) #因为此处只引入了module2，所以module1不能使用
```

##### 第三方包

在Python程序的生态中，有许多非常多的第三方包，可以极大的帮助我们提高开发效率，如： 

- 科学计算中常用的：numpy包 

- 数据分析中常用的：pandas包 
- 大数据计算中常用的：pyspark、apache-flink包 
- 图形可视化常用的：matplotlib、pyecharts 
- 人工智能常用的：tensorflow 

连接国内的网站进行包的安装： 

https://pypi.tuna.tsinghua.edu.cn/simple 是清华大学提供的一个网站，可供pip程序下载第三方包

```cmd
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名称
```

### 面向对象

在创建实例的时候，把一些我们认为必须绑定的属性强制填写进去。通过定义一个特殊的`__init__`方法，在创建实例的时候，就把`name`，`score`等属性绑上去：

```python
class 类名称:
    成员变量
    成员方法
class Student(object):
    def __init__(self, name, score):
        self.name = name
        self.score = score
        
    def print_score(self):
        print('%s: %s' % (self.name, self.score))    
```

#### 成员方法的定义

和普通的函数相比，在类中定义的函数只有一点不同，就是第一个参数永远是实例变量`self`，并且，调用时，不用传递该参数。除此之外，类的方法和普通函数没有什么区别

self主要有以下几个特点：

- self用来表示类对象自身的意思 
- 当我们使用类对象调用方法的是，self会自动被python传入 
- 在方法内部，想要访问类的成员变量，必须使用self

```python
# 定义一个带有成员方法的类
class Student:
    name = None     # 学生的姓名
    def __init__(self, age, score):
        self.age = age
        self.score = score
    def say_hi(self):
        print(f"大家好呀，我是{self.name}，欢迎大家多多关照")
    def say_hi2(self, msg):
        print(f"大家好，我是：{self.name}，{msg}")
stu = Student()
stu.name = "周杰轮"
stu.say_hi2("哎哟不错哟")

stu2 = Student()
stu2.name = "林俊节"
stu2.say_hi2("小伙子我看好你")
```

需要说明的是，上述的name是属于类属性，这个属性虽然归类所有，但类的所有实例都可以访问到。其他的属性是实例属性，比如age和score这些变量。

self关键字，尽管在参数列表中，但是**传参的时候可以忽略它**。

```python
class Student:
    name = None     # 学生的姓名
    def say_hiNoParam(self):
        print("无参数打印出来结果")
stu =Student()
stu.say_hi()#无参数打印出来结果
```

#### 访问限制

在Python中，实例的变量名如果以`__`开头，就变成了一个私有变量，只有内部可以访问，外部不能访问，想让外部变访问的化，可以对外提供一个方法

```python
class Student(object):
    def __init__(self, name, score):
        #内部变量的写法
        self.__name = name
        self.__score = score
    def get_name(self):
        return self.__name
    def get_score(self):
        return self.__score   
print(tom.get_name())    
```

如果想要允许外部代码修改内部变量，可以给类增加`set`方法

```python
class Student(object):
    def __init__(self, name, score):
        #内部变量的写法
        self.__name = name
        self.__score = score
    def set_score(self, score):
        if 0 <= score <= 100:
            self.__score = score
        else:
            raise ValueError('bad score')
 tom.set_score(12)           
```

Python中，变量名类似`__xxx__`的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的

虽然不能直接访问`__name`，但是，仍然可以通过`_Student__name`来访问`__name`变量：

```java
tom._Student__name
```

#### 获取对象信息

判断对象类型，使用`type()`函数，基本类型都可以用`type()`判断：

```python
print(type(123))
print(type(123)==int)
```

判断class的类型，可以使用`isinstance()`函数。

```python
a = Animal()
b = Dog()
print(isinstance(a,Animal)) # true
print(isinstance(b,Animal)) # true
print(isinstance(b,Dog)) 	# true 
```

用`type()`判断的基本类型也可以用`isinstance()`判断：

```python
isinstance('a', str)
```

还可以判断一个变量是否是某些类型中的一种，比如下面的代码就可以判断是否是list或者tuple：

```python
isinstance([1, 2, 3], (list, tuple)) # True
isinstance((1, 2, 3), (list, tuple)) # True
```

如果要获得一个对象的所有属性和方法，可以使用`dir()`函数，它返回一个包含字符串的list

```python
print(dir('ABC'))
# [__add__', '__class__', '__contains__', '__delattr__', '__dir__'...]
```

类似`__xxx__`的属性和方法在Python中都是有特殊用途的，比如`__len__`方法返回长度，所以以下写法其实效果一样

```python
len('ABC') #3
'ABC'.__len__() #3
```

#### 使用__slots__

为了限制该`class`实例能添加的属性，Python允许在定义`class`的时候，定义一个特殊的`__slots__`变量，来限制

```python
class Teacher(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称

t = Teacher()
t.name = "张三"
t.score = 12 # AttributeError: 'Teacher' object has no attribute 'score'
```

使用`__slots__`要注意，`__slots__`定义的属性仅对当前类实例起作用，对继承的子类是不起作用的。

#### 使用@property

Python内置的`@property`装饰器就是负责把一个方法变成属性调用的。

- 使用 `@property` 可以控制对属性的访问，确保数据的封装和安全。
- 如果只需要获取属性的值，而不需要设置值，可以只定义 `@property` 方法。

```python
class Student(object):
    @property
    def score(self):
        return self._score
    
    @score.setter
    def score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0 ~ 100!')
        self._score = value
```

#### 构造方法

Python类可以使用：__init__()方法，称之为构造方法。

- 在创建类对象（构造类）的时候，会自动执行
- 在创建类对象（构造类）的时候，将传入参数自动传递给__init__方法使用。

```python
class Student:
    def __init__(self, name, age ,tel):
        self.name = name
        self.age = age
        self.tel = tel
        print("Student类创建了一个类对象")
stu = Student("周杰轮", 31, "18500006666")
print(stu.name)
print(stu.age)
print(stu.tel)
```

注意:

- **千万不要忘记init前后都有2个下划线**
- 构造方法也是成员方法，不要忘记在参数列表中提供：self 
- 在构造方法内定义成员变量，需要使用self关键字，变量是定义在构造方法内部，如果要成为成员变量，需要用self来表示。

#### 魔术方法

**str 字符串方法**

我们可以通过__str__方法，控制类转换为字符串的行为。

```python
def __str__(self):
    return f"student类对象，name={self.name},age={self.age},tel={self.tel}"
stu = Student("周杰轮", 31, "18500006666")
print(str(stu))
```

**lt 小于符号**

在类中实现__lt__方法，即可同时完成：小于符号 和 大于符号 2种比较

```python
def __lt__(self, other):
    return self.age < other.age
stu = Student("周杰轮", 31, "18500006666")
stu1=Student("张安",12,"12344546")
print(stu<stu1) #false
```

**le 小于等于比较符号方法**

__le__可用于：<=、>=两种比较运算符上。

```python
def __le__(self, other):
     return self.age <= other.age
stu = Student("周杰轮", 31, "18500006666")
stu1=Student("张安",12,"12344546")
print(stu<stu1) #false
```

**eq，比较运算符实现方法**

- 不实现__eq__方法，对象之间可以比较，但是是比较内存地址，也即是：不同对象==比较一定是False结果。  
- 实现了__eq__方法，就可以按照自己的想法来决定2个对象是否相等了。

```python
def __eq__(self, other):
    return self.age == other.age
stu1 = Student("周杰轮", 31)
stu2 = Student("林俊节", 36)
print(stu1 == stu2)
```

#### 封装 

##### 私有成员

定义私有成员的方式非常简单，只需要： 

- 私有成员变量：变量名以__开头（2个下划线） __

- 私有成员方法：方法名以__开头（2个下划线） 即可完成私有成员的设置


在类中提供仅供内部使用的属性和方法，而不对外开放（类对象无法使用）

```python
class Phone:
    __current_voltage = 0.5        # 当前手机运行电压
    def __keep_single_core(self):
        print("让CPU以单核模式运行")
    def call_by_5g(self):
        if self.__current_voltage >= 1:
            print("5g通话已开启")
        else:
            self.__keep_single_core()
            print("电量不足，无法使用5g通话，并已设置为单核运行进行省电。")
phone = Phone()
phone.call_by_5g()
```

#### 继承

继承分为：单继承和多继承 。 

##### 单继承

继承表示：将从父类那里继承（复制）来成员变量和成员方法（不含私有）

```python
class Animal(object):
    def run(self):
        print('Animal is running...')
        
class Dog(Animal):
    def run(self):
        print('Dog is running...')

class Cat(Animal):
    def run(self):
        print('Cat is running...')
dog = Dog()
cat = Cat()
dog.run() # Dog is running...
cat.run() # Cat is running...
```

当子类和父类都存在相同的`run()`方法时，我们说，子类的`run()`覆盖了父类的`run()`，在代码运行的时候，总是会调用子类的`run()`。这样，我们就获得了继承的另一个好处：多态。多态是同一个接口可以被不同的对象以不同的方式实现，在这里不同的动物类都可以按照自己的需求实现run这个方法。

##### 多继承

Python的类之间也支持多继承，即一个类，可以继承多个父类，通过多重继承，一个子类就可以同时获得多个父类的所有功能。

```python
class Animal(object):
    def run(self):
        print('Animal is running...')
class Runnable(object):
    def run(self):
        print('Running...')

class Flyable(object):
    def fly(self):
        print('Flying...')
class Dog(Animal, Runnable):
    pass     
class Bat(Animal, Flyable):
    pass
```

多个父类中，如果有同名的成员，那么默认以继承顺序（从左到右）为优先级。 即：**先继承的保留，后继承的被覆盖**

pass是占位语句，用来保证函数（方法）或类定义的完整性，表示无内容，空的意思

##### MixIn

Mixin是一种设计模式，它允许将可重用的功能添加到类中，而不需要通过继承关系来实现。Mixin类通常包含一组方法，这些方法可以被其他类继承，以增强其功能。Mixin类本身可能不包含任何数据，或者只包含一些基本的数据。

```python
class LoggerMixin:
    def log(self, message):
        print(f"LOG: {message}")

class User(LoggerMixin):
    def __init__(self, username):
        self.username = username

    def login(self):
        self.log(f"User {self.username} logged in")

class PaymentProcessor(LoggerMixin):
    def __init__(self, processor_name):
        self.processor_name = processor_name

    def process_payment(self):
        self.log(f"Payment processed by {self.processor_name}")

user = User("Alice")
user.login()  # 输出: LOG: User Alice logged in

payment_processor = PaymentProcessor("PayPal")
payment_processor.process_payment()  # 输出: LOG: Payment processed by PayPal
```

##### 复写 

子类继承父类的成员属性和成员方法后，如果对其"不满意"，那么可以进行复写。 即：在子类中重新定义同名的属性或方法即可

```python
class Phone:
    Item=None
    product=None
    def call_by_4g(self):
        print("可以进行4g通话")
    def call_by5g(self):
        print("父类的5g")
class PhonePlus(Phone):
    face_id=None,
    def call_by_5g(self):
        # 使用被复写的父类的成员
        super().call_by5g()#父类的5g
        print("子类的5g，可以进行5g通话")
phone2=PhonePlus()
phone2.call_by_5g()#可以进行5g通话
```

如果需要使用被复写的父类的成员，需要特殊的调用方式: 

方式1： 

调用父类成员 使用成员变量：

​		父类名.成员变量 使用成员方法：

​		父类名.成员方法(self)

```python
print(f"父类的厂商是：{Phone.producer}")
Phone.call_by_5g(self)
```

 • 使用super()调用父类成员 使用成员变量：

​		super().成员变量 使用成员方法：

​		super().成员方法()

```python
def call_by_5g(self):
    # 使用被复写的父类的成员
    super().call_by5g()#父类的5g
    print("子类的5g，可以进行5g通话")
```

#### 类型注解 

类型注解：在代码中涉及数据交互的地方，提供数据类型的注解（显式的说明）。 

- 帮助第三方IDE工具对代码进行类型推断，协助做代码提示 

- 帮助开发者自身对变量进行类型注释支持： 

- 变量的类型注解 、函数（方法）形参列表和返回值的类型注解


```python
var_int:int=10
var_float:float=10.0
var_str:str="你好"
#类对象注解
cat:Cat=Cat()
cat.spark()
# 基础容器类型注解
my_list: list = [1, 2, 3]
my_tuple: tuple = (1, 2, 3)
my_dict: dict = {"itheima": 666}
my_list: list[int] = [1, 2, 3]
my_tuple: tuple[int, str, bool] = (1, "itheima", True)
my_dict: dict[str, int] = {"itheima": 666}
```

注意： 

- 元组类型设置类型详细注解，需要将每一个元素都标记出来 

- 字典类型设置类型详细注解，需要2个类型，第一个是key第二个是value


##### 函数的类型注解

函数和方法的形参类型注解语法：

```python
def 函数名(形参:类型,形参:类型...):
	pass
# 对形参进行类型注解
def add(x: int, y: int):
    return x + y
```

函数的类型注解 - 返回值注解

```python
def 函数名(形参:类型,形参:类型...)->返回值类型:
	pass
# 对返回值进行类型注解
def func(data: list) -> list:
    return data
```

##### Union类型 

Union联合类型注解，在变量注解、函数形参和返回值注解中，均可使用。

```python
# 使用Union类型，必须先导包
from typing import Union
my_list: list[Union[int, str]] = [1, 2, "itheima", "itcast"]
def func(data: Union[int, str]) -> Union[int, str]:
    pass
```

#### 抽象类（接口）

 包含抽象方法的类，称之为抽象类。抽象方法是指：没有具体实现的方法（pass） 称之为抽象方法

#### 枚举类

Python提供了`Enum`类来实现枚举功能，枚举类是定义一个class类型，然后，每个常量都是class的一个唯一实例。

```python
from enum import Enum

Month = Enum('Month', ('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'))
for name, member in Month.__members__.items():
    print(name, '=>', member, ',', member.value)
```

如果需要更精确地控制枚举类型，可以从`Enum`派生出自定义类：

```python
from enum import Enum, unique
@unique
class Weekday(Enum):
    Sun = 0 # Sun的value被设定为0
    Mon = 1
    Tue = 2
    Wed = 3
    Thu = 4
    Fri = 5 
    Sat = 6
```

### MySQL

#### 操作mysql

Python中使用第三方库来操作MySQL

```cmd
pip install pymysql
```

获取链接对象？

1. ```from pymysql import Connection ```导包
2. ```Connection(主机,端口,账户,密码)```即可得到链接对象
3. ```链接对象.close()``` 关闭和MySQL数据库的连接

```python
from pymysql import Connection
conn=Connection(
    host="localhost",   # 主机名（IP）
    port=3306,          # 端口
    user="root",        # 账户
    password="root",  # 密码
    autocommit=True     # 设置自动提交
)
# 获取游标对象
course=conn.cursor()
#选择数据库
conn.select_db("dormitorys")
#使用游标对象执行sql
course.execute("select * from student")
#获取查询结果
result=course.fetchall()
for r in result:
    print(r)
# 打印数据库信息
print(conn.get_server_info())
conn.close()
```

#### 插入语句

pymysql在执行数据插入或其它产生数据更改的SQL语句时，默认是需要提交更改的，即，需要通过代码"确认"这种更改行为。通过链接对象.commit() 即可确认此行为。

```python
flag=course.execute("insert into student values(64,'020','张三','男',5,'迁出','2023-10-09')")
if(flag):
    print("插入成功")
else:
    print("检查一下，多少有点问题")
```
