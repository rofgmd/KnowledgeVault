# Python官方教程学习

> 基于Python 3.13学习
> 使用Macos进行练习
> 目的：工作中需要高强度用到Python，必须在上班前非常熟悉Python的基础语法，标准库的使用
> 预计时间：36个工时完成
> 官方文档地址：[Python 教程](https://docs.python.org/zh-cn/3/tutorial/index.html)

## 1. 课前甜点

你可以针对这些任务编写 Unix shell 脚本或 Windows 批处理文件，但 shell 脚本擅长的是移动文件和改变文本数据，而不适合编写 GUI 应用或游戏。 你可以编写 C/C++/Java 程序，但即使只完成一个初始版程序也需要耗费很长的开发时间。 Python 则更为简单易用，同时支持 Windows, macOS 和 Unix 操作系统，并能帮助你更快速地完成工作。

Python 虽然简单易用，但它可是真正的编程语言，提供了大量的数据结构，也支持开发大型程序，远超 shell 脚本或批处理文件；Python 提供的错误检查比 C 还多；作为一种“非常高级的语言”，它内置了灵活的数组与字典等高级数据类型。正因为配备了更通用的数据类型，Python 比 Awk，甚至 Perl 能解决更多问题，而且，很多时候，Python 比这些语言更简单。

**Python 是一种解释型语言，不需要编译和链接，可以节省大量开发时间。它的解释器实现了交互式操作，轻而易举地就能试用各种语言功能，编写临时程序，或在自底向上的程序开发中测试功能。同时，它还是一个超好用的计算器。** 

## 2. 使用 Python 的解释器

```bash
kevinweng@KevindeMacBook-Air ~ % python
zsh: command not found: python
kevinweng@KevindeMacBook-Air ~ % python3
Python 3.13.0 (main, Oct  7 2024, 05:02:14) [Clang 16.0.0 (clang-1600.0.26.4)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
kevinweng@KevindeMacBook-Air ~ % python3.13
Python 3.13.0 (main, Oct  7 2024, 05:02:14) [Clang 16.0.0 (clang-1600.0.26.4)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
```

### 一些技巧

**启动解释器**：python、python -c command [arg]...

> 另一种启动解释器的方式是 python -c command [arg] ...，这将执行 command 中的语句，相当于 shell 的 -c 选项。 由于 Python 语句经常包含空格或其他会被 shell 特殊对待的字符，通常建议用引号将整个 command 括起来。
> 
> Python 模块也可以当作脚本使用。输入：python -m module [arg] ...，会执行 module 的源文件，这跟在命令行把路径写全了一样。
> 
> 在交互模式下运行脚本文件，只要在脚本名称参数前，加上选项 -i 就可以了。

**退出解释器**：Control-D、quit()、exit()

### 解释器运行环境

#### 源文件的字符编码

默认情况下，Python 源码文件的编码是 UTF-8。这种编码支持世界上大多数语言的字符，可以用于字符串字面值、变量、函数名及注释 —— 尽管标准库只用常规的 ASCII 字符作为变量名或函数名，可移植代码都应遵守此约定。要正确显示这些字符，编辑器必须能识别 UTF-8 编码，而且必须使用支持文件中所有字符的字体。

如果不使用默认编码，则要声明文件的编码，文件的 第一行要写成特殊注释。句法如下：

```python
# -*- coding: encoding -*-
# 其中，encoding 可以是 Python 支持的任意一种 codecs。
# 比如，声明使用 Windows-1252 编码，源码文件要写成：
# -*- coding: cp1252 -*-
# 第一行 的规则也有一种例外情况，源码以 UNIX "shebang" 行 开头。此时，编# 码声明要写在文件的第二行。例如：
#!/usr/bin/env python3
# -*- coding: cp1252 -*-
```

### 传入参数

解释器读取命令行参数，把脚本名与其他参数转化为字符串列表存到 sys 模块的 argv 变量里。执行 import sys，可以导入这个模块，并访问该列表。**该列表最少有一个元素；未给定输入参数时，sys.argv[0] 是空字符串**。给定脚本名是 '-' （标准输入）时，sys.argv[0] 是 '-'。使用 -c command 时，sys.argv[0] 是 '-c'。如果使用选项 -m module，sys.argv[0] 就是包含目录的模块全名。解释器不处理 -c command 或 -m module 之后的选项，而是直接留在 sys.argv 中由命令或模块来处理。

## 3. Python 速览

本手册中的许多例子，甚至交互式命令都包含注释。P**ython 注释以 # 开头，直到该物理行结束。注释可以在行开头，或空白符与代码之后，但不能在字符串里面**。字符串中的 # 号就是 # 号。注释用于阐明代码，Python 不解释注释，键入例子时，可以不输入注释。

### 3.1.1 Python用作计算器

`+`, `-`, `*`, `/`

> 除法运算总是返回一个浮点数

除法运算 (/) 总是返回浮点数。 如果要做 floor division 得到一个整数结果你可以使用 // 运算符；要计算余数你可以使用 %:

```python
>>> 8/6
1.3333333333333333
>>> 8//6
1
>>> 8%6
2
```

Python 用 ** 运算符计算乘方

等号（=）用于给变量赋值。赋值后，下一个交互提示符的位置不显示任何结果：

如果变量未定义（即，未赋值），使用该变量会提示错误

Python 全面支持浮点数；混合类型运算数的运算会把整数转换为浮点数：

交互模式下，上次输出的表达式会赋给变量 _。把 Python 当作计算器时，用该变量实现下一步计算更简单，例如：

```python
>>> tax = 12.5/100
>>> price = 100/50
>>> price = 100.50
>>> price * tax
12.5625
>>> price+_
113.0625
>>> round(_, 2)
113.06
```

最好把该变量当作只读类型。不要为它显式赋值，否则会创建一个同名独立局部变量，该变量会用它的魔法行为屏蔽内置变量。

#### round()函数

Python 的 round() 函数用于将数字四舍五入到指定的小数位数。其语法如下：

```python
round(number, ndigits)
```
##### 参数
	1.	number：必需，表示需要四舍五入的数字。
	2.	ndigits：可选，表示保留的小数位数。可以是正数（保留几位小数）或负数（四舍五入到十位、百位等）。如果未指定，默认值为 None，表示四舍五入到最接近的整数。

##### 返回值

返回四舍五入后的数字。如果是整数，返回值是 int 类型；如果是浮点数，返回值是 float 类型。

##### 示例

###### 四舍五入到整数

```python
print(round(3.14159))  # 输出 3
print(round(2.5))      # 输出 2
print(round(3.5))      # 输出 4
```

###### 四舍五入到指定小数位

```python
print(round(3.14159, 2))  # 输出 3.14
print(round(2.71828, 3))  # 输出 2.718
```

###### 负数的 ndigits 参数

```python
print(round(12345, -1))  # 输出 12340
print(round(67890, -2))  # 输出 67900
```

###### 特殊情况

```python
print(round(0.5))        # 输出 0
print(round(-0.5))       # 输出 0
```

##### 注意事项
- Python 的 round() 使用的是“银行家舍入”规则（也称为“偶数舍入”）：在需要舍弃的位数正好是 0.5 时，结果会舍入到最近的偶数。
    - 如 round(2.5) 输出 2，round(3.5) 输出 4。
- 对于金融或更精确的场景，可以考虑使用 decimal 模块，它提供更高的精度控制。

### 3.1.2 文本

除了数字 Python 还可以操作文本（由 str 类型表示，称为“字符串”）。 这包括字符 "!", 单词 "rabbit", 名称 "Paris", 句子 "Got your back." 等等. "Yay! :)"。 它们可以用成对的单引号 ('...') 或双引号 ("...") 来标示，结果完全相同

要标示引号本身，我们需要对它进行“转义”，即在前面加一个 \。 或者，我们也可以使用不同类型的引号:

```python
>>> 'doesn\'t'
"doesn't"
>>> "doesn't"
"doesn't"
```

多行文本，用`\`

```python
>>> print("""\
... Usage: thingy [OPTIONS]
...     -h
...     -H hostname
... """)
Usage: thingy [OPTIONS]
    -h
    -H hostname

>>>
```

#### 字符串拼接

字符串可以用 + 合并（粘到一起），也可以用 * 重复：

```python
>>> 'um'*3+'am'
'umumumam'
>>> 'Py' "thon"
'Python'
# 拼接分隔开的长字符串时，这个功能特别实用：
>>> text = ('Put several strings within parentheses ' 'to have them joined togeth\
er.')
>>> text
'Put several strings within parentheses to have them joined together.'
# 这项功能只能用于两个字面值，不能用于变量或表达式
# 合并多个变量，或合并变量与字面值，要用 +：
>>> text+_
'Put several strings within parentheses to have them joined together.Put several strings within parentheses to have them joined together.'
```

#### 字符串索引

```python
# 字符串支持 索引 （下标访问），第一个字符的索引是 0。单字符没有专用的类型，就是长度为一的字符串：
>>> text = "Python"
>>> text[0]
'P'
>>> text[1]
'y'
# 索引还支持负数，用负数索引时，从右边开始计数：
>>> text[-1]
'n'
>>> text[-2]
'o'
# 注意，-0 和 0 一样，因此，负数索引从 -1 开始。
>>> text[-0]
'P'
```

#### 字符串切片

```python
# 索引用来获取单个字符，而切片允许你获取子字符串:
>>> text[0:4]
'Pyth'
# 切片索引的默认值很有用；省略开始索引时，默认值为 0，省略结束索引时，默认为到字符串的结尾：
>>> text[:2]
'Py'
>>> text[2:]
'thon'
# 切片会自动处理越界索引：
>>> text[2:42]
'thon'
>>> text[42:]
''
# 注意，输出结果包含切片开始，但不包含切片结束。因此，s[:i] + s[i:] 总是等于 s：
>>> text[:2]+text[2:]
'Python'
# 还可以这样理解切片，索引指向的是字符 之间 ，第一个字符的左侧标为 0，最后一个字符的右侧标为 n ，n 是字符串长度。例如：
# +---+---+---+---+---+---+
# | P | y | t | h | o | n |
# +---+---+---+---+---+---+
# 0   1   2   3   4   5   6
# -6  -5  -4  -3  -2  -1
```

**Python 字符串不能修改，是 immutable 的。因此，为字符串中某个索引位置赋值会报错**

**要生成不同的字符串，应新建一个字符串**

#### 字符串获取长度

```python
# 内置函数 len() 返回字符串的长度：
>>> len(text)
6
```

### 3.1.3 列表

Python 支持多种 复合 数据类型，可将不同值组合在一起。最常用的 列表 ，是用方括号标注，逗号分隔的一组值。列表 可以包含不同类型的元素，但一般情况下，各个元素的类型相同：

```python
>>> nums = [1,3,5,6,7,8,8,9]
>>> nums
[1, 3, 5, 6, 7, 8, 8, 9]
>>> nums[-1]
9
>>> nums[-2]
8
>>> nums[1]
3
# 列表合并操作
>>> nums + [10,11,45]
[1, 3, 5, 6, 7, 8, 8, 9, 10, 11, 45]
# 列表是可更改类型
>>> nums[0]=0
>>> nums
[0, 3, 5, 6, 7, 8, 8, 9]
# 你也可以在通过使用 list.append() 方法，在列表末尾添加新条目
>>> nums.append(100)
>>> nums
[0, 3, 5, 6, 7, 8, 8, 9, 100]
```
**Python 中的简单赋值绝不会复制数据。当你将一个列表赋值给一个变量时，该变量将引用现有的列表。你通过一个变量对列表所做的任何更改都会被引用它的所有其他变量看到**

```python
>>> rgb = ["Red", "Green", "Blue"]
>>> rgba = rgb
>>> id(rgb) == id(rgba)
True
>>> rgba.append("Alph")
>>> rgb
['Red', 'Green', 'Blue', 'Alph']
# 切片操作返回包含请求元素的新列表。以下切片操作会返回列表的浅拷贝：
>>> correct_rgba = rgba[:]
>>> correct_rgba[-1]
'Alph'
>>> correct_rgba[-1]='Alpha'
>>> correct_rgba
['Red', 'Green', 'Blue', 'Alpha']
>>> rgba
['Red', 'Green', 'Blue', 'Alph']
# 列表可以通过切片进行清空
>>> letters = ['a', 'b', 'c']
>>> letters[:2] = ''
>>> letters
['c']
# 通过len()可以获取列表长度
>>> len(letters)
1
```

> Python 的赋值语句不复制对象，而是创建目标和对象的绑定关系。对于自身可变，或包含可变项的集合，有时要生成副本用于改变操作，而不必改变原始对象。
> 浅层与深层复制的区别仅与复合对象（即包含列表或类的实例等其他对象的对象）相关：
>   - 浅层复制 构造一个新的复合对象，然后（在尽可能的范围内）将原始对象中找到的对象的 引用 插入其中。
>   - 深层复制 构造一个新的复合对象，然后，递归地将在原始对象里找到的对象的 副本 插入其中。

## 4. 更多控制流工具

### 4.1 if 语句

```python
if x<0:
    ...
elif x == 0:
    ...
else:
    ...
```

### 4.2. for 语句

Python 的 for 语句与 C 或 Pascal 中的不同。Python 的 for 语句不迭代算术递增数值（如 Pascal），或是给予用户定义迭代步骤和结束条件的能力（如 C），而是在列表或字符串等任意序列的元素上迭代，按它们在序列中出现的顺序。

```python
>>> for color in rgb:
...     print(color)
...
Red
Green
Blue
Alph
```

### 4.3 range()函数

内置函数 range() 用于生成等差数列：

```python
>>> for i in range(10):
...     print(i)
...
0
1
2
3
4
5
6
7
8
9
```

#### 用range函数解决Leetcode70爬楼梯

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1 or n == 2:
            return n
        
        dp = [0]*(n+1)# 初始化dp数组
        dp[:3] = [1,1,2]
        for i in range(2, n+1):# 记住，range生成的数不包括n+1
            dp[i] = dp[i-1] + dp[i-2]
        
        return dp[n] 
```

**生成的序列绝不会包括给定的终止值**

range也可以不从0开始

```python
>>> list(range(5,10))
[5, 6, 7, 8, 9]
>>> list(range(0,10,3))
[0, 3, 6, 9]
>>> list(range(-10, -100, -30))
[-10, -40, -70]
```

#### 按索引迭代序列

```python
>>> for i in range(len(rgb)):
...     print(i, rgb[i])
...
0 Red
1 Green
2 Blue
3 Alph
```

不过大多数情况下 enumerate() 函数很方便

**range() 返回的对象在很多方面和列表的行为一样，但其实它和列表不一样。该对象只有在被迭代时才一个一个地返回所期望的列表项，并没有真正生成过一个含有全部项的列表，从而节省了空间**。

这种对象称为可迭代对象 iterable，适合作为需要获取一系列值的函数或程序构件的参数。for 语句就是这样的程序构件；以可迭代对象作为参数的函数例如 sum()：

```python
>>> sum(range(10))
45
```

### 4.4. break 和 continue 语句

和c++用法一致

### 4.5. 循环的 else 子句

在 for 或 while 循环中 break 语句可能对应一个 else 子句。 如果循环在未执行 break 的情况下结束，else 子句将会执行。

在 for 循环中，else 子句会在循环结束其他最后一次迭代之后，即未执行 break 的情况下被执行。

在 while 循环中，它会在循环条件变为假值后执行。

在这两类循环中，当在循环被 break 终结时 else 子句 不会 被执行。 当然，其他提前结束循环的方式，如 return 或是引发异常，也会跳过 else 子句的执行。

### 4.6 pass语句

```python
# pass 还可用作函数或条件语句体的占位符，让你保持在更抽象的层次进行思考。pass 会被默默地忽略：
def initlog(*args):
    pass   # 记得实现这个！
```

### 4.7 match语句

match 语句接受一个表达式并把它的值与一个或多个 case 块给出的一系列模式进行比较。这表面上像 C、Java 或 JavaScript（以及许多其他程序设计语言）中的 switch 语句，但其实它更像 Rust 或 Haskell 中的模式匹配。只有第一个匹配的模式会被执行，并且它还可以提取值的组成部分（序列的元素或对象的属性）赋给变量。

#### Best Practice

```python
# 这段代码刚好可以给自己警醒
def http_error(status):
    match status:
        case 400:
            return("Bad Request")
        case 404:
            return("No Found")
        case _:
            return("Error")

if __name__ == "__main__":
    status = '404'
    print(http_error(status))
```

运行结果，总是Error

```bash
kevinweng@KevindeMacBook-Air ~ % /opt/homebrew/bin/python3 /Users/kevinweng/Documents/Pyth
on_learning/test.py
Error
```

原因：match 语句是用来匹配值的，而你的 status 是一个字符串 '404'，而 case 404 是一个整数。这种类型不一致会导致匹配失败。要修复这个问题，你需要确保 status 的类型与 case 中的值一致。

修改后就正常了：

```python
def http_error(status):
    match status:
        case "400":
            return("Bad Request")
        case "404":
            return("No Found")
        case _:
            return("Error")

if __name__ == "__main__":
    status = '404'
    print(http_error(status))
```

现在就正常了

```bash
kevinweng@KevindeMacBook-Air ~ % /opt/homebrew/bin/python3 /Users/kevinweng/Documents/Pyth
on_learning/test.py
No Found
```

### 4.8 定义函数

**函数内的第一条语句是字符串时，该字符串就是文档字符串，也称为 docstring，详见 文档字符串。利用文档字符串可以自动生成在线文档或打印版文档，还可以让开发者在浏览代码时直接查阅文档；Python 开发者最好养成在代码中加入文档字符串的好习惯。**

函数在执行时使用**函数局部变量符号表**，所有函数变量赋值都存在局部符号表中；引用变量时，首先，**在局部符号表里查找变量**，然后，是**外层函数局部符号表**，**再是全局符号表**，最后是**内置名称符号表**。因此，尽管可以引用全局变量和外层函数的变量，但最好不要在函数内直接赋值（除非是 global 语句定义的全局变量，或 nonlocal 语句定义的外层函数变量）。

在调用函数时会将实际参数（实参）引入到被调用函数的局部符号表中；因此，实参是使用按值调用来传递的（**其中的值始终是对象的引用而不是对象的值**）。当一个函数调用另外一个函数时，会为该调用创建一个新的局部符号表

如果你用过其他语言，你可能会认为 fib 不是函数而是一个过程，因为它没有返回值。 事实上，即使没有 return 语句的函数也有返回值，尽管这个值可能相当无聊。 这个值被称为 None (是一个内置名称)。 通常解释器会屏蔽单独的返回值 None。 如果你确有需要可以使用 print() 查看它:

### 4.9. 函数定义详解

函数定义支持可变数量的参数。这里列出三种可以组合使用的形式。

#### 4.9.1. 默认值参数

```python
def ask_ok(prompt, retries=4, reminder='Please try again!'):
    while True:
        reply = input(prompt)
        if reply in {'y', 'ye', 'yes'}:
            return True
        if reply in {'n', 'no', 'nop', 'nope'}:
            return False
        retries = retries - 1
        if retries < 0:
            raise ValueError('invalid user response')
        print(reminder)
```

**本例还使用了关键字 in ，用于确认序列中是否包含某个值。**

重要警告： 默认值只计算一次。默认值为列表、字典或类实例等可变对象时，会产生与该规则不同的结果。例如，下面的函数会累积后续调用时传递的参数：

```python
>>> def f(a, L=[]):
...     L.append(a)
...     return L
...
>>> print(f(1))
[1]
>>> print(f(2))
[1, 2]
>>> print(f(3))
[1, 2, 3]
```

#### 4.9.2. 关键字参数

kwarg=value 形式的 关键字参数 也可以用于调用函数。

函数调用时，关键字参数必须跟在位置参数后面。所有传递的关键字参数都必须匹配一个函数接受的参数（比如，actor 不是函数 parrot 的有效参数），关键字参数的顺序并不重要。这也包括必选参数，（比如，parrot(voltage=1000) 也有效）。不能对同一个参数多次赋值

最后一个形参为 **name 形式时，接收一个字典（详见 映射类型 --- dict），该字典包含与函数中已定义形参对应之外的所有关键字参数。**name 形参可以与 *name 形参（下一小节介绍）组合使用（*name 必须在 **name 前面）， *name 形参接收一个 元组，该元组包含形参列表之外的位置参数。

```python
def cheeseshop(kind, *arguments, **keywords):
    print("-- Do you have any", kind, "?")
    print("-- I'm sorry, we're all out of", kind)
    for arg in arguments:
        print(arg)
    print("-" * 40)
    for kw in keywords:
        print(kw, ":", keywords[kw])
```

#### 4.9.3. 特殊参数

```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        位置或关键字   |
        |                                - 仅限关键字
         -- 仅限位置
```

/ 和 * 是可选的。这些符号表明形参如何把参数值传递给函数：位置、位置或关键字、关键字。关键字形参也叫作命名形参。

```python
def standard_arg(arg):
    print(arg)

def pos_only_arg(arg, /):
    print(arg)

def kwd_only_arg(*, arg):
    print(arg)

def combined_example(pos_only, /, standard, *, kwd_only):
    print(pos_only, standard, kwd_only)
```

第一个函数定义 standard_arg 是最常见的形式，对调用方式没有任何限制，可以按位置也可以按关键字传递参数：

```python
>>> def standard_arg(arg):
...     print(arg)
...
>>> standard_arg(2)
2
>>> standard_arg(arg=2)
2
```

第二个函数 pos_only_arg 的函数定义中有 /，仅限使用位置形参：

```python
>>> def pos_only_arg(arg, /):
...     print(arg)
...
>>> pos_only_arg(2)
2
>>> pos_only_arg(arg=2)
Traceback (most recent call last):
  File "<python-input-79>", line 1, in <module>
    pos_only_arg(arg=2)
    ~~~~~~~~~~~~^^^^^^^
TypeError: pos_only_arg() got some positional-only arguments passed as keyword arguments: 'arg'
```

第三个函数 kwd_only_arg 如在函数定义中通过 * 所指明的那样只允许关键字参数。

```python
>>> def kwd_only_arg(*, arg):
...     print(arg)
...
>>> kwd_only_arg(2)
Traceback (most recent call last):
  File "<python-input-81>", line 1, in <module>
    kwd_only_arg(2)
    ~~~~~~~~~~~~^^^
TypeError: kwd_only_arg() takes 0 positional arguments but 1 was given
>>> kwd_only_arg(arg=2)
2
```

##### 说明：

- 使用仅限位置形参，可以让用户无法使用形参名。形参名没有实际意义时，强制调用函数的实参顺序时，或同时接收位置形参和关键字时，这种方式很有用。
- **当形参名有实际意义，且显式名称可以让函数定义更易理解时，阻止用户依赖传递实参的位置时，才使用关键字**。
- **对于 API，使用仅限位置形参**，可以防止未来修改形参名时造成破坏性的 API 变动。

#### 4.9.4. 任意实参列表

```python
>>> def concat(*args, sep="/"):
...     return sep.join(args)
...
>>> concat("a", "b", "c")
'a/b/c'
>>> concat("a", "b", "c", sep="-")
'a-b-c'
```

这段代码定义了一个名为 concat 的函数，它的功能是将任意数量的字符串用指定的分隔符连接在一起。以下是详细解析：

函数签名

```python
def concat(*args, sep="/"):
    return sep.join(args)
```

##### 参数解析
1. *args:
    - *args 用于接收任意数量的非关键字参数，参数会被打包成一个元组。
    - 例如，调用 concat("a", "b", "c") 时，args 会是 ("a", "b", "c")。
2. sep="/":
    - 这是一个关键字参数，提供默认值为字符串 "/"，即默认的分隔符是 /。
    - 调用时可以通过 sep="..." 来指定其他分隔符，例如 sep="-"。

##### 返回值

函数返回一个字符串，它是通过 sep 分隔符连接 args 中所有字符串生成的结果。

##### 函数行为解析

函数内部逻辑非常简单：
1. 使用 sep 调用字符串方法 join()。
    - join() 是 Python 的字符串方法，语法为：sep.join(iterable)。
    - 它会将 iterable 中的元素（通常是字符串）按照 sep 连接成一个新的字符串。
2. 将 args 传入 join()，依次将参数连接起来。

##### 示例用法

###### 示例 1: 使用默认分隔符（/）
```python
print(concat("a", "b", "c"))  
# 输出: "a/b/c"
```

- 参数 *args 的值是 ("a", "b", "c")。
- 默认分隔符是 /，所以返回值是 "a/b/c"。

###### 示例 2: 指定分隔符

```python
print(concat("a", "b", "c", sep="-"))
# 输出: "a-b-c"
```

参数 sep="-" 指定了分隔符为 "-"，所以返回值是 "a-b-c"。

###### 示例 3: 单个参数

```python
print(concat("a"))
# 输出: "a"
```

参数 *args 的值是 ("a",)。
因为只有一个字符串，不需要分隔符，直接返回 "a"。

###### 示例 4: 没有参数
```python
print(concat())
# 输出: ""
```

- 参数 *args 是空元组 ()。
- join() 作用于空可迭代对象时，返回空字符串。

##### 优点
1. 灵活性高：
    - 可以处理任意数量的字符串。
    - 支持自定义分隔符。
2. 简洁易读：
    - 使用了 *args 和 join()，代码非常直观。

##### 注意事项
- 类型要求：
    - *args 中的所有元素必须是字符串，否则会引发 TypeError。
- 示例：`concat("a", 1, "b")  # TypeError: sequence item 1: expected str instance, int found`

如果需要支持其他类型，可以将参数先转换为字符串：

```python
def concat(*args, sep="/"):
    return sep.join(map(str, args))
```

##### 总结

concat 是一个简洁而实用的函数，适用于将多个字符串以指定分隔符连接成一个新字符串。

#### 4.9.6 Lambda函数

在 Python 中，lambda 函数是一种简洁的方式来创建**匿名函数**（没有名字的函数）。它通常用于需要定义简单函数的场景，尤其是在函数作为参数传递时。

##### 语法：

```python
lambda 参数1, 参数2, ...: 表达式
```
- 参数1, 参数2, ... 是函数的输入参数，可以有多个。
- 表达式是返回值，必须是单一的表达式，而不是代码块。

##### 示例：

1. 简单示例：
```python
# 定义一个lambda函数，将输入加2
add_two = lambda x: x + 2

# 使用
print(add_two(5))  # 输出 7
```

2. 多参数示例：
```python
# 定义一个lambda函数，计算两个数的乘积
multiply = lambda x, y: x * y

print(multiply(3, 4))  # 输出 12
```

3. 与内置函数结合使用：

```python
# 在排序中使用lambda函数
points = [(1, 2), (3, 1), (5, 0)]
# 按第二个元素排序
sorted_points = sorted(points, key=lambda point: point[1])

print(sorted_points)  # 输出 [(5, 0), (3, 1), (1, 2)]
```

4. 作为函数参数：

```python
# 使用lambda函数定义条件过滤
nums = [1, 2, 3, 4, 5]
even_nums = list(filter(lambda x: x % 2 == 0, nums))

print(even_nums)  # 输出 [2, 4]
```

##### 注意事项：
- lambda 函数适用于简单的功能逻辑。如果逻辑较为复杂，建议使用 def 定义普通函数。
- 由于 lambda 函数是匿名的，调试时可能不如普通函数方便。
	
##### 例子

```python
>>> pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
>>> pairs.sort(key=lambda pair: pair[1])
>>> pairs
[(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
```

#### 4.9.7 文档字符串

以下是文档字符串内容和格式的约定。

**第一行应为对象用途的简短摘要**。为保持简洁，不要在这里显式说明对象名或类型，因为可通过其他方式获取这些信息（除非该名称碰巧是描述函数操作的动词）。这一行应以**大写字母开头，以句点结尾**。

文**档字符串为多行时，第二行应为空白行，在视觉上将摘要与其余描述分开**。后面的行可包含若干段落，描述对象的调用约定、副作用等。

**Python 解析器不会删除 Python 中多行字符串字面值的缩进**，因此，文档处理工具应在必要时删除缩进。这项操作遵循以下约定：文档字符串**第一行之后的第一个非空行决定了整个文档字符串的缩进量**（第一行通常与字符串开头的引号相邻，其缩进在字符串中并不明显，因此，不能用第一行的缩进），然后，删除字符串中所有行开头处与此缩进“等价”的空白符。不能有比此缩进更少的行，但如果出现了缩进更少的行，应删除这些行的所有前导空白符。转化制表符后（通常为 8 个空格），应测试空白符的等效性。

#### 4.9.8. 函数注解

函数注解是可选的用户自定义函数类型的元数据完整信息。标注以字典的形式存放在函数的`__annotations__`属性中而对函数的其他部分没有影响。

### 4.10 编码风格

Python 项目大多都遵循 PEP 8 的风格指南；它推行的编码风格易于阅读、赏心悦目。Python 开发者均应抽时间悉心研读；以下是该提案中的核心要点：

- 缩进，用 4 个空格，不要用制表符。
    4 个空格是小缩进（更深嵌套）和大缩进（更易阅读）之间的折中方案。制表符会引起混乱，最好别用。
- 换行，一行不超过 79 个字符。
    这样换行的小屏阅读体验更好，还便于在大屏显示器上并排阅读多个代码文件。
- 用空行分隔函数和类，及函数内较大的代码块。
- 最好把注释放到单独一行。
- 使用文档字符串。
- 运算符前后、逗号后要用空格，但不要直接在括号内使用
- 类和函数的命名要一致；按惯例，命名类用 UpperCamelCase，命名函数与方法用 lowercase_with_underscores。命名方法中第一个参数总是用 self (类和方法详见 初探类)。
- 编写用于国际多语环境的代码时，不要用生僻的编码。Python 默认的 UTF-8 或纯 ASCII 可以胜任各种情况。
- 同理，就算多语阅读、维护代码的可能再小，也不要在标识符中使用非 ASCII 字符。

## 5. 数据结构

### 5.1. 列表详解

```python
list.append(x) # 列表末尾添加一项
list.extend(iterable) # 添加来自iterable的所有项扩展列表
list.insert(i, x) # 在制定位置插入元素 
list.remove(x)
list.pop()
list.pop([i])
list.clear()
list.index(x[, start[, end]])
list.count(x)
list.sort(*, key=None, reverse=False)
list.reverse()
list.copy() # 返回列表的浅拷贝
```

#### 列表Best Practice：Leetcode118 杨辉三角

这题唯一要注意的是：**问题的根本原因是 Python 的列表是可变对象，直接赋值或追加只是创建了引用。使用 copy() 创建独立的对象可以避免引用共享问题。**

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        dp = []
        tmp = []
        for i in range(numRows):
            for j in range(i+1):
                if j == 0 or j == i:
                    tmp.append(1)
                else:
                    tmp.append(dp[i-1][j-1]+dp[i-1][j])
                
            dp.append(tmp.copy())# 直接赋值或追加只是创建了引用
            tmp.clear()
        
        return dp
```

#### Best Practice：Leetcode 283 移动零

```python
# 练习一下remove和count的用法
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        count_zero = nums.count(0)
        for i in range(count_zero):
            nums.remove(0)
            nums.append(0)
```

#### 5.1.1. 用列表实现堆栈

列表方法使得将列表用作栈非常容易，最后添加的元素会最先被取出（“后进先出”）。 **要将一个条目添加到栈顶，可使用 append()**。 **要从栈顶取出一个条目，则使用 pop() 且不必显式指定索引**。

#### Best Practice：Leetcode 20

```python
class Solution:
    def isValid(self, s: str) -> bool:
        Parentheses_list = []
        for parenthes in s:
            match parenthes:
                case '(' | '[' | '{':
                    Parentheses_list.append(parenthes)
                case ')':
                    if len(Parentheses_list)==0 or Parentheses_list.pop()!='(':
                        return False
                case ']':
                    if len(Parentheses_list)==0 or Parentheses_list.pop()!='[':
                        return False                    
                case '}':
                    if len(Parentheses_list)==0 or Parentheses_list.pop()!='{':
                        return False 
                case _:
                    return False

        return len(Parentheses_list) == 0     
```

官方解有非常值得学习的地方，代码设计其中一个原则：对扩展开放，对修改关闭。

```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2 == 1:
            return False
        
        pairs = {
            ")": "(",
            "]": "[",
            "}": "{",
        }
        stack = list()
        for ch in s:
            if ch in pairs:
                if not stack or stack[-1] != pairs[ch]:
                    return False
                stack.pop()
            else:
                stack.append(ch)
        
        return not stack

# 作者：力扣官方题解
# 链接：https://leetcode.cn/problems/valid-parentheses/solutions/373578/you-xiao-de-gua-hao-by-leetcode-solution/
# 来源：力扣（LeetCode）
# 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

#### 5.1.2. 用列表实现队列

列表也可以用作队列，最先加入的元素，最先取出（“先进先出”）；然而，列表作为队列的效率很低。因为，在列表末尾添加和删除元素非常快，但在列表开头插入或移除元素却很慢（因为所有其他元素都必须移动一位）。

实现队列最好用 collections.deque，可以快速从两端添加或删除元素。

#### 5.1.3. 列表推导式

列表推导式创建列表的方式更简洁。常见的用法为，对序列或可迭代对象中的每个元素应用某种操作，用生成的结果创建新的列表；或用满足特定条件的元素创建子序列。

```python
>>> squares = list(map(lambda x:x**2, range(10)))
>>> squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> squares = [x**2 for x in range(11)]
>>> squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
这段代码的含义是：

**使用 map 函数和 lambda 表达式生成从 0 到 9 的平方值，并将结果转换为一个列表。**

逐步解析这段代码：

##### 代码：

```python
squares = list(map(lambda x: x**2, range(10)))
```

##### 含义：
1. range(10):
- 生成一个从 0 到 9 的整数序列（不包括 10）。具体内容为：[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]。
2. lambda x: x**2:
- 创建了一个匿名函数（即 lambda 表达式），其作用是：对于输入的每一个值 x，返回它的平方（x * x 或 x**2）。
3. map(lambda x: x**2, range(10)):
- map 是 Python 的一个内置函数，它会将提供的函数（这里是 lambda x: x**2）依次应用到 range(10) 生成的每个元素上。
- 结果是一个惰性序列，表示每个输入数字的平方，计算的结果类似于：[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]。
4. list(map(...)):
- 将 map 生成的惰性序列强制转换为一个列表类型（list），以便进一步操作或打印。

##### 最终结果：

变量 squares 保存了从 0 到 9 的平方值组成的列表：

```python
squares = [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

##### 总结

这段代码的作用是生成一个从 0 到 9 的平方值的列表，是 Python 中函数式编程的一种常见用法，灵活简洁。

#### 5.1.4. 嵌套的列表推导式

```python
>>> matrix = [[1,2,3,4], [5,6,7,8], [9,10,11,12],]
>>> list(zip(*matrix))
[(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]
```

#### 列表扩展：extend()

在 Python 中，可以通过多种方法将一个列表附加到另一个列表后面。以下是几种常见的方法：

##### 方法 1：使用 extend() 方法

```python
A = [1, 2, 3]
B = [4, 5, 6]

A.extend(B)  # 将 B 中的元素添加到 A 的末尾
print(A)  # 输出: [1, 2, 3, 4, 5, 6]
```

##### 方法 2：使用 + 操作符创建新列表

```python
A = [1, 2, 3]
B = [4, 5, 6]

C = A + B  # 创建一个新的列表，不改变原来的 A 和 B
print(C)  # 输出: [1, 2, 3, 4, 5, 6]
```

方法 3：使用列表切片赋值

```python
A = [1, 2, 3]
B = [4, 5, 6]

A[len(A):] = B  # 将 B 添加到 A 的末尾
print(A)  # 输出: [1, 2, 3, 4, 5, 6]
```

#### Best Practise: Leetcode 121买卖股票的最佳时机

练习二维数组的初始化

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # dp[i][0] = max(dp[i-1][0], -prices[i])
        # dp[i][1] = max(dp[i-1][1], prices[i]-dp[i][0])
        dp = [[0, 0] for _ in range(len(prices))]
        dp[0] = [-prices[0], 0]
        for i in range(1,len(prices)):
            dp[i][0] = max(dp[i-1][0], -prices[i])
            dp[i][1] = max(dp[i-1][1], prices[i]+dp[i][0])
        
        return dp[-1][1]
```

### 5.2 del语句

可以按索引而不是按值从一个列表移除条目：即使用 del 语句。 这不同于返回一个值的 pop() 方法。 del 语句还可被用来从列表移除切片或清空整个列表（之前我们通过将一个空列表赋值给切片实现此功能）。

```python
>>> a = [-1,1,1,2,3,4,5,6,7,8,4,5,9]
>>> del a[0]
>>> a
[1, 1, 2, 3, 4, 5, 6, 7, 8, 4, 5, 9]
>>> del a[:2]
>>> a
[2, 3, 4, 5, 6, 7, 8, 4, 5, 9]
>>> del a
>>> a
Traceback (most recent call last):
  File "<python-input-14>", line 1, in <module>
    a
NameError: name 'a' is not defined
```

### 5.3 元组和序列

列表和字符串有很多共性，例如，索引和切片操作。这两种数据类型是**序列**（参见 序列类型 --- list, tuple, range）。随着 Python 语言的发展，其他的序列类型也被加入其中。本节介绍另一种标准序列类型：**元组**。

元组由多个用逗号隔开的值组成，例如：

```python
>>> t = 12345, 54321, 'hello!'
>>> t[0]
12345
>>> t
(12345, 54321, 'hello!')
>>> t[0]=888 # 元组是不可变对象，对元组进行赋值会报错
Traceback (most recent call last):
  File "<python-input-18>", line 1, in <module>
    t[0]=888
    ~^^^
TypeError: 'tuple' object does not support item assignment
```

输出时，元组都要由圆括号标注，这样才能正确地解释嵌套元组。输入时，圆括号可有可无，不过经常是必须的（如果元组是更大的表达式的一部分）。不允许为元组中的单个元素赋值，**当然，可以创建含列表等可变对象的元组**。

虽然，元组与列表很像，但使用场景不同，用途也不同。元组是 immutable （不可变的），一般可包含异质元素序列，通过**解包**（见本节下文）或**索引访问**（如果是 namedtuples，可以属性访问）。列表是 mutable （可变的），列表元素一般为同质类型，**可迭代访问**。

#### 元组计算长度

```python
>>> t= 123,
>>> len(t)
1
```

#### 元组解包

```python
>>> x, y, z = t
>>> x
12345
>>> y
54321
>>> z
'hello!'
```

称之为 序列解包 也是妥妥的，适用于右侧的任何序列。**序列解包时，左侧变量与右侧序列元素的数量应相等**。注意，多重赋值其实只是元组打包和序列解包的组合。

### 5.4 集合

Python 还支持 集合 这种数据类型。集合是由不重复元素组成的无序容器。基本用法包括成员检测、消除重复元素。集合对象支持合集、交集、差集、对称差分等数学运算。

创建集合用花括号或 set() 函数。注意，创建空集合只能用 set()，不能用 {}，{} 创建的是空字典，下一小节介绍数据结构：字典。

> 和c++的`unordered_set`差不多，两者都是基于哈希表实现的无序集合

```python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> basket # 删除重复元素
{'banana', 'apple', 'orange', 'pear'}
>>> 'apple' in basket # 查看元素是否在集合中
True
>>> 'orange' in basket
True
>>> 'crabgrass' in basket
False
```

#### 集合运算

```python
>>> a = set('abracadabra')# 字符串本质上是字符数组
>>> b = set('alacazam')
>>> a
{'a', 'r', 'd', 'b', 'c'}
>>> b
{'a', 'l', 'z', 'c', 'm'}
>>> a-b # 差集
{'r', 'b', 'd'}
>>> a | b # 并集
{'a', 'r', 'l', 'd', 'z', 'b', 'c', 'm'}
>>> a & b # 交集
{'a', 'c'}
>>> a ^ b # 对称差：只出现在一个集合中的字符
{'r', 'b', 'l', 'd', 'z', 'm'}
```

### 5.5 字典

另一个常用的 Python 内置数据类型是 字典 (参见 映射类型 --- dict)。 字典在其他编程语言中可能称为“联合内存”或“联合数组”。 与以连续整数为索引的序列不同，字典是以**键**来索引的，键可以是任何不可变类型；**字符串和数字总是可以作为键**。 **元组在其仅包含字符串、数字或元组时也可以作为键**；**如果一个元组直接或间接地包含了任何可变对象，则不可以用作键**。 你不能使用列表作为键，因为列表可使用索引赋值、切片赋值或 append() 和 extend() 等方法进行原地修改。

可以把字典理解为 键值对 的集合，但字典的键必须是唯一的。花括号 {} 用于创建空字典。另一种初始化字典的方式是，在花括号里输入逗号分隔的键值对，这也是字典的输出方式。

字典的主要用途是通过关键字存储、提取值。用 del 可以删除键值对。用已存在的关键字存储值，与该关键字关联的旧值会被取代。通过不存在的键提取值，则会报错。

对字典执行 list(d) 操作，返回该字典中所有键的列表，按插入次序排列（如需排序，请使用 sorted(d)）。检查字典里是否存在某个键，使用关键字 in。

`dict()`构造函数可以直接用键值对序列创建字典：

```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'guido': 4127, 'jack': 4098}
>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```

#### Best Practice：Leetcode 1 两数之和

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        map = {}
        for i in range(len(nums)):
            if (target-nums[i]) not in map:
                map[nums[i]]=i
            else:
                return [map[target-nums[i]], i]
        
        return None
```

### 5.6. 循环的技巧

#### items()

当对字典执行循环时，可以使用`items()`方法同时提取键及其对应的值。

```python
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave
```

#### enumerate()

在序列中循环时，用`enumerate()`函数可以同时取出位置索引和对应的值：

```python
>>> for i, value in enumerate(['tic', 'tac', 'toe']):
...     print(i, value)
...
0 tic
1 tac
2 toe
```

##### Best Practice: Leetcode 1 两数之和

```python
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        map = {}
        for i, value in enumerate(nums):# 实践
            if target-value not in map:
                map[value]=i 
            else:
                return [map[target-value],i]
        
        return None
```

#### zip()

同时循环

```python
>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> for q, a in zip(questions, answers):
...     print(q,": ",a)
...
name : lancelot
quest : the holy grail
favorite color : blue
```

#### reversed()

为了逆向对序列进行循环，可以求出欲循环的正向序列，然后调用 reversed() 函数：

```python
>>> for i in reversed(range(10)):
...     print(i)
...
9
8
7
6
5
4
3
2
1
0
```

#### sorted()

按指定顺序循环序列，可以用 sorted() 函数，在不改动原序列的基础上，返回一个重新的序列：

```python
>>> basket
{'banana', 'apple', 'orange', 'pear'}
>>> basket = list(basket)
>>> basket
['banana', 'apple', 'orange', 'pear']
>>> for i in sorted(basket):
...     print(i)
...
apple
banana
orange
pear
```

#### set()

使用 set() 去除序列中的重复元素。使用 sorted() 加 set() 则按排序后的顺序，循环遍历序列中的唯一元素

### 5.7 深入条件控制

while 和 if 条件句不只可以进行比较，还可以使用任意运算符。

**比较运算符 in 和 not in 用于执行确定一个值是否存在（或不存在）于某个容器中的成员检测**。 **运算符 is 和 is not 用于比较两个对象是否是同一个对象**。**所有比较运算符的优先级都一样，且低于任何数值运算符**。

比较操作支持链式操作。例如`a < b == c`校验`a`是否小于`b`，且`b`是否等于`c`。

比较操作可以用布尔运算符`and`和`or`组合，并且，比较操作（或其他布尔运算）的结果都可以用`not`取反。这些操作符的优先级低于比较操作符；`not`的优先级最高，`or`的优先级最低，因此，`A and not B or C`等价于`(A and (not B)) or C`。与其他运算符操作一样，此处也可以用圆括号表示想要的组合。

布尔运算符`and`和`or`是所谓的`短路`运算符：**其参数从左至右求值，一旦可以确定结果，求值就会停止**。例如，如果`A`和`C`为真，`B`为假，那么`A and B and C`不会对`C`求值。用作普通值而不是布尔值时，短路运算符的返回值通常是最后一个求了值的参数。

注意，Python 与 C 不同，在表达式内部赋值必须显式使用海象运算符`:=`。 这避免了 C 程序中常见的问题：要在表达式中写`==`时，却写成了`=`。

### 5.8 序列和其他类型的比较

**序列对象可以与相同序列类型的其他对象比较**。这种比较使用**字典式顺序**：首先，比较前两个对应元素，如果不相等，则可确定比较结果；如果相等，则比较之后的两个元素，以此类推，直到其中一个序列结束。如果要比较的两个元素本身是相同类型的序列，则递归地执行字典式顺序比较。如果两个序列中所有的对应元素都相等，则两个序列相等。如果一个序列是另一个的初始子序列，则较短的序列可被视为较小（较少）的序列。 对于字符串来说，字典式顺序使用**Unicode码位序号**排序单个字符。下面列出了一些比较相同类型序列的例子：

```python
>>> (1,2,3)<(1,2,4)
True
>>> [1,2,3]<[1,2,4]
True
>>> (1,2,3,4)<(1,2,4)
True
>>> (1,2)<(1,2,4)
True
>>> [1,2,3]=[1,2,3]# 经典错误，= 是赋值不是比较
  File "<python-input-59>", line 1
    [1,2,3]=[1,2,3]
     ^
SyntaxError: cannot assign to literal
>>> [1,2,3]==[1,2,3]
True
>>> (1, 2, ('aa', 'ab'))   < (1, 2, ('abc', 'a'), 4)
True
```

注意，当比较不同类型的对象时，只要待比较的对象提供了合适的比较方法，就可以使用 < 和 > 进行比较。例如，混合的数字类型通过数字值进行比较，所以，0 等于 0.0，等等。如果没有提供合适的比较方法，解释器不会随便给出一个比较结果，而是引发 TypeError 异常。

### collections.deque使用方法

`collections.deque`是 Python 的标准库 `collections` 模块中的双端队列（double-ended queue），专为快速从队列的两端添加或删除元素而设计。它比使用列表（list）在队列场景下更高效，因为 list 在两端插入或删除时复杂度是 `O(n)`，而 deque 是 `O(1)`。

#### 主要功能

1. 创建 deque
```python
from collections import deque

# 创建空的 deque
dq = deque()

# 从一个可迭代对象创建 deque
dq = deque([1, 2, 3])
print(dq)  # deque([1, 2, 3])
```
2. 添加元素
- append(x): 在右侧添加元素。
- appendleft(x): 在左侧添加元素。
```python
dq = deque([1, 2, 3])
dq.append(4)         # 右侧添加
dq.appendleft(0)     # 左侧添加
print(dq)  # deque([0, 1, 2, 3, 4])
```
3. 删除元素
- pop(): 从右侧移除并返回元素。
- popleft(): 从左侧移除并返回元素。
```python
dq = deque([1, 2, 3, 4])
dq.pop()            # 删除右侧
dq.popleft()        # 删除左侧
print(dq)  # deque([2, 3])
```
4. 限制 deque 长度

可以通过参数 `maxlen` 限制队列的最大长度，超出时会自动移除最旧的元素。
```python
dq = deque(maxlen=3)
dq.append(1)
dq.append(2)
dq.append(3)
dq.append(4)  # 队列满时，左侧元素被移除
print(dq)  # deque([2, 3, 4], maxlen=3)
```
5. 旋转 deque
- rotate(n): 将 deque 的元素旋转 n 步。正数表示右移，负数表示左移。
```python
dq = deque([1, 2, 3, 4])
dq.rotate(1)  # 右移 1 步
print(dq)  # deque([4, 1, 2, 3])
dq.rotate(-2) # 左移 2 步
print(dq)  # deque([2, 3, 4, 1])
```
6. 其他操作
- extend(iterable): 将一个可迭代对象的元素添加到 deque 的右侧。
- extendleft(iterable): 将一个可迭代对象的元素添加到 deque 的左侧（顺序会反转）。
```python
dq = deque([1, 2, 3])
dq.extend([4, 5])
print(dq)  # deque([1, 2, 3, 4, 5])

dq.extendleft([0, -1])
print(dq)  # deque([-1, 0, 1, 2, 3, 4, 5])
```
#### 常见应用场景
1. 队列操作（FIFO）
```python
dq = deque()
dq.append(1)
dq.append(2)
print(dq.popleft())  # 输出 1
print(dq.popleft())  # 输出 2
```
2.	栈操作（LIFO）
```python
dq = deque()
dq.append(1)
dq.append(2)
print(dq.pop())  # 输出 2
print(dq.pop())  # 输出 1
```
3.	滑动窗口
```python
nums = [1, 2, 3, 4, 5]
k = 3
dq = deque(maxlen=k)

for num in nums:
    dq.append(num)
    print(list(dq))  # 输出当前窗口内容
```

collections.deque 非常适合需要高效的队列或双端操作的场景。你可以尝试根据自己的应用需求实现不同的功能！

#### Best Practice: Leetcode 102. 二叉树的层序遍历

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        dq = deque()
        dq.append(root)
        ans = []
        while(len(dq) != 0):
            tmp = []
            size = len(dq)
            for i in range(size):
                if dq[0].left is not None:
                    dq.append(dq[0].left)
                if dq[0].right is not None:
                    dq.append(dq[0].right)
                tmp.append(dq.popleft().val)
            
            ans.append(tmp)
        
        return ans    
```

### bisect使用方法

`bisect` 是 Python 标准库中的一个模块，提供了用于有序列表的二分查找算法工具。它可以高效地找到元素插入的位置或进行相关操作，非常适合处理排序数组。

#### 核心函数

`bisect` 模块包含以下几个主要函数：

1. **`bisect.bisect_left(a, x, lo=0, hi=len(a))`**
   - 在 `a` 中找到插入点 `i`，使得所有 `a[:i]` 的元素都小于 `x`。
   - 如果 `x` 已经存在，插入点会在 `x` 左侧。
2. **`bisect.bisect_right(a, x, lo=0, hi=len(a))` 或 `bisect.bisect(a, x, lo=0, hi=len(a))`**
   - 在 `a` 中找到插入点 `i`，使得所有 `a[:i]` 的元素都小于或等于 `x`。
   - 如果 `x` 已经存在，插入点会在 `x` 右侧。
3. **`bisect.insort_left(a, x, lo=0, hi=len(a))`**
   - 在 `a` 中找到合适的位置并插入 `x`，保持 `a` 的有序性。插入点在左侧。
4. **`bisect.insort_right(a, x, lo=0, hi=len(a))` 或 `bisect.insort(a, x, lo=0, hi=len(a))`**
   - 在 `a` 中找到合适的位置并插入 `x`，保持 `a` 的有序性。插入点在右侧。

------

#### 示例用法

##### 1. 查找插入点

```python
import bisect

a = [1, 3, 4, 7, 9]
x = 5

# 使用 bisect_left
position_left = bisect.bisect_left(a, x)
print(f"bisect_left: {position_left}")  # 输出 3

# 使用 bisect_right
position_right = bisect.bisect_right(a, x)
print(f"bisect_right: {position_right}")  # 输出 3
```

##### 2. 插入元素

```python
import bisect

a = [1, 3, 4, 7, 9]
x = 5

# 使用 insort_left 插入
bisect.insort_left(a, x)
print(f"insort_left: {a}")  # 输出 [1, 3, 4, 5, 7, 9]

# 使用 insort_right 插入
bisect.insort_right(a, x)
print(f"insort_right: {a}")  # 输出 [1, 3, 4, 5, 5, 7, 9]
```

##### 3. 查找区间

结合 `bisect_left` 和 `bisect_right`，可以快速找到某个值在数组中的范围：

```python
import bisect

a = [1, 2, 2, 3, 4, 4, 5]
x = 4

# 找到值为 4 的范围
left = bisect.bisect_left(a, x)
right = bisect.bisect_right(a, x)
print(f"Range of {x}: {left} to {right}")  # 输出 Range of 4: 4 to 6
```

------

#### 注意事项

1. 列表 `a` 必须是**有序**的，否则结果不可靠。
2. 插入操作的时间复杂度是 $O(n)$，因为插入需要移动元素。
3. 查找操作的时间复杂度是 $O(\log n)$。

------

#### 应用场景

1. 在动态更新的排序数组中高效地插入数据。
2. 查找特定范围的数据（如区间查询）。
3. 解决竞赛中需要对有序数组快速插入和查找的问题。

#### Best Practice：Leetocde 35. 搜索插入位置

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        return bisect.bisect_left(nums,target)
```

## 6. 模块

退出Python解释器后，再次进入时，之前在Python解释器中定义的函数和变量就丢失了。因此，编写较长程序时，最好用文本编辑器代替解释器，执行文件中的输入内容，这就是编写**脚本**。随着程序越来越长，为了方便维护，最好把脚本拆分成多个文件。编写脚本还一个好处，不同程序调用同一个函数时，不用把函数定义复制到各个程序。

为实现这些需求，Python把各种定义存入一个文件，在脚本或解释器的交互式实例中使用。这个文件就是 模块 ；模块中的定义可以 导入 到其他模块或 主 模块（在顶层和计算器模式下，执行脚本中可访问的变量集）。

模块是包含 Python 定义和语句的文件。其文件名是模块名加后缀名`.py`。在模块内部，通过全局变量`__name__`可以获取模块名（即字符串）。例如，用文本编辑器在当前目录下创建`fibo.py`文件，输入以下内容：

```python
def generate(numRows):
    dp = []
    tmp = []
    for i in range(numRows):
        for j in range(i+1):
            if j == 0 or j == i:
                tmp.append(1)
            else:
                tmp.append(dp[i-1][j-1]+dp[i-1][j])
            
        dp.append(tmp.copy())
        tmp.clear()
    
    return dp
```

现在，进入 Python 解释器，用以下命令导入该模块：

```python
>>> import test
```

此操作不会直接把 fibo 中定义的函数名称添加到当前 namespace 中（请参阅 Python作用域和命名空间了解详情）；它只是将模块名称fibo添加到那里。 使用该模块名称你可以访问其中的函数:

```python
>>> test.generate(4)
[[1], [1, 1], [1, 2, 1], [1, 3, 3, 1]]
```

### 6.1. 模块详解

模块包含可执行语句及函数定义。这些语句用于初始化模块，且仅在`import`语句第一次 遇到模块名时执行.

每个模块都有自己的私有命名空间，它会被用作模块中定义的所有函数的全局命名空间。 因此，模块作者可以在模块内使用全局变量而不必担心与用户的全局变量发生意外冲突。 另一方面，如果你知道要怎么做就可以通过与引用模块函数一样的标记法 modname.itemname 来访问一个模块的全局变量。

模块可以导入其他模块。 根据惯例可以将所有 import 语句都放在模块（或者也可以说是脚本）的开头但这并非强制要求。 如果被放置于一个模块的最高层级，则被导入的模块名称会被添加到该模块的全局命名空间。

用as作为别名导入

```python
>>> from test import http_error as error
>>> test.error('401')
Traceback (most recent call last):
  File "<python-input-7>", line 1, in <module>
    test.error('401')
    ^^^^^^^^^^
AttributeError: module 'test' has no attribute 'error'
>>> error('401')
'Error'
>>> error('400')
'Bad Request'
```

#### 6.1.1. 以脚本方式执行模块

```python
if __name__ == "__main__":
    # status = '404'
    # print(http_error(status))
    # cheeseshop("Limburger", "It's very runny, sir.",
    #        "It's really very, VERY runny, sir.",
    #        shopkeeper="Michael Palin",
    #        client="John Cleese",
    #        sketch="Cheese Shop Sketch")
    numRows = 5
    print(generate(numRows))
```

这常用于为模块提供一个便捷的用户接口，或用于测试（把模块作为执行测试套件的脚本运行）

#### 6.1.2. 模块搜索路径

当导入一个名为 spam 的模块时，解释器首先会搜索具有该名称的内置模块。 这些模块的名称在`sys.builtin_module_names`中列出。如果未找到，它将在变量`sys.path`所给出的目录列表中搜索名为`spam.py`的文件。`sys.path`是从这些位置初始化的:

- 被命令行直接运行的脚本所在的目录（或未指定文件时的当前目录）。
- PYTHONPATH （目录列表，与 shell 变量 PATH 的语法一样）。
- 依赖于安装的默认值（按照惯例包括一个 site-packages 目录，由 site 模块处理）。

#### 6.1.3. “已编译的” Python 文件

为了快速加载模块，Python 把模块的编译版本缓存在`__pycache__`目录中，文件名为`module.version.pyc`，`version`对编译文件格式进行编码，一般是 Python的版本号。例如，CPython的`3.3`发行版中，`spam.py`的编译版本缓存为`__pycache__/spam.cpython-33.pyc`。这种命名惯例让不同Python版本编译的模块可以共存。

**Python对比编译版与源码的修改日期，查看编译版是否已过期，是否要重新编译**。**此进程完全是自动的**。此外，**编译模块与平台无关**，因此，可在不同架构的系统之间共享相同的库。

Python在两种情况下不检查缓存。一，**从命令行直接载入的模块**，**每次都会重新编译，且不储存编译结果**；二，**没有源模块，就不会检查缓存**。为了让一个库能以隐藏源代码的形式分发（通过将所有源代码变为编译后的版本），编译后的模块必须放在源目录而非缓存目录中，并且源目录绝不能包含同名的未编译的源模块。

给专业人士的一些小建议：

- 在 Python 命令中使用 -O 或 -OO 开关，可以减小编译模块的大小。`-O`去除断言语句，`-OO`去除断言语句和`__doc__`字符串。有些程序可能依赖于这些内容，因此，没有十足的把握，不要使用这两个选项。“优化过的”模块带有`opt-`标签，并且文件通常会一小些。将来的发行版或许会改进优化的效果。
- **从`.pyc`文件读取的程序不比从`.py`读取的执行速度快，`.pyc`文件只是加载速度更快。**
- compileall 模块可以为一个目录下的所有模块创建 .pyc 文件。
- 本过程的细节及决策流程图，详见 PEP 3147。

### 6.2 标准模块

Python自带一个标准模块的库，它在Python库参考（此处以下称为"库参考"）里另外描述。一些模块是内嵌到解释器里面的，它们给一些虽并非语言核心但却内嵌的操作提供接口，要么是为了效率，要么是给操作系统基础操作例如系统调入提供接口。这些模块集是一个配置选项，并且还依赖于底层的操作系统。例如，`winreg`模块只在 Windows系统上提供。一个特别值得注意的模块`sys`，它被内嵌到每一个Python 解释器中。`sys.ps1`和`sys.ps2`变量定义了一些字符，**它们可以用作主提示符和辅助提示符**:

```python
>>> sys.ps1
'>>> '
>>> sys.ps2
'... '
```

**只有解释器用于交互模式时，才定义这两个变量。**

变量`sys.path`是字符串列表，用于确定解释器的模块搜索路径。该变量以环境变量 PYTHONPATH 提取的默认路径进行初始化，如未设置 PYTHONPATH，则使用内置的默认路径。可以用标准列表操作修改该变量：

```python
>>> import sys
>>> print(sys.path)
['', '/opt/homebrew/Cellar/python@3.13/3.13.0_1/Frameworks/Python.framework/Versions/3.13/lib/python313.zip', '/opt/homebrew/Cellar/python@3.13/3.13.0_1/Frameworks/Python.framework/Versions/3.13/lib/python3.13', '/opt/homebrew/Cellar/python@3.13/3.13.0_1/Frameworks/Python.framework/Versions/3.13/lib/python3.13/lib-dynload', '/opt/homebrew/lib/python3.13/site-packages']
```

### 6.3. dir() 函数

内置函数 dir() 用于查找模块定义的名称。返回结果是经过排序的字符串列表：

```python
>>> dir(sys)
['__breakpointhook__', '__displayhook__', '__doc__', '__excepthook__', '__interactivehook__', '__loader__', '__name__', '__package__', '__spec__', '__stderr__', '__stdin__', '__stdout__', '__unraisablehook__', '_base_executable', '_baserepl', '_clear_internal_caches', '_clear_type_cache', '_current_exceptions', '_current_frames', '_debugmallocstats', '_framework', '_get_cpu_count_config', '_getframe', '_getframemodulename', '_git', '_home', '_is_gil_enabled', '_is_interned', '_setprofileallthreads', '_settraceallthreads', '_stdlib_dir', '_xoptions', 'abiflags', 'activate_stack_trampoline', 'addaudithook', 'api_version', 'argv', 'audit', 'base_exec_prefix', 'base_prefix', 'breakpointhook', 'builtin_module_names', 'byteorder', 'call_tracing', 'copyright', 'deactivate_stack_trampoline', 'displayhook', 'dont_write_bytecode', 'exc_info', 'excepthook', 'exception', 'exec_prefix', 'executable', 'exit', 'flags', 'float_info', 'float_repr_style', 'get_asyncgen_hooks', 'get_coroutine_origin_tracking_depth', 'get_int_max_str_digits', 'getallocatedblocks', 'getdefaultencoding', 'getdlopenflags', 'getfilesystemencodeerrors', 'getfilesystemencoding', 'getprofile', 'getrecursionlimit', 'getrefcount', 'getsizeof', 'getswitchinterval', 'gettrace', 'getunicodeinternedsize', 'hash_info', 'hexversion', 'implementation', 'int_info', 'intern', 'is_finalizing', 'is_stack_trampoline_active', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'monitoring', 'orig_argv', 'path', 'path_hooks', 'path_importer_cache', 'platform', 'platlibdir', 'prefix', 'ps1', 'ps2', 'pycache_prefix', 'set_asyncgen_hooks', 'set_coroutine_origin_tracking_depth', 'set_int_max_str_digits', 'setdlopenflags', 'setprofile', 'setrecursionlimit', 'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdlib_module_names', 'stdout', 'thread_info', 'unraisablehook', 'version', 'version_info', 'warnoptions']
# 没有参数时，dir() 列出当前已定义的名称：
>>> dir()
['__annotations__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'sys']
>>> __name__
'__main__'
>>> __package__
'_pyrepl
# 注意它列出所有类型的名称：变量，模块，函数，……。
# dir() 不会列出内置函数和变量的名称。这些内容的定义在标准模块 builtins 中：
>>> help
>>> Welcome to Python 3.13's help utility! If this is your first time using
Python, you should definitely check out the tutorial at
https://docs.python.org/3.13/tutorial/.

Enter the name of any module, keyword, or topic to get help on writing
Python programs and using Python modules.  To get a list of available
modules, keywords, symbols, or topics, enter "modules", "keywords",
"symbols", or "topics".

Each module also comes with a one-line summary of what it does; to list
the modules whose name or summary contain a given string such as "spam",
enter "modules spam".

To quit this help utility and return to the interpreter,
enter "q", "quit" or "exit".
```

### 6.4. 包

包是通过使用“带点号模块名”来构造Python模块命名空间的一种方式。 例如，模块名A.B表示名为`A`的包中名为`B`的子模块。就像使用模块可以让不同模块的作者不必担心彼此的全局变量名一样，使用带点号模块名也可以让`NumPy`或`Pillow`等多模块包的作者也不必担心彼此的模块名冲突。

假设要为统一处理声音文件与声音数据设计一个模块集（“包”）。声音文件的格式很多（通常以扩展名来识别，例如：.wav，.aiff，.au），因此，为了不同文件格式之间的转换，需要创建和维护一个不断增长的模块集合。为了实现对声音数据的不同处理（例如，混声、添加回声、均衡器功能、创造人工立体声效果），还要编写无穷无尽的模块流。下面这个分级文件树展示了这个包的架构：

```markdown
sound/                          最高层级的包
      __init__.py               初始化 sound 包
      formats/                  用于文件格式转换的子包
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  用于音效的子包
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  用于过滤器的子包
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

注意，使用`from package import item`时，`item`可以是包的子模块（或子包），也可以是包中定义的函数、类或变量等其他名称。`import`语句首先测试包中是否定义了`item`；如果未在包中定义，则假定`item`是模块，并尝试加载。如果找不到`item`，则触发`ImportError`异常。

相反，使用`import item.subitem.subsubitem`句法时，除最后一项外，每个`item`都必须是包；最后一项可以是模块或包，但不能是上一项中定义的类、函数或变量。

#### 6.4.1. 从包中导入 *

使用 from sound.effects import * 时会发生什么？你可能希望它会查找并导入包的所有子模块，但事实并非如此。因为这将花费很长的时间，并且可能会产生你不想要的副作用，如果这种副作用被你设计为只有在导入某个特定的子模块时才应该发生。

唯一的解决办法是提供包的显式索引。import 语句使用如下惯例：如果包的`__init__.py`代码定义了列表`__all__`，运行`from package import *`时，它就是被导入的模块名列表。发布包的新版本时，包的作者应更新此列表。如果包的作者认为没有必要在包中执行导入 * 操作，也可以不提供此列表。例如，`sound/effects/__init__.py`文件可以包含以下代码：

```python
__all__ = ["echo", "surround", "reverse"]
```

这意味着`from sound.effects import *`将导入`sound.effects`包的三个命名子模块。

请注意子模块可能会受到本地定义名称的影响。 例如，如果你在`sound/effects/__init__.py`文件中添加了一个`reverse`函数，`from sound.effects import *`将只导入`echo`和`surround`这两个子模块，但不会导入`reverse`子模块，因为它被本地定义的`reverse`函数所遮挡

如果没有定义`__all__`，`from sound.effects import *`语句不会把包 `sound.effects`中的所有子模块都导入到当前命名空间；它只是确保包 sound.effects 已被导入（可能还会运行 __init__.py 中的任何初始化代码），然后再导入包中定义的任何名称。 这包括由 __init__.py 定义的任何名称（以及显式加载的子模块）。 它还包括先前`import`语句显式加载的包里的任何子模块。 请看以下代码:

```python
import sound.effects.echo
import sound.effects.surround
from sound.effects import *
```

在本例中，`echo`和`surround`模块被导入到当前命名空间，因为在执行 `from...import`语句时它们已在`sound.effects`包中定义了。 （当定义了 `__all__`时也是如此）。

虽然，可以把模块设计为用`import *`时只导出遵循指定模式的名称，**但仍不提倡在生产代码中使用这种做法**。

记住，使用`from package import specific_submodule`没有任何问题！ 实际上，除了导入模块使用不同包的同名子模块之外，这种方式是推荐用法。

#### 6.4.2. 相对导入

```python
from . import echo
from .. import formats
from ..filters import equalizer
```

注意，相对导入基于当前模块名。因为主模块名永远是`"__main__"`，所以**如果计划将一个模块用作Python应用程序的主模块，那么该模块内的导入语句必须始终使用绝对导入**。

#### 6.4.3. 多目录中的包

包还支持一个特殊的属性，`__path__`。 在执行该文件中的代码之前，它被初始化为字符串的`sequence`，其中包含包的`__init__.py`的目录名称。这个变量可以修改；修改后会影响今后对模块和包中包含的子包的搜索。

这个功能虽然不常用，但可用于扩展包中的模块集。

## 7. 输入与输出

程序输出有几种显示方式；数据既可以输出供人阅读的形式，也可以写入文件备用。本章探讨一些可用的方式。

### 7.1. 更复杂的输出格式

到目前为止我们已遇到过两种写入值的方式: 表达式语句和`print()`函数。（第三种方式是使用文件对象的`write()`方法；标准输出文件可以被引用为`sys.stdout`。 更多相关信息请参阅标准库参考）

对输出格式的控制不只是打印空格分隔的值，还需要更多方式。格式化输出包括以下几种方法。

#### 使用格式化字符串字面值

要在字符串开头的引号/三引号前添加`f`或`F`。在这种字符串中，可以在`{`和`}`字符之间输入引用的变量，或字面值的Python表达式。

```python
>>> year = 2016
>>> event = 'bilibili_word'
>>> f'Today is {year} {event}'
'Today is 2016 bilibili_word'
```

#### str.format()

字符串的`str.format()`方法需要更多手动操作。你仍将使用`{`和`}`来标记变量将被替换的位置并且可以提供详细的格式化指令，但你还需要提供待格式化的信息。下面的代码块中有两个格式化变量的例子：

```python
>>> yes_votes = 42_572_654
>>> total_votes = 85_705_149
>>> percentage = yes_votes / total_votes
>>> '{:-9} YES votes  {:2.2%}'.format(yes_votes, percentage)
' 42572654 YES votes  49.67%'
```

##### 格式说明符解释：

1. {:-9}:
    - `-` 表示对齐方向，表示左对齐（默认是右对齐）。
    - 9 表示字段宽度，确保输出的内容至少占 9 个字符的宽度。
    - 所以，这部分将 yes_votes 按照 9 个字符的宽度左对齐，并且在需要时用空格填充。
2. {:2.2%}:
    - 2.2 是一个格式指定符，表示数字应该总共占 2 个字符，并且小数点后保留 2 位。由于在显示百分比时，Python 会自动乘以 100，并附加一个 % 符号。
    - : 表示格式化的开始，2.2% 意味着：
        - 2 表示总宽度（包括数字和百分号），
        - 2 表示小数点后的位数，
        - % 表示百分比格式。

如果不需要花哨的输出，只想快速显示变量进行调试，可以用`repr()`或`str()`函数把值转化为字符串。

`str()`函数返回供人阅读的值，`repr()`则生成适于解释器读取的值（如果没有等效的语法，则强制执行`SyntaxError）`。对于没有支持供人阅读展示结果的对象，`str()`返回与`repr()`相同的值。一般情况下，数字、列表或字典等结构的值，使用这两个函数输出的表现形式是一样的。字符串有两种不同的表现形式。

```python
' 42572654 YES votes  49.67%'
>>> str = "hello, world\n"
>>> str
'hello, world\n'
>>> print(str)
hello, world

```

#### 7.1.1. 格式化字符串字面值

格式化字符串字面值（简称为f-字符串）在字符串前加前缀`f`或`F`，通过`{expression}`表达式，把Python表达式的值添加到字符串内。

格式说明符是可选的，写在表达式后面，可以更好地控制格式化值的方式。下例将`pi`舍入到小数点后三位：

```python
>>> import math
>>> print(f"PI is {math.pi:.3f}")
PI is 3.142
```

在`':'`后传递整数，为该字段设置最小字符宽度，常用于列对齐：

```python
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
>>> for name, phone in table.items():
...     print(f'{name:10} ==> {phone:10d}')
...
Sjoerd     ==>       4127
Jack       ==>       4098
Dcab       ==>       7678

# 还有一些修饰符可以在格式化前转换值。
# '!a' 应用 ascii()
# '!s' 应用 str()
# '!r' 应用 repr()
>>> animals = 'eels'
>>> print(f'My hovercraft is full of {animals}.')
My hovercraft is full of eels.
>>> print(f'My hovercraft is full of {animals!r}.')
My hovercraft is full of 'eels'.
>>> print(f'My hovercraft is full of {animals!a}.')
My hovercraft is full of 'eels'.
>>> print(f'My hovercraft is full of {animals!s}.')
My hovercraft is full of eels.

# = 说明符可被用于将一个表达式扩展为表达式文本、等号再加表达式求值结果的形式。
>>> bugs = 'roaches'
>>> count = 13
>>> area = 'living room'
>>> print(f'Debugging {bugs=} {count=} {area=}')
Debugging bugs='roaches' count=13 area='living room'
```

#### 7.1.2. 字符串 format() 方法

```python
# 基本用法
>>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
We are the knights who say "Ni!"
# 花括号及之内的字符（称为格式字段）被替换为传递给 str.format() 方法的对象。花括号中的数字表示传递给 str.format() 方法的对象所在的位置。
>>> print('We are the {1} who say "{1}!"'.format('knights', 'Ni'))
We are the Ni who say "Ni!"
# str.format() 方法中使用关键字参数名引用值。
>>> print('This {food} is {adjective}.'.format(
...       food='spam', adjective='absolutely horrible'))
This spam is absolutely horrible.
# 位置参数和关键字参数可以任意组合：
>>> print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
...                                                    other='Georg'))
The story of Bill, Manfred, and Georg.
# 如果不想分拆较长的格式字符串，最好按名称引用变量进行格式化，不要按位置。这项操作可以通过传递字典，并用方括号 '[]' 访问键来完成。
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
...       'Dcab: {0[Dcab]:d}'.format(table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
# 这也可以通过将 table 字典作为采用 ** 标记的关键字参数传入来实现。
> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
# 另一种方法是 str.zfill() ，该方法在数字字符串左边填充零，且能识别正负号：
>>> num=12
>>> str(num).zfill(5)
'00012'
>>> num=-12
>>> str(num).zfill(5)
'-0012'
```

#### 7.1.4 旧式字符串格式化风格

```python
>>> import math
>>> print('The value of pi is approximately %5.3f.' % math.pi)
The value of pi is approximately 3.142.
```

### 7.2. 读写文件

```python
# open() 返回一个 file object
# 最常使用的是两个位置参数和一个关键字参数：open(filename, mode, encoding=None)
>>> f = open("text.txt", 'w', encoding="utf-8")
# 第一个实参是文件名字符串。
# 第二个实参是包含描述文件使用方式字符的字符串。
# mode 的值包括 'r' ，表示文件只能读取；
# 'w' 表示只能写入（现有同名文件会被覆盖）；
# 'a' 表示打开文件并追加内容，任何写入的数据会自动添加到文件末尾。
# 'r+' 表示打开文件进行读写。mode 实参是可选的，省略时的默认值为 'r'。
# 通常情况下，文件是以 text mode 打开的，
# 也就是说，你从文件中读写字符串，这些字符串是以特定的 encoding 编码的。
# 如果没有指定 encoding ，默认的是与平台有关的（见 open() ）。
# 因为 UTF-8 是现代事实上的标准，除非你知道你需要使用一个不同的编码，否则建议使用 encoding="utf-8" 。
# 在模式后面加上一个 'b' ，可以用 binary mode 打开文件。
# 二进制模式的数据是以 bytes 对象的形式读写的。在二进制模式下打开文件时，你不能指定 encoding 。
# 在文本模式下读取文件时，默认把平台特定的行结束符（Unix 上为 \n, Windows 上为 \r\n）转换为 \n。
# 在文本模式下写入数据时，默认把 \n 转换回平台特定结束符。
# 这种操作方式在后台修改文件数据对文本文件来说没有问题，
# 但会破坏 JPEG 或 EXE 等二进制文件中的数据。
# 注意，在读写此类文件时，一定要使用二进制模式。
# --------------------------------------------------------------
# 在处理文件对象时，最好使用 with 关键字。
# 优点是，子句体结束后，文件会正确关闭，即便触发异常也可以。
# 而且，使用 with 相比等效的 try-finally 代码块要简短得多：
>>> f = open("text.txt", 'w', encoding="utf-8")
>>> with open('text.txt') as f:
...     read_data = f.read()
...
>>> f.closed # 我们可以检测文件是否已被自动关闭。
True
# 如果没有使用 with 关键字，则应调用 f.close() 关闭文件，即可释放文件占用的系统资源。
```

**警告 调用`f.write()`时，未使用`with`关键字，或未调用`f.close()`，即使程序正常退出，也可能导致`f.write()`的参数没有完全写入磁盘。**

```python
# 通过 with 语句，或调用 f.close() 关闭文件对象后，再次使用该文件对象将会失败。
>>> f.read()
Traceback (most recent call last):
  File "<python-input-3>", line 1, in <module>
    f.read()
    ~~~~~~^^
ValueError: I/O operation on closed file.
```

#### 7.2.1. 文件对象的方法

本节下文中的例子假定已创建 `f` 文件对象。

`f.read(size)` 可用于读取文件内容，它会读取一些数据，并返回字符串（文本模式），或字节串对象（在二进制模式下）。 *size* 是可选的数值参数。省略 *size* 或 *size* 为负数时，读取并返回整个文件的内容；文件大小是内存的两倍时，会出现问题。*size* 取其他值时，读取并返回最多 *size* 个字符（文本模式）或 *size* 个字节（二进制模式）。如已到达文件末尾，`f.read()` 返回空字符串（`''`）。

```python
>>> with open('test.txt', encoding="utf-8") as f:
...     f.read()
...
'Hello World!\nTest File\nhello world!\ntest file\n'
```

`f.readline()` 从文件中读取单行数据；字符串末尾保留换行符（`\n`），只有在文件不以换行符结尾时，文件的最后一行才会省略换行符。这种方式让返回值清晰明确；只要 `f.readline()` 返回空字符串，就表示已经到达了文件末尾，空行使用 `'\n'` 表示，该字符串只包含一个换行符。

```python
>>> with open('test.txt', encoding="utf-8") as f:
...     f.readline()
...
'Hello World!\n'
```

如需以列表形式读取文件中的所有行，可以用 `list(f)` 或 `f.readlines()`。

```python
>>> with open('test.txt', encoding="utf-8") as f:
...     list(f)
...
['Hello World!\n', 'Test File\n', 'hello world!\n', 'test file\n']
>>> with open('test.txt', encoding="utf-8") as f:
...     f.readlines()
...
['Hello World!\n', 'Test File\n', 'hello world!\n', 'test file\n']
```

向文件写内容（我用w模式写，会覆盖掉原有内容）

```python
>>> f.write("This is a test\n")
15
>>> with open('test.txt', encoding="utf-8") as f:
...     f.read()
...
'This is a test\n'
```

`f.tell()` 返回整数，给出文件对象在文件中的当前位置，表示为二进制模式下时从文件开始的字节数，以及文本模式下的意义不明的数字。

`f.seek(offset, whence)` 可以改变文件对象的位置。通过向参考点添加 *offset* 计算位置；参考点由 *whence* 参数指定。 *whence* 值为 0 时，表示从文件开头计算，1 表示使用当前文件位置，2 表示使用文件末尾作为参考点。省略 *whence* 时，其默认值为 0，即使用文件开头作为参考点。

```python
>>> f = open("test.txt", "rb+")
>>> f.write(b'0123456789abcdef')
16
>>> f.seek(5)
5
>>> f.read(1)
b'5'
>>> f.seek(-3, 2)
13
>>> f.read(1)
b'd'
```

在文本文件（模式字符串未使用 `b` 时打开的文件）中，只允许相对于文件开头搜索（使用 `seek(0, 2)` 搜索到文件末尾是个例外），唯一有效的 *offset* 值是能从 `f.tell()` 中返回的，或 0。其他 *offset* 值都会产生未定义的行为。

文件对象还有一些额外的方法，如使用频率较低的 [`isatty()`](https://docs.python.org/zh-cn/3/library/io.html#io.IOBase.isatty) 和 [`truncate()`](https://docs.python.org/zh-cn/3/library/io.html#io.IOBase.truncate) 等；有关文件对象的完整指南请查阅标准库参考。

#### 7.2.2. 使用 [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json) 保存结构化数据

字符串可以很容易地写入文件或从文件中读取。 数字则更麻烦一些，因为 [`read()`](https://docs.python.org/zh-cn/3/library/io.html#io.TextIOBase.read) 方法只返回字符串，而字符串必须传给 [`int()`](https://docs.python.org/zh-cn/3/library/functions.html#int) 这样的函数，它接受 `'123'` 这样的字符串并返回其数值 123。 当你想要保存嵌套列表和字典等更复杂的数据类型时，手动执行解析和序列化操作将会变得非常复杂。

Python 允许你使用流行的数据交换格式 [JSON (JavaScript Object Notation)](https://json.org/)，而不是让用户持续编写和调试代码来将复杂的数据类型存入文件中。 标准库模块 [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json) 可以接受带有层级结构的 Python 数据，并将其转换为字符串表示形式；这个过程称为 *serializing*。 根据字符串表示形式重建数据则称为 *deserializing*。 在序列化和反序列化之间，用于代表对象的字符串可以存储在文件或数据库中，或者通过网络连接发送到远端主机。

```python
>>> import json
>>> x = [1, 'simple', 'list']
>>> json.dumps(x)
'[1, "simple", "list"]'
```

## 8. 错误和异常

至此，本教程还未深入介绍错误信息，但如果您尝试过本教程前文中的例子，应该已经看到过一些错误信息。**错误可（至少）被分为两种：*语法错误* 和 *异常*。**

### 8.1. 语法错误

语法错误又称解析错误，是学习 Python 时最常见的错误.

解析器会重复存在错误的行并显示一个指向廖行中检测到错误的词元的小箭头。 错误可能是由于所指向的词元 *之前* 缺少某个词元而导致的。 

### 8.2. 异常

即使语句或表达式使用了正确的语法，执行时仍可能触发错误。执行时检测到的错误称为 *异常*，异常不一定导致严重的后果：很快我们就能学会如何处理 Python 的异常。大多数异常不会被程序处理，而是显示下列错误信息：

```python
>>> 10*(2/0)# 除零错误
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
```

错误信息的最后一行说明程序遇到了什么类型的错误。异常有不同的类型，而类型名称会作为错误信息的一部分中打印出来：上述示例中的异常类型依次是：[`ZeroDivisionError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ZeroDivisionError)， [`NameError`](https://docs.python.org/zh-cn/3/library/exceptions.html#NameError) 和 [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError)。作为异常类型打印的字符串是发生的内置异常的名称。对于所有内置异常都是如此，但对于用户定义的异常则不一定如此（虽然这种规范很有用）。标准的异常类型是内置的标识符（不是保留关键字）。

此行其余部分根据异常类型，结合出错原因，说明错误细节。

错误信息开头用堆栈回溯形式展示发生异常的语境。一般会列出源代码行的堆栈回溯；但不会显示从标准输入读取的行。

[内置异常](https://docs.python.org/zh-cn/3/library/exceptions.html#bltin-exceptions) 列出了内置异常及其含义。

### 8.3. 异常的处理

可以编写程序处理选定的异常。下例会要求用户一直输入内容，直到输入有效的整数，但允许用户中断程序（使用 Control-C 或操作系统支持的其他操作）；注意，用户中断程序会触发 [`KeyboardInterrupt`](https://docs.python.org/zh-cn/3/library/exceptions.html#KeyboardInterrupt) 异常。

```python
>>> while True:
...     try:
...             x = int(input("Please enter a number: "))
...             break
...     except ValueError:
...             print("Oops!  That was no valid number.  Try again...")
...
Please enter a number: skjkj
Oops!  That was no valid number.  Try again...
Please enter a number: sskjh
Oops!  That was no valid number.  Try again...
Please enter a number: sjhh
Oops!  That was no valid number.  Try again...
Please enter a number: se
Oops!  That was no valid number.  Try again...
Please enter a number: 3445
```

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句的工作原理如下：

- 首先，执行 *try 子句* （[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 和 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 关键字之间的（多行）语句）。
- 如果没有触发异常，则跳过 *except 子句*，[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句执行完毕。
- 如果在执行 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 子句时发生了异常，则跳过该子句中剩下的部分。 如果异常的类型与 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 关键字后指定的异常相匹配，则会执行 *except 子句*，然后跳到 try/except 代码块之后继续执行。
- 如果发生的异常与 *except 子句* 中指定的异常不匹配，则它会被传递到外层的 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句中；如果没有找到处理器，则它是一个 *未处理异常* 且执行将停止并输出一条错误消息。

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句可以有多个 *except 子句* 来为不同的异常指定处理程序。 但最多只有一个处理程序会被执行。 处理程序只处理对应的 *try 子句* 中发生的异常，而不处理同一 `try` 语句内其他处理程序中的异常。 *except 子句* 可以用带圆括号的元组来指定多个异常，例如:

```python
... except (RuntimeError, TypeError, NameError):
...     pass
```

未处理异常的 [`__str__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__str__) 输出会被打印为该异常消息的最后部分 ('detail')。

[`BaseException`](https://docs.python.org/zh-cn/3/library/exceptions.html#BaseException) 是所有异常的共同基类。它的一个子类， [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) ，是所有非致命异常的基类。不是 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 的子类的异常通常不被处理，因为它们被用来指示程序应该终止。它们包括由 [`sys.exit()`](https://docs.python.org/zh-cn/3/library/sys.html#sys.exit) 引发的 [`SystemExit`](https://docs.python.org/zh-cn/3/library/exceptions.html#SystemExit) ，以及当用户希望中断程序时引发的 [`KeyboardInterrupt`](https://docs.python.org/zh-cn/3/library/exceptions.html#KeyboardInterrupt) 。

[`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 可以被用作通配符，捕获（几乎）一切。然而，好的做法是，尽可能具体地说明我们打算处理的异常类型，并允许任何意外的异常传播下去。

处理 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 最常见的模式是打印或记录异常，然后重新提出（允许调用者也处理异常）:

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) ... [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 语句具有可选的 *else 子句*，该子句如果存在，它必须放在所有 *except 子句* 之后。 它适用于 *try 子句* 没有引发异常但又必须要执行的代码。 例如:

```python
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

**使用 `else` 子句比向 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 子句添加额外的代码要好，可以避免意外捕获非 `try` ... `except` 语句保护的代码触发的异常。**

异常处理程序不仅会处理在 *try 子句* 中立刻发生的异常，还会处理在 *try 子句* 中调用（包括间接调用）的函数。 例如:

```python
def this_fails():
    x = 1/0

try:
    this_fails()
except ZeroDivisionError as err:
    print('Handling run-time error:', err)

Handling run-time error: division by zero
```

### 8.4. 触发异常

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句支持强制触发指定的异常。例如：

```python
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 唯一的参数就是要触发的异常。这个参数必须是**异常实例或异常类**（派生自 [`BaseException`](https://docs.python.org/zh-cn/3/library/exceptions.html#BaseException) 类，例如 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 或其子类）。如果传递的是异常类，将通过调用没有参数的构造函数来隐式实例化：

```python
>>> raise ValueError
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError
```

### 8.5. 异常链

如果一个未处理的异常发生在 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 部分内，它将会有被处理的异常附加到它上面，并包括在错误信息中

为了表明一个异常是另一个异常的直接后果， [`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句允许一个可选的 [`from`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 子句:

```python
# exc 必须为异常实例或为 None。
raise RuntimeError from exc
```

### 8.6. 用户自定义异常

程序可以通过创建新的异常类命名自己的异常（Python 类的内容详见 [类](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-classes)）。不论是以直接还是间接的方式，异常都应从 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 类派生。

异常类可以被定义成能做其他类所能做的任何事，但通常应当保持简单，它往往只提供一些属性，允许相应的异常处理程序提取有关错误的信息。

大多数异常命名都以 “Error” 结尾，类似标准异常的命名。

许多标准模块定义了自己的异常，以报告他们定义的函数中可能出现的错误。

### 8.7. 定义清理操作

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句还有一个可选子句，用于定义在所有情况下都必须要执行的清理操作。例如：

```python
>>> try:
...     raise KeyboardInterrupt
... finally:
...     print('Goodbye, world!')
...
Goodbye, world!
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
KeyboardInterrupt
```

如果存在 [`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句，则 `finally` 子句是 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句结束前执行的最后一项任务。不论 `try` 语句是否触发异常，都会执行 `finally` 子句。以下内容介绍了几种比较复杂的触发异常情景：

- 如果执行 `try` 子句期间触发了某个异常，则某个 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 子句应处理该异常。如果该异常没有 `except` 子句处理，在 `finally` 子句执行后会被重新触发。
- `except` 或 `else` 子句执行期间也会触发异常。 同样，该异常会在 `finally` 子句执行之后被重新触发。
- 如果 `finally` 子句中包含 [`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break)、[`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue) 或 [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return) 等语句，异常将不会被重新引发。
- 如果执行 `try` 语句时遇到 [`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break),、[`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue) 或 [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return) 语句，则 `finally` 子句在执行 `break`、`continue` 或 `return` 语句之前执行。
- **如果 `finally` 子句中包含 `return` 语句，则返回值来自 `finally` 子句的某个 `return` 语句的返回值，而不是来自 `try` 子句的 `return` 语句的返回值。**

**在实际应用程序中，[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句对于释放外部资源（例如文件或者网络连接）非常有用，无论是否成功使用资源。**

### 8.8. 预定义的清理操作

某些对象定义了不需要该对象时要执行的标准清理操作。无论使用该对象的操作是否成功，都会执行清理操作。比如，下例要打开一个文件，并输出文件内容：

```python
for line in open("myfile.txt"):
    print(line, end="")
```

这个代码的问题在于，执行完代码后，文件在一段不确定的时间内处于打开状态。在简单脚本中这没有问题，但对于较大的应用程序来说可能会出问题。[`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with) 语句支持以及时、正确的清理的方式使用文件对象：

```python
with open("myfile.txt") as f:
    for line in f:
        print(line, end="")
```

语句执行完毕后，即使在处理行时遇到问题，都会关闭文件 *f*。和文件一样，支持预定义清理操作的对象会在文档中指出这一点。

### 8.9. 引发和处理多个不相关的异常

在有些情况下，有必要报告几个已经发生的异常。这通常是在并发框架中当几个任务并行失败时的情况，但也有其他的用例，有时需要是继续执行并收集多个错误而不是引发第一个异常。

内置的 [`ExceptionGroup`](https://docs.python.org/zh-cn/3/library/exceptions.html#ExceptionGroup) 打包了一个异常实例的列表，这样它们就可以一起被引发。它本身就是一个异常，所以它可以像其他异常一样被捕获。

通过使用 `except*` 代替 `except` ，我们可以有选择地只处理组中符合某种类型的异常。在下面的例子中，显示了一个嵌套的异常组，每个 `except*` 子句都从组中提取了某种类型的异常，而让所有其他的异常传播到其他子句，并最终被重新引发。

### 8.10. 用注释细化异常情况

当一个异常被创建以引发时，它通常被初始化为描述所发生错误的信息。在有些情况下，在异常被捕获后添加信息是很有用的。为了这个目的，异常有一个 `add_note(note)` 方法接受一个字符串，并将其添加到异常的注释列表。标准的回溯在异常之后按照它们被添加的顺序呈现包括所有的注释。

```python
try:
    raise TypeError('bad type')
except Exception as e:
    e.add_note('Add some information')
    e.add_note('Add some more information')
    raise

Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
    raise TypeError('bad type')
TypeError: bad type
Add some information
Add some more information
```

## 9. 类

类提供了把数据和功能绑定在一起的方法。创建新类时创建了新的对象 *类型*，从而能够创建该类型的新 *实例*。实例具有能维持自身状态的属性，还具有能修改自身状态的方法（由其所属的类来定义）。

和其他编程语言相比，Python 的类只使用了很少的新语法和语义。Python 的类有点类似于 C++ 和 Modula-3 中类的结合体，而且支持面向对象编程（OOP）的所有标准特性：**类的继承机制支持多个基类、派生的类能覆盖基类的方法、类的方法能调用基类中的同名方法。对象可包含任意数量和类型的数据。和模块一样，类也支持 Python 动态特性：在运行时创建，创建后还可以修改。**

如果用 C++ 术语来描述的话，**类成员（包括数据成员）通常为 *public*** （例外的情况见下文 [私有变量](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-private)），**所有成员函数都为 *virtual*** 。与 Modula-3 中一样，没有用于从对象的方法中引用本对象成员的简写形式：方法函数在声明时，有一个显式的第一个参数代表本对象，该参数由方法调用隐式提供。与在 Smalltalk 中一样，**Python 的类也是对象，这为导入和重命名提供了语义支持**。与 C++ 和 Modula-3 不同，**Python 的内置类型可以用作基类，供用户扩展**。此外，与 C++ 一样，**具有特殊语法的内置运算符（算术运算符、下标等）都可以为类实例重新定义**。

### 9.1. 名称和对象

对象之间相互独立，多个名称（甚至是多个作用域内的多个名称）可以绑定到同一对象。这在其他语言中通常被称为别名。Python 初学者通常不容易理解这个概念，处理数字、字符串、元组等不可变基本类型时，可以不必理会。但是，对于涉及可变对象（如列表、字典，以及大多数其他类型）的 Python 代码的语义，别名可能会产生意料之外的效果。这样做，通常是为了让程序受益，**因为别名在某些方面就像指针**。例如，传递对象的代价很小，因为实现只传递一个指针；如果函数修改了作为参数传递的对象，调用者就可以看到更改——无需像 Pascal 那样用两个不同的机制来传参。

### 9.2. Python 作用域和命名空间

在介绍类前，首先要介绍 Python 的作用域规则。类定义对命名空间有一些巧妙的技巧，了解作用域和命名空间的工作机制有利于加强对类的理解。并且，即便对于高级 Python 程序员，这方面的知识也很有用

*namespace* （命名空间）是从名称到对象的映射。现在，大多数命名空间都使用 Python 字典实现，但除非涉及到性能优化，我们一般不会关注这方面的事情，而且将来也可能会改变这种方式。命名空间的例子有：内置名称集合（包括 [`abs()`](https://docs.python.org/zh-cn/3/library/functions.html#abs) 函数以及内置异常的名称等）；一个模块的全局名称；一个函数调用中的局部名称。对象的属性集合也是命名空间的一种形式。关于命名空间的一个重要知识点是，**不同命名空间中的名称之间绝对没有关系**；例如，两个不同的模块都可以定义 `maximize` 函数，且不会造成混淆。用户使用函数时必须要在函数名前面加上模块名。

点号之后的名称是 **属性**。例如，表达式 `z.real` 中，`real` 是对象 `z` 的属性。严格来说，对模块中名称的引用是属性引用：表达式 `modname.funcname` 中，`modname` 是模块对象，`funcname` 是模块的属性。**模块属性和模块中定义的全局名称之间存在直接的映射：它们共享相同的命名空间！**

属性可以是只读的或者可写的。 在后一种情况下，可以对属性进行赋值。 模块属性是可写的：你可以写入 `modname.the_answer = 42` 。 也可以使用 [`del`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#del) 语句删除可写属性。 例如，`del modname.the_answer` 将从名为 `modname` 对象中移除属性 `the_answer`。

命名空间是在不同时刻创建的，且拥有不同的生命周期。内置名称的命名空间是在 Python 解释器启动时创建的，永远不会被删除。模块的全局命名空间在读取模块定义时创建；通常，模块的命名空间也会持续到解释器退出。从脚本文件读取或交互式读取的，由解释器顶层调用执行的语句是 [`__main__`](https://docs.python.org/zh-cn/3/library/__main__.html#module-__main__) 模块调用的一部分，也拥有自己的全局命名空间。内置名称实际上也在模块里，即 [`builtins`](https://docs.python.org/zh-cn/3/library/builtins.html#module-builtins) 。

函数的局部命名空间在函数被调用时被创建，并在函数返回或抛出未在函数内被处理的异常时，被删除。（实际上，用“遗忘”来描述实际发生的情况会更好一些。）当然，每次递归调用都有自己的局部命名空间。

一个命名空间的 *作用域* 是 Python 代码中的一段文本区域，从这个区域可直接访问该命名空间。“可直接访问”的意思是，该文本区域内的名称在被非限定引用时，查找名称的范围，是包括该命名空间在内的。

作用域虽然是被静态确定的，但会被动态使用。执行期间的任何时刻，都会有 3 或 4 个“命名空间可直接访问”的嵌套作用域：

- 最内层作用域，包含局部名称，并首先在其中进行搜索
- 那些外层闭包函数的作用域，包含“非局部、非全局”的名称，从最靠内层的那个作用域开始，逐层向外搜索。
- 倒数第二层作用域，包含当前模块的全局名称
- 最外层（最后搜索）的作用域，是内置名称的命名空间

**如果一个名称被声明为全局，则所有引用和赋值都将直接指向“倒数第二层作用域”**，即包含模块的全局名称的作用域。 要重新绑定在最内层作用域以外找到的变量，可以使用 [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal) 语句；如果未使用 nonlocal 声明，这些变量将为只读（尝试写入这样的变量将在最内层作用域中创建一个 *新的* 局部变量，而使得同名的外部变量保持不变）。

通常，当前局部作用域将（按字面文本）引用当前函数的局部名称。在函数之外，局部作用域引用与全局作用域一致的命名空间：模块的命名空间。 类定义在局部命名空间内再放置另一个命名空间。

划重点，作用域是按字面文本确定的：**模块内定义的函数的全局作用域就是该模块的命名空间，无论该函数从什么地方或以什么别名被调用。另一方面，实际的名称搜索是在运行时动态完成的。但是，Python 正在朝着“编译时静态名称解析”的方向发展，因此不要过于依赖动态名称解析！（局部变量已经是被静态确定了。）**

Python 有一个特殊规定。如果不存在生效的 [`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global) 或 [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal) 语句，则对名称的赋值总是会进入最内层作用域。**赋值不会复制数据，只是将名称绑定到对象**。**删除也是如此：语句 `del x` 从局部作用域引用的命名空间中移除对 `x` 的绑定**。所有引入新名称的操作都是使用局部作用域：尤其是 [`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import) 语句和函数定义会在局部作用域中绑定模块或函数名称。

[`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global) 语句用于表明特定变量在全局作用域里，并应在全局作用域中重新绑定；[`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal) 语句表明特定变量在外层作用域中，并应在外层作用域中重新绑定。

```python
def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)
```

执行结果：

```bash
(ollama) kevin@Desktop:~/mmdetection$ python demo/test.py 
After local assignment: test spam
After nonlocal assignment: nonlocal spam
After global assignment: nonlocal spam
In global scope: global spam
```

在小的命名空间内屏蔽其他命名空间同名变量

注意，**局部** 赋值（这是默认状态）不会改变 *scope_test* 对 *spam* 的绑定。 [`nonlocal`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#nonlocal) 赋值会改变 *scope_test* 对 *spam* 的绑定，而 [`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global) 赋值会改变模块层级的绑定。

而且，[`global`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#global) 赋值前没有 *spam* 的绑定。

### Best Practice：Leetcode 141 环形链表

这里使用了类的成员变量

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head
        while fast is not None and fast.next is not None:
            fast = fast.next.next
            slow = slow.next
            if slow == fast:
                return True

        return False
        
```

### Best Practice: Leetcode 142 环形链表 II

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        have_cycle = False
        while fast is not None and fast.next is not None:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                break
        
        slow = head
        while fast is not None and fast.next is not None:
            if fast == slow:
                return slow
            fast = fast.next
            slow = slow.next

        return None 
```

### Best Practice: Leetcode 94 二叉树的中序遍历

这里犯了一个错误，当root为空的时候，一定要返回空列表，而不是空对象

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        road = []
        if root is None:
            return road
        road.extend(self.inorderTraversal(root.left))
        road.append(root.val)
        road.extend(self.inorderTraversal(root.right))
        return road
```

### Best Practice：Leetcode 104 二叉树的最大深度

类的对象调用类中的函数，要使用`self`

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0
        
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        return max(left_depth, right_depth)+1
```

### 9.3. 初探类

类引入了一点新语法，三种新的对象类型和一些新语义。

#### 9.3.1. 类定义语法

最简单的类定义形式如下：

```python
class ClassName:
    <语句-1>
    .
    .
    .
    <语句-N>
```

**与函数定义 ([`def`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#def) 语句) 一样，类定义必须先执行才能生效。把类定义放在 [`if`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#if) 语句的分支里或函数内部试试。**

在实践中，类定义内的语句通常都是函数定义，但也可以是其他语句。这部分内容稍后再讨论。类里的函数定义一般是特殊的参数列表，这是由方法调用的约定规范所指明的 --- 同样，稍后再解释。

**当进入类定义时，将创建一个新的命名空间，并将其用作局部作用域** --- 因此，所有对局部变量的赋值都是在这个新命名空间之内。 **特别的，函数定义会绑定到这里的新函数名称。**

**当 (从结尾处) 正常离开类定义时，将创建一个 *类对象***。 这基本上是一个围绕类定义所创建的命名空间的包装器；我们将在下一节中了解有关类对象的更多信息。 原始的 (在进入类定义之前有效的) 作用域将重新生效，类对象将在这里与类定义头所给出的类名称进行绑定 (在这个示例中为 `ClassName`)。

#### 9.3.2. Class 对象

类对象支持两种操作：属性引用和实例化。

*属性引用* 使用 Python 中所有属性引用所使用的标准语法: `obj.name`。 有效的属性名称是类对象被创建时存在于类命名空间中的所有名称。 因此，如果类定义是这样的:

```python
class MyClass:
    """一个简单的示例类"""
    i = 12345

    def f(self):
        return 'hello world'
```

那么 `MyClass.i` 和 `MyClass.f` 就是有效的属性引用，将分别返回一个整数和一个函数对象。 类属性也可以被赋值，因此可以通过赋值来改变 `MyClass.i` 的值。 [`__doc__`](https://docs.python.org/zh-cn/3/reference/datamodel.html#type.__doc__) 也是一个有效的属性，将返回所属类的文档字符串: `"A simple example class"`。

类的 *实例化* 使用函数表示法。 可以把类对象视为是返回该类的一个新实例的不带参数的函数。 举例来说（假设使用上述的类）:

```python
x = MyClass()
```

创建类的新 *实例* 并将此对象分配给局部变量 `x`。

实例化操作 (“调用”类对象) 会创建一个空对象。 许多类都希望创建的对象实例是根据特定初始状态定制的。 因此一个类可能会定义名为 [`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__) 的特殊方法，就像这样:

```python
def __init__(self):
    self.data = []
```

当一个类定义了 [`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__) 方法时，类的实例化会自动为新创建的类实例发起调用 `__init__()`。 因此在这个例子中，可以通过以下语句获得一个已初始化的新实例:

```python
x = MyClass()
```

当然，[`__init__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html#object.__init__) 方法还有一些参数用于实现更高的灵活性。 在这种情况下，提供给类实例化运算符的参数将被传递给 `__init__()`。 例如，

```python
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart

x = Complex(3.0, -4.5)
x.r, x.i
(3.0, -4.5)
```

#### 9.3.3. 实例对象

现在我们能用实例对象做什么？ 实例对象所能理解的唯一操作是属性引用。 有两种有效的属性名称：数据属性和方法。

*数据属性* 对应于 Smalltalk 中的“实例变量”，以及 C++ 中的“数据成员”。 数据属性不需要声明；就像局部变量一样，它们将在首次被赋值时产生。 举例来说，如果 `x` 是上面创建的 `MyClass` 的实例，则以下代码将打印数值 `16`，且不保留任何追踪信息:

```python
x.counter = 1
while x.counter < 10:
    x.counter = x.counter * 2
print(x.counter)
del x.counter
```

**另一种实例属性引用称为 *方法*。 方法是“从属于”对象的函数。**

实例对象的有效方法名称依赖于其所属的类。 根据定义，一个类中所有是函数对象的属性都是定义了其实例的相应方法。 因此在我们的示例中，`x.f` 是有效的方法引用，因为 `MyClass.f` 是一个函数，而 `x.i` 不是方法，因为 `MyClass.i` 不是函数。 但是 `x.f` 与 `MyClass.f` 并不是一回事 --- 它是一个 *方法对象*，不是函数对象。

#### 9.3.4. 方法对象

通常，方法在绑定后立即被调用:

```python
x.f()
```

在 `MyClass` 示例中，这将返回字符串 `'hello world'`。 但是，方法并不是必须立即调用: `x.f` 是一个方法对象，它可以被保存起来以后再调用。 例如:

```python
xf = x.f
while True:
    print(xf())
```

将持续打印 `hello world`，直到结束。

当一个方法被调用时究竟会发生什么？ 你可能已经注意到尽管 `f()` 的函数定义指定了一个参数，但上面调用 `x.f()` 时却没有带参数。 **这个参数发生了什么事？ 当一个需要参数的函数在不附带任何参数的情况下被调用时 Python 肯定会引发异常 --- 即使参数实际上没有被使用...**

实际上，你可能已经猜到了答案：方法的特殊之处就在于实例对象会作为函数的第一个参数被传入。 在我们的示例中，调用 `x.f()` 其实就相当于 `MyClass.f(x)`。 总之，调用一个具有 *n* 个参数的方法就相当于调用再多一个参数的对应函数，这个参数值为方法所属实例对象，位置在其他参数之前。

总而言之，方法的运作方式如下。 当一个实例的非数据属性被引用时，将搜索该实例所属的类。 如果名称表示一个属于函数对象的有效类属性，则指向实例对象和函数对象的引用将被打包为一个方法对象。 当传入一个参数列表调用该方法对象时，将基于实例对象和参数列表构造一个新的参数列表，并传入这个新参数列表调用相应的函数对象。

#### 9.3.5. 类和实例变量

一般来说，**实例变量用于每个实例的唯一数据，而类变量用于类的所有实例共享的属性和方法:**

```python
>>> class Dog:
...     kind = 'canine'
...     def __init__(self, name):
...             self.name = name
...
>>> d = Dog("Fido")
>>> e = Dog("Buddy")
>>> d.kind
'canine'
>>> e.kind
'canine'
>>> d.name
'Fido'
>>> e.name
'Buddy'
```

正如 [名称和对象](https://docs.python.org/zh-cn/3/tutorial/classes.html#tut-object) 中已讨论过的，共享数据可能在涉及 [mutable](https://docs.python.org/zh-cn/3/glossary.html#term-mutable) 对象例如列表和字典的时候导致令人惊讶的结果。 例如以下代码中的 *tricks* 列表不应该被用作类变量，因为所有的 *Dog* 实例将只共享一个单独的列表:

```python
class Dog:

    tricks = []             # 类变量的错误用法

    def __init__(self, name):
        self.name = name

    def add_trick(self, trick):
        self.tricks.append(trick)

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks                # 非预期地被所有的 Dog 实例所共享
['roll over', 'play dead']
```

正确的类设计应该使用实例变量:

```python
class Dog:

    def __init__(self, name):
        self.name = name
        self.tricks = []    # 为每个 Dog 实例新建一个空列表

    def add_trick(self, trick):
        self.tricks.append(trick)

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks
['roll over']
>>> e.tricks
['play dead']
```

### 9.4. 补充说明

**如果同样的属性名称同时出现在实例和类中，则属性查找会优先选择实例**:

```python
class Warehouse:
   purpose = 'storage'
   region = 'west'

w1 = Warehouse()
print(w1.purpose, w1.region)
storage west
w2 = Warehouse()
w2.region = 'east'
print(w2.purpose, w2.region)
storage east
```

数据属性可以被方法以及一个对象的普通用户（“客户端”）所引用。 换句话说，类不能用于实现纯抽象数据类型。 实际上，在 Python 中没有任何东西能强制隐藏数据 --- 它是完全基于约定的。 （而在另一方面，用 C 语言编写的 Python 实现则可以完全隐藏实现细节，并在必要时控制对象的访问；此特性可以通过用 C 编写 Python 扩展来使用。）

客户端应当谨慎地使用数据属性 --- 客户端可能通过直接操作数据属性的方式破坏由方法所维护的固定变量。 请注意客户端可以向一个实例对象添加他们自己的数据属性而不会影响方法的可用性，只要保证避免名称冲突 --- 再次提醒，在此使用命名约定可以省去许多令人头痛的麻烦。

在方法内部引用数据属性（或其他方法！）并没有简便方式。 我发现这实际上提升了方法的可读性：当浏览一个方法代码时，不会存在混淆局部变量和实例变量的机会。

方法的第一个参数常常被命名为 `self`。 这也不过就是一个约定: `self` 这一名称在 Python 中绝对没有特殊含义。 但是要注意，不遵循此约定会使得你的代码对其他 Python 程序员来说缺乏可读性，而且也可以想像一个 *类浏览器* 程序的编写可能会依赖于这样的约定。

任何一个作为类属性的函数都为该类的实例定义了一个相应方法。 函数定义的文本并非必须包含于类定义之内：将一个函数对象赋值给一个局部变量也是可以的。 例如:

```python
# 在类之外定义的函数
def f1(self, x, y):
    return min(x, x+y)

class C:
    f = f1

    def g(self):
        return 'hello world'

    h = g
```

现在 `f`、`g` 和 `h` 都 `C` 类的指向函数对象的属性，因此它们都是 `C` 实例的方法 --- 其中 `h` 与 `g` 完全等价。 但请注意这种做法通常只会使程序的阅读者感到迷惑。

方法可以通过使用 `self` 参数的方法属性调用其他方法:

```python
class Bag:
    def __init__(self):
        self.data = []

    def add(self, x):
        self.data.append(x)

    def addtwice(self, x):
        self.add(x)
        self.add(x)
```

方法可以通过与普通函数相同的方式引用全局名称。与方法相关联的全局作用域就是包含该方法的定义语句的模块。（类永远不会被用作全局作用域。）尽管一个人很少会有好的理由在方法中使用全局作用域中的数据，全局作用域依然存在许多合理的使用场景：举个例子，导入到全局作用域的函数和模块可以被方法所使用，定义在全局作用域中的函数和类也一样。通常，包含该方法的类本身就定义在全局作用域中，而在下一节中我们将会发现，为何有些时候方法需要引用其所属类。

**每个值都是一个对象，因此具有 *类* （也称为 *类型*），并存储为 `object.__class__` 。**

### 9.5. 继承

当然，如果不支持继承，语言特性就不值得称为“类”。派生类定义的语法如下所示:

```python
class DerivedClassName(BaseClassName):
    <语句-1>
    .
    .
    .
    <语句-N>
```

**名称 `BaseClassName` 必须定义于可从包含所派生的类的定义的作用域访问的命名空间中**。 作为基类名称的替代，也允许使用其他任意表达式。 例如，当基类定义在另一个模块中时，这就会很有用处:

```python
class DerivedClassName(modname.BaseClassName):
```

**派生类定义的执行过程与基类相同。 当构造类对象时，基类会被记住。 此信息将被用来解析属性引用：如果请求的属性在类中找不到，搜索将转往基类中进行查找。 如果基类本身也派生自其他某个类，则此规则将被递归地应用。**

派生类的实例化没有任何特殊之处: `DerivedClassName()` 会创建该类的一个新实例。 方法引用将按以下方式解析：**搜索相应的类属性，如有必要将按基类继承链逐步向下查找，如果产生了一个函数对象则方法引用就生效**。

**派生类可能会重写其基类的方法**。 因为方法在调用同一对象的其他方法时没有特殊权限，所以基类方法在尝试调用调用同一基类中定义的另一方法时，可能实际上调用是该基类的派生类中定义的方法。（**对 C++ 程序员的提示：Python 中所有的方法实际上都是 `virtual` 方法。**）

在派生类中的重写方法实际上可能想要扩展而非简单地替换同名的基类方法。 有一种方式可以简单地直接调用基类方法：即调用 `BaseClassName.methodname(self, arguments)`。 有时这对客户端来说也是有用的。 （请注意仅当此基类可在全局作用域中以 `BaseClassName` 的名称被访问时方可使用此方式。）

Python有两个内置函数可被用于继承机制：

- 使用 [`isinstance()`](https://docs.python.org/zh-cn/3/library/functions.html#isinstance) 来检查一个实例的类型: `isinstance(obj, int)` 仅会在 `obj.__class__` 为 [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int) 或某个派生自 [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int) 的类时为 `True`。
- 使用 [`issubclass()`](https://docs.python.org/zh-cn/3/library/functions.html#issubclass) 来检查类的继承关系: `issubclass(bool, int)` 为 `True`，因为 [`bool`](https://docs.python.org/zh-cn/3/library/functions.html#bool) 是 [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int) 的子类。 但是，`issubclass(float, int)` 为 `False`，因为 [`float`](https://docs.python.org/zh-cn/3/library/functions.html#float) 不是 [`int`](https://docs.python.org/zh-cn/3/library/functions.html#int) 的子类。

#### 9.5.1. 多重继承

Python 也支持一种多重继承。 带有多个基类的类定义语句如下所示:

```python
class DerivedClassName(Base1, Base2, Base3):
    <语句-1>
    .
    .
    .
    <语句-N>
```

对于多数目的来说，在最简单的情况下，**你可以认为搜索从父类所继承属性的操作是深度优先、从左到右的，当层次结构存在重叠时不会在同一个类中搜索两次。** 因此，如果某个属性在 `DerivedClassName` 中找不到，就会在 `Base1` 中搜索它，然后（递归地）在 `Base1` 的基类中搜索，如果在那里也找不到，就将在 `Base2` 中搜索，依此类推。

真实情况比这个更复杂一些；方法解析顺序会动态改变以支持对 [`super()`](https://docs.python.org/zh-cn/3/library/functions.html#super) 的协同调用。 **这种方式在某些其他多重继承型语言中被称为后续方法调用**，它比单继承型语言中的 super 调用更强大。

动态调整顺序是有必要的，**因为所有多重继承的情况都会显示出一个或更多的菱形关联**（即至少有一个上级类可通过多条路径被最底层的类所访问）。 例如，所有类都是继承自 [`object`](https://docs.python.org/zh-cn/3/library/functions.html#object)，因此任何多重继承的情况都提供了一条以上的路径可以通向 [`object`](https://docs.python.org/zh-cn/3/library/functions.html#object)。 为了确保基类不会被访问一次以上，动态算法会用一种特殊方式将搜索顺序线性化，**保留每个类所指定的从左至右的顺序，只调用每个上级类一次，并且保持单调性**（即一个类可以被子类化而不影响其父类的优先顺序）。 总而言之，这些特性使得设计具有多重继承的可靠且可扩展的类成为可能。 要了解更多细节，请参阅 [Python 2.3 方法解析顺序](https://docs.python.org/zh-cn/3/howto/mro.html#python-2-3-mro)。

### 9.6. 私有变量

那种仅限从一个对象内部访问的“私有”实例变量在 Python 中并不存在。 但是，大多数 Python 代码都遵循这样一个约定：**带有一个下划线的名称 (例如 `_spam`) 应该被当作是 API 的非公有部分 (无论它是函数、方法或是数据成员)。 这应当被视为一个实现细节，可能不经通知即加以改变。**

由于存在对于类私有成员的有效使用场景（例如避免名称与子类所定义的名称相冲突），因此存在对此种机制的有限支持，称为 ***名称改写***。 任何形式为 `__spam` 的标识符（至少带有两个前缀下划线，至多一个后缀下划线）的文本将被替换为 `_classname__spam`，其中 `classname` 为去除了前缀下划线的当前类名称。 这种改写不考虑标识符的句法位置，只要它出现在类定义内部就会进行。

**名称改写有助于让子类重写方法而不破坏类内方法调用。例如:**

```python
class Mapping:
    def __init__(self, iterable):
        self.items_list = []
        self.__update(iterable)

    def update(self, iterable):
        for item in iterable:
            self.items_list.append(item)

    __update = update   # 原始 update() 方法的私有副本

class MappingSubclass(Mapping):

    def update(self, keys, values):
        # 为 update() 提供了新的签名
        # 但不会破坏 __init__()
        for item in zip(keys, values):
            self.items_list.append(item)
```

上面的示例即使在 `MappingSubclass` 引入了一个 `__update` 标识符的情况下也不会出错，因为它会在 `Mapping` 类中被替换为 `_Mapping__update` 而在 `MappingSubclass` 类中被替换为 `_MappingSubclass__update`。

请注意，**改写规则的设计主要是为了避免意外冲突**；访问或修改被视为私有的变量仍然是可能的。这在特殊情况下甚至会很有用，例如在调试器中。

请注意传递给 `exec()` 或 `eval()` 的代码不会将发起调用类的类名视作当前类；这类似于 `global` 语句的效果，因此这种效果仅限于同时经过字节码编译的代码。 同样的限制也适用于 `getattr()`, `setattr()` 和 `delattr()`，以及对于 `__dict__` 的直接引用。

### 9.7. 杂项说明

有时具有类似于 Pascal "record" 或 C "struct" 的数据类型是很有用的，将一些带名称的数据项捆绑在一起。 实现这一目标的理想方式是使用 [`dataclasses`](https://docs.python.org/zh-cn/3/library/dataclasses.html#module-dataclasses):

```python
>>> from dataclasses import dataclass
>>> @dataclass
... class Employee:
...     name: str
...     dept: str
...     salary: int
...
>>> john = Employee('john', 'computer lab', 1000)
>>> john.dept
'computer lab'
>>> john.salary
1000
```

一段期望使用特定抽象数据类型的 Python 代码通常可以通过传入一个模拟了该数据类型的方法的类作为替代。 例如，如果你有一个基于文件对象来格式化某些数据的函数，你可以定义一个带有 [`read()`](https://docs.python.org/zh-cn/3/library/io.html#io.TextIOBase.read) 和 [`readline()`](https://docs.python.org/zh-cn/3/library/io.html#io.TextIOBase.readline) 方法以便从字典串缓冲区获取数据的类，并将其作为参数传入。

[实例方法对象](https://docs.python.org/zh-cn/3/reference/datamodel.html#instance-methods) 也具有属性: [`m.__self__`](https://docs.python.org/zh-cn/3/reference/datamodel.html#method.__self__) 就是带有 `m()` 方法的实例对象，而 [`m.__func__`](https://docs.python.org/zh-cn/3/reference/datamodel.html#method.__func__) 就是该方法所对应的 [函数对象](https://docs.python.org/zh-cn/3/reference/datamodel.html#user-defined-funcs)。

### 9.8. 迭代器

到目前为止，您可能已经注意到大多数容器对象都可以使用 [`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for) 语句:

```python
for element in [1, 2, 3]:
    print(element)
for element in (1, 2, 3):
    print(element)
for key in {'one':1, 'two':2}:
    print(key)
for char in "123":
    print(char)
for line in open("myfile.txt"):
    print(line, end='')
```

这种访问风格清晰、简洁又方便。 迭代器的使用非常普遍并使得 Python 成为一个统一的整体。 在幕后，**[`for`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#for) 语句会在容器对象上调用 [`iter()`](https://docs.python.org/zh-cn/3/library/functions.html#iter)。 该函数返回一个定义了 [`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__) 方法的迭代器对象，此方法将逐一访问容器中的元素。** 当元素用尽时，[`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__) 将引发 [`StopIteration`](https://docs.python.org/zh-cn/3/library/exceptions.html#StopIteration) 异常来通知终止 `for` 循环。 你可以使用 [`next()`](https://docs.python.org/zh-cn/3/library/functions.html#next) 内置函数来调用 [`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__) 方法；这个例子显示了它的运作方式:

```python
>>> s = "abc"
>>> it = iter(s)
>>> it
<str_iterator object at 0x7fd8f7816cb0>
>>> next(it)
'a'
>>> next(it)
'b'
>>> next(it)
'c'
>>> next(it)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

了解了迭代器协议背后的机制后，就可以轻松地为你的类添加迭代器行为了。 定义 [`__iter__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#container.__iter__) 方法用于返回一个带有 [`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__next__) 方法的对象。 如果类已定义了 `__next__()`，那么 `__iter__()` 可以简单地返回 `self`:

```python
class Reverse:
    """对一个序列执行反向循环的迭代器"""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index-1
        return self.data[self.index]
    
rev = Reverse("spam")
iter(rev)
for char in rev:
    print(char)
```

执行结果：

```bash
(base) kevin@Desktop:~/playground$ /usr/local/bin/python3.9 /home/kevin/playground/test.py
m
a
p
s
```

### 9.9. 生成器

[生成器](https://docs.python.org/zh-cn/3/glossary.html#term-generator) 是一个用于创建迭代器的简单而强大的工具。 **它们的写法类似于标准的函数，但当它们要返回数据时会使用 [`yield`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#yield) 语句。** 每次在生成器上调用 [`next()`](https://docs.python.org/zh-cn/3/library/functions.html#next) 时，它会从上次离开的位置恢复执行（它会记住上次执行语句时的所有数据值）。 一个显示如何非常容易地创建生成器的示例如下:

```python
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]
        
for char in reverse("golf"):
    print(char)
```

执行结果：

```bash
(base) kevin@Desktop:~/playground$ /usr/local/bin/python3.9 /home/kevin/playground/test.py
f
l
o
g
```

可以用生成器来完成的任何功能同样可以通用前一节所描述的基于类的迭代器来完成。 但生成器的写法更为紧凑，因为它会自动创建 [`__iter__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.__iter__) 和 [`__next__()`](https://docs.python.org/zh-cn/3/reference/expressions.html#generator.__next__) 方法。

**另一个关键特性在于局部变量和执行状态会在每次调用之间自动保存。 这使得该函数相比使用 `self.index` 和 `self.data` 这种实例变量的方式更易编写且更为清晰。**

**除了会自动创建方法和保存程序状态，当生成器终结时，它们还会自动引发 [`StopIteration`](https://docs.python.org/zh-cn/3/library/exceptions.html#StopIteration)。 这些特性结合在一起，使得创建迭代器能与编写常规函数一样容易。**

### 9.10. 生成器表达式

某些简单的生成器可以写成简洁的表达式代码，所用语法类似列表推导式，**但外层为圆括号而非方括号**。 这种表达式被设计用于生成器将立即被外层函数所使用的情况。 生成器表达式相比完整的生成器更紧凑但较不灵活，相比等效的列表推导式则更为节省内存。

```python
>>> sum(i*i for i in range(10))
285
>>> xvec = [10, 20, 30]
>>> yvec = [7, 5, 3]
>>> sum(x*y for x,y in zip(xvec, yvec))
260
>>> data = "golf"
>>> list(data[i] for i in range(len(data)-1, -1, -1))
['f', 'l', 'o', 'g']
```

## 10. 标准库简介

### 10.1. 操作系统接口

[`os`](https://docs.python.org/zh-cn/3/library/os.html#module-os) 模块提供了许多与操作系统交互的函数:

```bash
>>> import os
>>> os.getcwd()
'/home/kevin'
>>> os.chdir("/home/kevin/mmdetection")
>>> os.getcwd()
'/home/kevin/mmdetection'
>>> os.system("cd ..")
0
>>> os.getcwd()
'/home/kevin/mmdetection'
>>> os.chdir("/home/kevin/")
>>> os.getcwd()
'/home/kevin'
>>> os.system("mkdir today")
0
>>> exit()
(base) kevin@Desktop:~$ ls today/
(base) kevin@Desktop:~$ ls -a today/
.  ..
(base) kevin@Desktop:~$ ls | grep today
today
```

一定要使用 `import os` 而不是 `from os import *` 。这将避免内建的 [`open()`](https://docs.python.org/zh-cn/3/library/functions.html#open) 函数被 [`os.open()`](https://docs.python.org/zh-cn/3/library/os.html#os.open) 隐式替换掉，因为它们的使用方式大不相同。

**内置的 [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir) 和 [`help()`](https://docs.python.org/zh-cn/3/library/functions.html#help) 函数可用作交互式辅助工具，用于处理大型模块**，如 [`os`](https://docs.python.org/zh-cn/3/library/os.html#module-os):

```python
>>> dir(os)
['CLD_CONTINUED', 'CLD_DUMPED', 'CLD_EXITED', 'CLD_KILLED', 'CLD_STOPPED', 'CLD_TRAPPED', 'DirEntry', 'EFD_CLOEXEC', 'EFD_NONBLOCK', 'EFD_SEMAPHORE', 'EX_CANTCREAT', 'EX_CONFIG', 'EX_DATAERR', 'EX_IOERR', 'EX_NOHOST', 'EX_NOINPUT', 'EX_NOPERM', 'EX_NOUSER', 'EX_OK', 'EX_OSERR', 'EX_OSFILE', 'EX_PROTOCOL', 'EX_SOFTWARE', 'EX_TEMPFAIL', 'EX_UNAVAILABLE', 'EX_USAGE', 'F_LOCK', 'F_OK', 'F_TEST', 'F_TLOCK', 'F_ULOCK', 'GRND_NONBLOCK', 'GRND_RANDOM', 'GenericAlias', 'Mapping', 'MutableMapping', 'NGROUPS_MAX', 'O_ACCMODE', 'O_APPEND', 'O_ASYNC', 'O_CLOEXEC', 'O_CREAT', 'O_DIRECT', 'O_DIRECTORY', 'O_DSYNC', 'O_EXCL', 'O_FSYNC', 'O_LARGEFILE', 'O_NDELAY', 'O_NOATIME', 'O_NOCTTY', 'O_NOFOLLOW', 'O_NONBLOCK', 'O_PATH', 'O_RDONLY', 'O_RDWR', 'O_RSYNC', 'O_SYNC', 'O_TMPFILE', 'O_TRUNC', 'O_WRONLY', 'POSIX_FADV_DONTNEED', 'POSIX_FADV_NOREUSE', 'POSIX_FADV_NORMAL', 'POSIX_FADV_RANDOM', 'POSIX_FADV_SEQUENTIAL', 'POSIX_FADV_WILLNEED', 'POSIX_SPAWN_CLOSE', 'POSIX_SPAWN_DUP2', 'POSIX_SPAWN_OPEN', 'PRIO_PGRP', 'PRIO_PROCESS', 'PRIO_USER', 'P_ALL', 'P_NOWAIT', 'P_NOWAITO', 'P_PGID', 'P_PID', 'P_WAIT', 'PathLike', 'RTLD_DEEPBIND', 'RTLD_GLOBAL', 'RTLD_LAZY', 'RTLD_LOCAL', 'RTLD_NODELETE', 'RTLD_NOLOAD', 'RTLD_NOW', 'R_OK', 'SCHED_BATCH', 'SCHED_FIFO', 'SCHED_IDLE', 'SCHED_OTHER', 'SCHED_RESET_ON_FORK', 'SCHED_RR', 'SEEK_CUR', 'SEEK_DATA', 'SEEK_END', 'SEEK_HOLE', 'SEEK_SET', 'SPLICE_F_MORE', 'SPLICE_F_MOVE', 'SPLICE_F_NONBLOCK', 'ST_APPEND', 'ST_MANDLOCK', 'ST_NOATIME', 'ST_NODEV', 'ST_NODIRATIME', 'ST_NOEXEC', 'ST_NOSUID', 'ST_RDONLY', 'ST_RELATIME', 'ST_SYNCHRONOUS', 'ST_WRITE', 'TMP_MAX', 'WCONTINUED', 'WCOREDUMP', 'WEXITED', 'WEXITSTATUS', 'WIFCONTINUED', 'WIFEXITED', 'WIFSIGNALED', 'WIFSTOPPED', 'WNOHANG', 'WNOWAIT', 'WSTOPPED', 'WSTOPSIG', 'WTERMSIG', 'WUNTRACED', 'W_OK', 'XATTR_CREATE', 'XATTR_REPLACE', 'XATTR_SIZE_MAX', 'X_OK', '_Environ', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '_check_methods', '_execvpe', '_exists', '_exit', '_fspath', '_fwalk', '_get_exports_list', '_spawnvef', '_walk', '_wrap_close', 'abc', 'abort', 'access', 'altsep', 'chdir', 'chmod', 'chown', 'chroot', 'close', 'closerange', 'confstr', 'confstr_names', 'cpu_count', 'ctermid', 'curdir', 'defpath', 'device_encoding', 'devnull', 'dup', 'dup2', 'environ', 'environb', 'error', 'eventfd', 'eventfd_read', 'eventfd_write', 'execl', 'execle', 'execlp', 'execlpe', 'execv', 'execve', 'execvp', 'execvpe', 'extsep', 'fchdir', 'fchmod', 'fchown', 'fdatasync', 'fdopen', 'fork', 'forkpty', 'fpathconf', 'fsdecode', 'fsencode', 'fspath', 'fstat', 'fstatvfs', 'fsync', 'ftruncate', 'fwalk', 'get_blocking', 'get_exec_path', 'get_inheritable', 'get_terminal_size', 'getcwd', 'getcwdb', 'getegid', 'getenv', 'getenvb', 'geteuid', 'getgid', 'getgrouplist', 'getgroups', 'getloadavg', 'getlogin', 'getpgid', 'getpgrp', 'getpid', 'getppid', 'getpriority', 'getrandom', 'getresgid', 'getresuid', 'getsid', 'getuid', 'getxattr', 'initgroups', 'isatty', 'kill', 'killpg', 'lchown', 'linesep', 'link', 'listdir', 'listxattr', 'lockf', 'lseek', 'lstat', 'major', 'makedev', 'makedirs', 'minor', 'mkdir', 'mkfifo', 'mknod', 'name', 'nice', 'open', 'openpty', 'pardir', 'path', 'pathconf', 'pathconf_names', 'pathsep', 'pipe', 'pipe2', 'popen', 'posix_fadvise', 'posix_fallocate', 'posix_spawn', 'posix_spawnp', 'pread', 'preadv', 'putenv', 'pwrite', 'pwritev', 'read', 'readlink', 'readv', 'register_at_fork', 'remove', 'removedirs', 'removexattr', 'rename', 'renames', 'replace', 'rmdir', 'scandir', 'sched_get_priority_max', 'sched_get_priority_min', 'sched_getaffinity', 'sched_getparam', 'sched_getscheduler', 'sched_param', 'sched_rr_get_interval', 'sched_setaffinity', 'sched_setparam', 'sched_setscheduler', 'sched_yield', 'sendfile', 'sep', 'set_blocking', 'set_inheritable', 'setegid', 'seteuid', 'setgid', 'setgroups', 'setpgid', 'setpgrp', 'setpriority', 'setregid', 'setresgid', 'setresuid', 'setreuid', 'setsid', 'setuid', 'setxattr', 'spawnl', 'spawnle', 'spawnlp', 'spawnlpe', 'spawnv', 'spawnve', 'spawnvp', 'spawnvpe', 'splice', 'st', 'stat', 'stat_result', 'statvfs', 'statvfs_result', 'strerror', 'supports_bytes_environ', 'supports_dir_fd', 'supports_effective_ids', 'supports_fd', 'supports_follow_symlinks', 'symlink', 'sync', 'sys', 'sysconf', 'sysconf_names', 'system', 'tcgetpgrp', 'tcsetpgrp', 'terminal_size', 'times', 'times_result', 'truncate', 'ttyname', 'umask', 'uname', 'uname_result', 'unlink', 'unsetenv', 'urandom', 'utime', 'wait', 'wait3', 'wait4', 'waitid', 'waitid_result', 'waitpid', 'waitstatus_to_exitcode', 'walk', 'write', 'writev']
>>> help(os)

```

对于日常文件和目录管理任务， [`shutil`](https://docs.python.org/zh-cn/3/library/shutil.html#module-shutil) 模块提供了更易于使用的更高级别的接口:

```bash
(base) kevin@Desktop:~/today$ python
Python 3.10.12 (main, Jul  5 2023, 18:54:27) [GCC 11.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import shutil
>>> shutil.copyfile('test.file', 'test.txt')
'test.txt'
>>> shutil.move('TEST', 'test.md')
'test.md'
>>> exit()
(base) kevin@Desktop:~/today$ ls
test.file  test.md  test.txt
(base) kevin@Desktop:~/today$
(base) kevin@Desktop:~/today$
(base) kevin@Desktop:~/today$
(base) kevin@Desktop:~/today$ cat test.file
TEST
(base) kevin@Desktop:~/today$ cat test.md
(base) kevin@Desktop:~/today$ cat test.txt
TEST
```

### 10.2. 文件通配符

[`glob`](https://docs.python.org/zh-cn/3/library/glob.html#module-glob) 模块提供了一个在目录中使用通配符搜索创建文件列表的函数:

```python
>>> import glob
>>> glob.glob("*.py")
['mask-rcnn_swin-t-p4-w7_fpn_amp-ms-crop-1x_cow.py', 'rtmdet-ins_s_1xb4-300e_cow_update_20240325.py', 'rtmdet_m_8xb32-300e_cow_update.py', 'rtmdet-ins_m_1xb4-300e_cow_update.py', 'rtmdet-ins_m_1xb4-300e_cow_update_20241005.py', 'solo_r50_fpn_1x_cow_update_0602.py', 'solo_r50_fpn_1x_cow_update_1005.py', 'rtmdet-ins_m_1xb4-300e_cow_update_20240325.py', 'solov2_r50_fpn_ms-3x_cow_update_0602.py', 'yolact_r50_1xb1-55e_cow.py', 'yolact_r50_1xb2-150e_cow_update_0602.py', 'rtmdet-ins_s_1xb4-300e_cow_update_20240327.py', 'rtmdet-ins_tiny_1xb4-500e_cow_update_20241202.py', 'mask-rcnn_r50_fpn_1x_cow_update_0325.py', 'rtmdet-ins_s_1xb4-400e_cow_update_20241216.py', 'yolact_r50_1xb1-100e_cow.py', 'rtmdet-ins_m_1xb4-300e_5e-5_cow_update.py', 'mask-rcnn_r50_fpn_1x_cow_update_1005.py', 'mask-rcnn_r50_fpn_1x_cow_update_0603.py', 'yolact_r50_1xb2-150e_cow.py', 'rtmdet-ins_tiny_1xb4-500e_cow_update_20240416.py', 'decoupled-solo-light_r50_fpn_3x_cow_update_0602.py', 'yolact_r50_1xb2-150e_cow_update_1005.py', 'rtmdet-ins_s_1xb4-300e_cow_update_20240603.py', 'solov2_r50_fpn_1x_cow_update_0602.py', 'solo_r50_fpn_1x_cow_update_0325.py', 'rtmdet-ins_s_1xb4-300e_cow_update_20241017.py', 'solov2_r50_fpn_ms-3x_cow_update_1005.py', 'yolact_r50_1xb2-150e_cow_update_0325.py', 'yolact_r50_1xb2-150e_cow_update.py', 'rtmdet-ins_m_1xb4-300e_cow_update_20240604.py', 'rtmdet-ins_tiny_1xb4-500e_cow_update_20241017.py', 'yolact_r50_1xb2-regional_cow.py']
```

### 10.3. 命令行参数

一般的工具脚本常常需要处理命令行参数。 这些参数以列表形式存储在 [`sys`](https://docs.python.org/zh-cn/3/library/sys.html#module-sys) 模块的 *argv* 属性中。 举例来说，让我们查看下面的 `demo.py` 文件:

```python
>>> import sys
>>> print(sys.argv)
['']
```

[`argparse`](https://docs.python.org/zh-cn/3/library/argparse.html#module-argparse) 模块提供了一种更复杂的机制来处理命令行参数。 以下脚本可提取一个或多个文件名，并可选择要显示的行数:

```python
import argparse

parser = argparse.ArgumentParser(
    prog='top',
    description='Show top lines from each file')
parser.add_argument('filenames', nargs='+')
parser.add_argument('-l', '--lines', type=int, default=10)
args = parser.parse_args()
print(args)
```

当在通过 `python top.py --lines=5 alpha.txt beta.txt` 在命令行运行时，该脚本会将 `args.lines` 设为 `5` 并将 `args.filenames` 设为 `['alpha.txt', 'beta.txt']`。

### 10.4. 错误输出重定向和程序终止

[`sys`](https://docs.python.org/zh-cn/3/library/sys.html#module-sys) 模块还具有 *stdin* ， *stdout* 和 *stderr* 的属性。后者对于发出警告和错误消息非常有用，即使在 *stdout* 被重定向后也可以看到它们:

```python
>>> sys.stderr.write('Warning, log file not found starting a new one\n')
Warning, log file not found starting a new one
47
```

终止脚本的最直接方法是使用 `sys.exit()` 。

### 10.5. 字符串模式匹配

[`re`](https://docs.python.org/zh-cn/3/library/re.html#module-re) 模块为高级字符串处理提供正则表达式工具。对于复杂的匹配和操作，正则表达式提供简洁，优化的解决方案:

```python
>>> import re
>>> re.findall(r'\bf[a-z]', "which foot or hand fell fastest")
['fo', 'fe', 'fa']
>>> re.findall(r'\bf[a-z]*', "which foot or hand fell fastest")
['foot', 'fell', 'fastest']
```

这句话描述了一个正则表达式 `r'\bf[a-z]*'` 在字符串 `"which foot or hand fell fastest"` 中匹配的结果。

#### 解析：

1. **正则表达式 `r'\bf[a-z]\*'`**：

   - `\b`：表示单词边界，确保匹配的内容是从单词的开头开始。
   - `f`：匹配字母 `f`，即所有以 `f` 开头的单词。
   - `[a-z]*`：匹配零个或多个小写字母。

2. **匹配逻辑**：

   - 正则表达式会寻找所有以 `f` 开头的小写单词，并且只能匹配单词的起始部分（因为有 `\b` 限定）。

3. **在字符串中匹配**：

   - 字符串是 `"which foot or hand fell fastest"`。

   - 按正则表达式规则，匹配以 

     ```
     f
     ```

      开头的单词边界：

     - `foot`：匹配成功。
     - `fell`：匹配成功。
     - `fastest`：匹配成功。

4. **最终结果**： 匹配到的单词是 `['foot', 'fell', 'fastest']`。

#### 翻译：

“在字符串中找到所有以 `f` 开头的单词，并返回它们：`foot`, `fell`, `fastest`。”

以下是一些使用 Python 中的 `re` 模块（正则表达式）的实用技巧，可以帮助你高效处理文本：

------

#### **1. 基本用法**

- **匹配单词**：使用 `re.findall()` 找出所有符合模式的内容。

  ```python
  import re
  text = "apple, banana, cherry, date"
  print(re.findall(r'\b[a-z]{5}\b', text))  # 匹配长度为5的单词
  # 输出: ['apple', 'cherry']
  ```

- **替换文本**：使用 `re.sub()` 替换匹配的内容。

  ```python
  text = "I love apples and oranges."
  new_text = re.sub(r'apples|oranges', 'fruits', text)
  print(new_text)  # 输出: I love fruits and fruits.
  ```

- **分割字符串**：使用 `re.split()` 按模式分割字符串。

  ```python
  text = "apple1banana2cherry3"
  print(re.split(r'\d+', text))  # 使用数字分割
  # 输出: ['apple', 'banana', 'cherry', '']
  ```

------

#### **2. 常用正则表达式模式**

- **匹配特定字符**：
  - `.`：匹配任意字符（除换行符）。
  - `\d`：匹配数字 `[0-9]`。
  - `\w`：匹配单词字符（字母、数字、下划线）。
  - `\s`：匹配空白字符（空格、制表符等）。
  - `[a-z]`：匹配小写字母范围。
  - `[A-Z]`：匹配大写字母范围。
- **重复次数**：
  - `*`：匹配零次或多次。
  - `+`：匹配一次或多次。
  - `?`：匹配零次或一次。
  - `{n}`：匹配指定次数 `n`。
  - `{n,m}`：匹配 `n` 到 `m` 次。
- **特殊边界**：
  - `^`：匹配字符串的开头。
  - `$`：匹配字符串的结尾。
  - `\b`：匹配单词边界。
  - `\B`：非单词边界。

------

#### **3. 高级技巧**

##### **1）命名捕获组**

为捕获的子模式命名，方便后续引用。

```python
text = "2025-01-02"
pattern = r'(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})'
match = re.search(pattern, text)
if match:
    print(match.group('year'))   # 输出: 2025
    print(match.group('month'))  # 输出: 01
    print(match.group('day'))    # 输出: 02
```

##### **2）非捕获组**

用 `(?:...)` 定义不需要捕获的分组，提升效率。

```python
text = "apple banana apple cherry"
pattern = r'(?:apple|banana)'
print(re.findall(pattern, text))  # 输出: ['apple', 'banana', 'apple']
```

##### **3）正向/反向零宽断言**

用零宽断言匹配指定条件的上下文：

- 正向断言

  ```
  (?=...)
  ```

  ：

  ```python
  text = "apple123banana456"
  print(re.findall(r'[a-z]+(?=\d+)', text))  # 输出: ['apple', 'banana']
  ```

- 反向断言

  ```
  (?<=...)
  ```

  ：

  ```python
  text = "123apple456banana"
  print(re.findall(r'(?<=\d+)[a-z]+', text))  # 输出: ['apple', 'banana']
  ```

##### **4）懒惰匹配**

用 `?` 实现懒惰匹配（匹配尽可能短的字符串）。

```python
text = "<div>content</div><div>more</div>"
print(re.findall(r'<div>.*?</div>', text))  # 输出: ['<div>content</div>', '<div>more</div>']
```

------

#### **4. 性能优化**

- **预编译正则表达式**： 使用 `re.compile()` 编译正则表达式，提升多次匹配的效率。

  ```python
  pattern = re.compile(r'\d+')
  for text in ["123abc", "456def"]:
      print(pattern.findall(text))  # 每次都复用已编译的模式
  ```

- **避免回溯过多**： 尽量减少使用贪婪匹配 (`.*` 或 `.*?`)，替代为更明确的匹配模式。

------

#### **5. 调试工具**

- **在线工具**：使用 [regex101](https://regex101.com/) 或类似网站调试正则表达式，支持分组解析和性能分析。

- 标记模式

  ：使用 

  ```
  re.DEBUG
  ```

   查看正则表达式的详细解析信息。

  ```python
  pattern = re.compile(r'\d+', re.DEBUG)
  ```

------

当只需要简单的功能时，首选字符串方法因为它们更容易阅读和调试:

```python
>>> "tea for too".replace("too", "two")
'tea for two'
```

### 10.6. 数学

[`math`](https://docs.python.org/zh-cn/3/library/math.html#module-math) 模块提供对用于浮点数学运算的下层 C 库函数的访问:

```python
>>> import math
>>> math.cos(math.pi / 4)
0.7071067811865476
>>> math.log(1024,2)
10.0
```

[`random`](https://docs.python.org/zh-cn/3/library/random.html#module-random) 模块提供了进行随机选择的工具:

```python
>>> import random
>>> random.choice(["apple", "banana", "pear"])
'banana'
>>> random.choice(["apple", "banana", "pear"])
'apple'
>>> random.choice(["apple", "banana", "pear"])
'apple'
>>> random.choice(["apple", "banana", "pear"])
'banana'
>>> random.choice(["apple", "banana", "pear"])
'pear'
>>> random.sample(range(100), 10)
[38, 56, 23, 34, 63, 95, 58, 22, 78, 7]
>>> random.random()
0.13055455638543578
>>> random.randrange(6)
4
```

[`statistics`](https://docs.python.org/zh-cn/3/library/statistics.html#module-statistics) 模块计算数值数据的基本统计属性（均值，中位数，方差等）:

```python
>>> import statistics
>>> data =  [2.75, 1.75, 1.25, 0.25, 0.5, 1.25, 3.5]
>>> statistics.mean(data)
1.6071428571428572
>>> statistics.median(data)
1.25
>>> statistics.variance(data)
1.3720238095238095
```

### 10.7. 互联网访问

有许多模块可用于访问互联网和处理互联网协议。其中两个最简单的 [`urllib.request`](https://docs.python.org/zh-cn/3/library/urllib.request.html#module-urllib.request) 用于从URL检索数据，以及 [`smtplib`](https://docs.python.org/zh-cn/3/library/smtplib.html#module-smtplib) 用于发送邮件

感觉用`requests`库就行了

### 10.8. 日期和时间

[`datetime`](https://docs.python.org/zh-cn/3/library/datetime.html#module-datetime) 模块提供了以简单和复杂的方式操作日期和时间的类。虽然支持日期和时间算法，但实现的重点是有效的成员提取以进行输出格式化和操作。该模块还支持可感知时区的对象。

```python
>>> from datetime import date
>>> now = date.today()
>>> now
datetime.date(2025, 1, 2)
>>> now.strftime("%m-%d-%y. %d %b %Y is a %A on the %d day of %B.")
'01-02-25. 02 Jan 2025 is a Thursday on the 02 day of January.'
>>> birthday = date(2000, 5, 9)
>>> age = now - birthday
>>> age.days
9004
```

### 10.9. 数据压缩

常见的数据存档和压缩格式由模块直接支持，包括：[`zlib`](https://docs.python.org/zh-cn/3/library/zlib.html#module-zlib), [`gzip`](https://docs.python.org/zh-cn/3/library/gzip.html#module-gzip), [`bz2`](https://docs.python.org/zh-cn/3/library/bz2.html#module-bz2), [`lzma`](https://docs.python.org/zh-cn/3/library/lzma.html#module-lzma), [`zipfile`](https://docs.python.org/zh-cn/3/library/zipfile.html#module-zipfile) 和 [`tarfile`](https://docs.python.org/zh-cn/3/library/tarfile.html#module-tarfile)。:

```python
>>> import zlib
>>> s = b"witch which has which witches wrist watch"
>>> len(s)
41
>>> t = zlib.compress(s)
>>> len(t)
37
>>> zlib.decompress(t)
b'witch which has which witches wrist watch'
>>> zlib.crc32(s)
226805979
```

### 10.10. 性能测量

一些Python用户对了解同一问题的不同方法的相对性能产生了浓厚的兴趣。 Python提供了一种可以立即回答这些问题的测量工具。

例如，元组封包和拆包功能相比传统的交换参数可能更具吸引力。[`timeit`](https://docs.python.org/zh-cn/3/library/timeit.html#module-timeit) 模块可以快速演示在运行效率方面一定的优势:

```python
>>> from timeit import Timer
>>> Timer('t=a; a=b; b=t', 'a=1;b=2').timeit()
0.007786237000004803
>>> Timer('a,b= b,a', 'a=1;b=2').timeit()# 结果完全没优势捏
0.00916625299998941
```

与 [`timeit`](https://docs.python.org/zh-cn/3/library/timeit.html#module-timeit) 的精细粒度级别相反， [`profile`](https://docs.python.org/zh-cn/3/library/profile.html#module-profile) 和 [`pstats`](https://docs.python.org/zh-cn/3/library/profile.html#module-pstats) 模块提供了用于在较大的代码块中识别时间关键部分的工具。

### 10.11. 质量控制

开发高质量软件的一种方法是在开发过程中为每个函数编写测试，并在开发过程中经常运行这些测试。

[`doctest`](https://docs.python.org/zh-cn/3/library/doctest.html#module-doctest) 模块提供了一个工具，用于扫描模块并验证程序文档字符串中嵌入的测试。测试构造就像将典型调用及其结果剪切并粘贴到文档字符串一样简单。这通过向用户提供示例来改进文档，并且它允许doctest模块确保代码保持对文档的真实:

```python
>>> def average(values):
...     """计算数字列表的算术平均值
...
...     >>> print(average([20, 30, 70]))
...     40.0
...     """
...     return sum(values) / len(values)
...
>>> import doctest
>>> doctest.testmod()
TestResults(failed=0, attempted=1)
```

[`unittest`](https://docs.python.org/zh-cn/3/library/unittest.html#module-unittest) 模块不像 [`doctest`](https://docs.python.org/zh-cn/3/library/doctest.html#module-doctest) 模块那样易于使用，但它允许在一个单独的文件中维护更全面的测试集:

```python
import unittest

class TestStatisticalFunctions(unittest.TestCase):

    def test_average(self):
        self.assertEqual(average([20, 30, 70]), 40.0)
        self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
        with self.assertRaises(ZeroDivisionError):
            average([])
        with self.assertRaises(TypeError):
            average(20, 30, 70)

unittest.main()  # 从命令行调用时会执行所有测试
```

### 10.12. 自带电池

Python有“自带电池”的理念。通过其包的复杂和强大功能可以最好地看到这一点。例如:

- [`xmlrpc.client`](https://docs.python.org/zh-cn/3/library/xmlrpc.client.html#module-xmlrpc.client) 和 [`xmlrpc.server`](https://docs.python.org/zh-cn/3/library/xmlrpc.server.html#module-xmlrpc.server) 模块使得实现远程过程调用变成了小菜一碟。 尽管存在于模块名称中，但用户不需要直接了解或处理 XML。
-  [`email`](https://docs.python.org/zh-cn/3/library/email.html#module-email) 包是一个用于管理电子邮件的库，包括MIME和其他符合 [**RFC 2822**](https://datatracker.ietf.org/doc/html/rfc2822.html) 规范的邮件文档。与 [`smtplib`](https://docs.python.org/zh-cn/3/library/smtplib.html#module-smtplib) 和 [`poplib`](https://docs.python.org/zh-cn/3/library/poplib.html#module-poplib) 不同（它们实际上做的是发送和接收消息），电子邮件包提供完整的工具集，用于构建或解码复杂的消息结构（包括附件）以及实现互联网编码和标头协议。
-  [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json) 包为解析这种流行的数据交换格式提供了强大的支持。 [`csv`](https://docs.python.org/zh-cn/3/library/csv.html#module-csv) 模块支持以逗号分隔值格式直接读取和写入文件，这种格式通常为数据库和电子表格所支持。 XML 处理由 [`xml.etree.ElementTree`](https://docs.python.org/zh-cn/3/library/xml.etree.elementtree.html#module-xml.etree.ElementTree) ， [`xml.dom`](https://docs.python.org/zh-cn/3/library/xml.dom.html#module-xml.dom) 和 [`xml.sax`](https://docs.python.org/zh-cn/3/library/xml.sax.html#module-xml.sax) 包支持。这些模块和软件包共同大大简化了 Python 应用程序和其他工具之间的数据交换。
-  [`sqlite3`](https://docs.python.org/zh-cn/3/library/sqlite3.html#module-sqlite3) 模块是 SQLite 数据库库的包装器，提供了一个可以使用稍微非标准的 SQL 语法更新和访问的持久数据库。
- 国际化由许多模块支持，包括 [`gettext`](https://docs.python.org/zh-cn/3/library/gettext.html#module-gettext) ， [`locale`](https://docs.python.org/zh-cn/3/library/locale.html#module-locale) ，以及 [`codecs`](https://docs.python.org/zh-cn/3/library/codecs.html#module-codecs) 包。

## 11. 标准库简介 —— 第二部分

第二部分涵盖了专业编程所需要的更高级的模块。这些模块很少用在小脚本中。

### 11.1. 格式化输出

[`reprlib`](https://docs.python.org/zh-cn/3/library/reprlib.html#module-reprlib) 模块提供了一个定制化版本的 [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr) 函数，用于缩略显示大型或深层嵌套的容器对象:

```python
>>> import reprlib
>>> reprlib.repr(set("supercalifragilisticexpialidocious"))
"{'a', 'c', 'd', 'e', 'f', 'g', ...}"
```

[`pprint`](https://docs.python.org/zh-cn/3/library/pprint.html#module-pprint) 模块提供了更加复杂的打印控制，其输出的内置对象和用户自定义对象能够被解释器直接读取。当输出结果过长而需要折行时，“美化输出机制”会添加换行符和缩进，以更清楚地展示数据结构:

```python
>>> import pprint
>>> t =  [[[['black', 'cyan'], 'white', ['green', 'red']], [['magenta','yellow'], 'blue']]]
>>> pprint.pprint(t, width=30)
[[[['black', 'cyan'],
   'white',
   ['green', 'red']],
  [['magenta', 'yellow'],
   'blue']]]
```

[`textwrap`](https://docs.python.org/zh-cn/3/library/textwrap.html#module-textwrap) 模块能够格式化文本段落，以适应给定的屏幕宽度:

```python
>>> import textwrap
>>> doc = """The wrap() method is just like fill() except that it returns a list of strings instead of one big string with newlines to separate the wrapped lines."""
>>> print(textwrap.fill(doc, width=40))
The wrap() method is just like fill()
except that it returns a list of strings
instead of one big string with newlines
to separate the wrapped lines.
```

[`locale`](https://docs.python.org/zh-cn/3/library/locale.html#module-locale) 模块处理与特定地域文化相关的数据格式。locale 模块的 format 函数包含一个 grouping 属性，可直接将数字格式化为带有组分隔符的样式:

```python
>>> conv = locale.localeconv()
>>> x = 1234567.8
>>> locale.format_string("%d", x, grouping=True)
'1234567'
>>> locale.format_string("%s%.*f", (conv['currency_symbol'],
... conv['frac_digits'], x), grouping=True)
'1234567.8000000000465661287307739257812500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000'
```

### 11.2. 模板

[`string`](https://docs.python.org/zh-cn/3/library/string.html#module-string) 模块包含一个通用的 [`Template`](https://docs.python.org/zh-cn/3/library/string.html#string.Template) 类，具有适用于最终用户的简化语法。它允许用户在不更改应用逻辑的情况下定制自己的应用。

上述格式化操作是通过占位符实现的，占位符由 `$` 加上合法的 Python 标识符（只能包含字母、数字和下划线）构成。一旦使用花括号将占位符括起来，就可以在后面直接跟上更多的字母和数字而无需空格分割。**`$$` 将被转义成单个字符 `$`**:

```python
>>> from string import Template
>>> t = Template("${village}folk send $$10 to $cause.")
>>> t.substitute(village='Nottingham', cause='the ditch fund')
'Nottinghamfolk send $10 to the ditch fund.'
```

如果在字典或关键字参数中未提供某个占位符的值，那么 [`substitute()`](https://docs.python.org/zh-cn/3/library/string.html#string.Template.substitute) 方法将抛出 [`KeyError`](https://docs.python.org/zh-cn/3/library/exceptions.html#KeyError)。对于邮件合并类型的应用，用户提供的数据有可能是不完整的，**此时使用 [`safe_substitute()`](https://docs.python.org/zh-cn/3/library/string.html#string.Template.safe_substitute) 方法更加合适 —— 如果数据缺失，它会直接将占位符原样保留。**

```python
>>> t = Template('Return the $item to $owner.')
>>> d = dict(item='unladen swallow')
>>> t.substitute(d)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/kevin/miniconda3/lib/python3.10/string.py", line 121, in substitute
    return self.pattern.sub(convert, self.template)
  File "/home/kevin/miniconda3/lib/python3.10/string.py", line 114, in convert
    return str(mapping[named])
KeyError: 'owner'
>>> t.safe_substitute(d)
'Return the unladen swallow to $owner.'
```

Template 的子类可以自定义分隔符。例如，以下是某个照片浏览器的批量重命名功能，采用了百分号作为日期、照片序号和照片格式的占位符:

```python
>>> import time, os.path
>>> photofiles = ['img_1074.jpg', 'img_1076.jpg', 'img_1077.jpg']
>>> class BatchRename(Template):
...     delimiter = '%'
...
>>> fmt = input('Enter rename style (%d-date %n-seqnum %f-format):  ')
Enter rename style (%d-date %n-seqnum %f-format):  Ashley_%n%f
>>> t = BatchRename(fmt)
>>> date = time.strftime('%d%b%y')
>>> for i, filename in enumerate(photofiles):
...     base, ext = os.path.splitext(filename)
...     newname = t.substitute(d=date, n=i, f=ext)
...     print('{0} --> {1}'.format(filename, newname))
...
img_1074.jpg --> Ashley_0.jpg
img_1076.jpg --> Ashley_1.jpg
img_1077.jpg --> Ashley_2.jpg
```

模板的另一个应用是将程序逻辑与多样的格式化输出细节分离开来。这使得对 XML 文件、纯文本报表和 HTML 网络报表使用自定义模板成为可能。

### 11.3. 使用二进制数据记录格式

[`struct`](https://docs.python.org/zh-cn/3/library/struct.html#module-struct) 模块提供了 [`pack()`](https://docs.python.org/zh-cn/3/library/struct.html#struct.pack) 和 [`unpack()`](https://docs.python.org/zh-cn/3/library/struct.html#struct.unpack) 函数，**用于处理不定长度的二进制记录格式**。下面的例子展示了在不使用 [`zipfile`](https://docs.python.org/zh-cn/3/library/zipfile.html#module-zipfile) 模块的情况下，如何循环遍历一个 ZIP 文件的所有头信息。Pack 代码 `"H"` 和 `"I"` 分别代表两字节和四字节无符号整数。`"<"` 代表它们是标准尺寸的小端字节序:

```python
import struct

with open('myfile.zip', 'rb') as f:
    data = f.read()

start = 0
for i in range(3):                      # 显示前 3 个文件标头
    start += 14
    fields = struct.unpack('<IIIHH', data[start:start+16])
    crc32, comp_size, uncomp_size, filenamesize, extra_size = fields

    start += 16
    filename = data[start:start+filenamesize]
    start += filenamesize
    extra = data[start:start+extra_size]
    print(filename, hex(crc32), comp_size, uncomp_size)

    start += extra_size + comp_size     # 跳过下一个标头
```

### 11.4. 多线程

线程是一种对于非顺序依赖的多个任务进行解耦的技术。多线程可以提高应用的响应效率，当接收用户输入的同时，保持其他任务在后台运行。一个有关的应用场景是，将 I/O 和计算运行在两个并行的线程中。

以下代码展示了高阶的 [`threading`](https://docs.python.org/zh-cn/3/library/threading.html#module-threading) 模块如何在后台运行任务，且不影响主程序的继续运行:

```python
import threading, zipfile

class AsyncZip(threading.Thread):
    def __init__(self, infile, outfile):
        threading.Thread.__init__(self)
        self.infile = infile
        self.outfile = outfile

    def run(self):
        f = zipfile.ZipFile(self.outfile, 'w', zipfile.ZIP_DEFLATED)
        f.write(self.infile)
        f.close()
        print('Finished background zip of:', self.infile)

background = AsyncZip('mydata.txt', 'myarchive.zip')
background.start()
print('The main program continues to run in foreground.')

background.join()    # 等待背景任务结束
print('Main program waited until background was done.')
```

多线程应用面临的主要挑战是，相互协调的多个线程之间需要共享数据或其他资源。为此，threading 模块提供了多个同步操作原语，包括线程锁、事件、条件变量和信号量。

尽管这些工具非常强大，但微小的设计错误却可以导致一些难以复现的问题。因此，实现多任务协作的首选方法是将所有对资源的请求集中到一个线程中，然后使用 [`queue`](https://docs.python.org/zh-cn/3/library/queue.html#module-queue) 模块向该线程供应来自其他线程的请求。 应用程序使用 [`Queue`](https://docs.python.org/zh-cn/3/library/queue.html#queue.Queue) 对象进行线程间通信和协调，更易于设计，更易读，更可靠。

### 11.5. 日志记录

[`logging`](https://docs.python.org/zh-cn/3/library/logging.html#module-logging) 模块提供功能齐全且灵活的日志记录系统。在最简单的情况下，日志消息被发送到文件或 `sys.stderr`

```python
>>> import logging
>>> logging.debug("Debugging information")
>>> logging.info("Informational message")
>>> logging.warning('Warning:config file %s not found', 'server.conf')
WARNING:root:Warning:config file server.conf not found
>>> logging.error('Error occurred')
ERROR:root:Error occurred
>>> logging.critical('Critical error -- shutting down')
CRITICAL:root:Critical error -- shutting down
```

**默认情况下，informational 和 debugging 消息被压制，输出会发送到标准错误流**。其他输出选项包括将消息转发到电子邮件，数据报，套接字或 HTTP 服务器。新的过滤器可以根据消息优先级选择不同的路由方式：[`DEBUG`](https://docs.python.org/zh-cn/3/library/logging.html#logging.DEBUG)，[`INFO`](https://docs.python.org/zh-cn/3/library/logging.html#logging.INFO)，[`WARNING`](https://docs.python.org/zh-cn/3/library/logging.html#logging.WARNING)，[`ERROR`](https://docs.python.org/zh-cn/3/library/logging.html#logging.ERROR)，和 [`CRITICAL`](https://docs.python.org/zh-cn/3/library/logging.html#logging.CRITICAL)。

日志系统可以直接从 Python 配置，也可以从用户配置文件加载，以便自定义日志记录而无需更改应用程序。

### 11.6. 弱引用

Python 会自动进行内存管理（对大多数对象进行引用计数并使用 [garbage collection](https://docs.python.org/zh-cn/3/glossary.html#term-garbage-collection) 来清除循环引用）。 当某个对象的最后一个引用被移除后不久就会释放其所占用的内存。

此方式对大多数应用来说都适用，但偶尔也必须在对象持续被其他对象所使用时跟踪它们。 不幸的是，跟踪它们将创建一个会令其永久化的引用。 [`weakref`](https://docs.python.org/zh-cn/3/library/weakref.html#module-weakref) 模块提供的工具可以不必创建引用就能跟踪对象。 当对象不再需要时，它将自动从一个弱引用表中被移除，并为弱引用对象触发一个回调。 典型应用包括对创建开销较大的对象进行缓存:

```python
>>> import weakref, gc
>>> class A:
...     def __init__(self, value):
...             self.value = value
...     def __repr__(self):
...             return str(self.value)
...
>>> a = A(10)
>>> d = weakref.WeakValueDictionary()
>>> d["primary"] = a
>>> d["primary"]
10
>>> del a
>>> gc.collect()
56
>>> d["primary"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/kevin/miniconda3/lib/python3.10/weakref.py", line 137, in __getitem__
    o = self.data[key]()
KeyError: 'primary'
```

### 11.7. 用于操作列表的工具

许多对于数据结构的需求可以通过内置列表类型来满足。 但是，有时也会需要具有不同效费比的替代实现。

[`array`](https://docs.python.org/zh-cn/3/library/array.html#module-array) 模块提供了一种 [`array`](https://docs.python.org/zh-cn/3/library/array.html#array.array) 对象，它类似于列表，但只能存储类型一致的数据且存储密度更高。 下面的例子显示了一个由存储为双字节无符号整数的数字 (类型码 `"H"`) 组成的元组，而不是常规 Python int 对象列表所采用的每个条目 16 字节:

```python
>>> from array import array
>>> a = array('H', [4000, 10, 700, 22222])
>>> sum(a)
26932
>>> a[1:3]
array('H', [10, 700])
```

[`collections`](https://docs.python.org/zh-cn/3/library/collections.html#module-collections) 模块提供了一种 [`deque`](https://docs.python.org/zh-cn/3/library/collections.html#collections.deque) 对象，它类似于列表，但从左端添加和弹出的速度较快而在中间查找的速度较慢。 此种对象适用于实现队列和广度优先树搜索:

```python
from collections import deque
d = deque(["task1", "task2", "task3"])
d.append("task4")
print("Handling", d.popleft())
Handling task1
unsearched = deque([starting_node])
def breadth_first_search(unsearched):
    node = unsearched.popleft()
    for m in gen_moves(node):
        if is_goal(m):
            return m
        unsearched.append(m)
```

在替代的列表实现以外，标准库也提供了其他工具，例如 [`bisect`](https://docs.python.org/zh-cn/3/library/bisect.html#module-bisect) 模块具有用于操作有序列表的函数:

```python
import bisect
scores = [(100, 'perl'), (200, 'tcl'), (400, 'lua'), (500, 'python')]
bisect.insort(scores, (300, 'ruby'))
scores
[(100, 'perl'), (200, 'tcl'), (300, 'ruby'), (400, 'lua'), (500, 'python')]
```

[`heapq`](https://docs.python.org/zh-cn/3/library/heapq.html#module-heapq) 模块提供了基于常规列表来实现堆的函数。 最小值的条目总是保持在位置零。 这对于需要重复访问最小元素而不希望运行完整列表排序的应用来说非常有用:

```python
from heapq import heapify, heappop, heappush
data = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
heapify(data)                      # 将列表重新调整为堆顺序
heappush(data, -5)                 # 添加一个新条目
[heappop(data) for i in range(3)]  # 获取三个最小的条目
[-5, 0, 1]
```

### 11.8. 十进制浮点运算

[`decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#module-decimal) 模块提供了一种 [`Decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#decimal.Decimal) 数据类型用于十进制浮点运算。 相比内置的 [`float`](https://docs.python.org/zh-cn/3/library/functions.html#float) 二进制浮点实现，该类特别适用于

- 财务应用和其他需要精确十进制表示的用途，
- 控制精度，
- 控制四舍五入以满足法律或监管要求，
- 跟踪有效小数位，或
- 用户期望结果与手工完成的计算相匹配的应用程序。

例如，使用十进制浮点和二进制浮点数计算70美分手机和5％税的总费用，会产生的不同结果。如果结果四舍五入到最接近的分数差异会更大:

```python
>>> from decimal import *
>>> round(Decimal('0.70') * Decimal('1.05'), 2)
Decimal('0.74')
>>> round(.70 * 1.05, 2)
0.73
```

[`Decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#decimal.Decimal) 表示的结果会保留尾部的零，并根据具有两个有效位的被乘数自动推出四个有效位。 Decimal 可以模拟手工运算来避免当二进制浮点数无法精确表示十进制数时会导致的问题。

精确表示特性使得 [`Decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#decimal.Decimal) 类能够执行对于二进制浮点数来说不适用的模运算和相等性检测:

```python
>>> Decimal('1.00') % Decimal('.10')
Decimal('0.00')
>>> 1.00 % 0.10
0.09999999999999995
>>> sum([Decimal('0.1')]*10) == Decimal('1.0')
True
>>> 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 == 1.0
False
```

[`decimal`](https://docs.python.org/zh-cn/3/library/decimal.html#module-decimal) 模块提供了运算所需要的足够精度:

```python
>>> getcontext().prec = 36
>>> Decimal(1) / Decimal(7)
Decimal('0.142857142857142857142857142857142857')
```

## 12. 虚拟环境和包

### 12.1. 概述

Python应用程序通常会使用不在标准库内的软件包和模块。应用程序有时需要特定版本的库，因为应用程序可能需要修复特定的错误，或者可以使用库的过时版本的接口编写应用程序。

这意味着一个Python安装可能无法满足每个应用程序的要求。如果应用程序A需要特定模块的1.0版本但应用程序B需要2.0版本，则需求存在冲突，安装版本1.0或2.0将导致某一个应用程序无法运行。

这个问题的解决方案是创建一个 [virtual environment](https://docs.python.org/zh-cn/3/glossary.html#term-virtual-environment)，一个目录树，其中安装有特定Python版本，以及许多其他包。

然后，不同的应用将可以使用不同的虚拟环境。 要解决先前需求相冲突的例子，应用程序 A 可以拥有自己的 安装了 1.0 版本的虚拟环境，而应用程序 B 则拥有安装了 2.0 版本的另一个虚拟环境。 如果应用程序 B 要求将某个库升级到 3.0 版本，也不会影响应用程序 A 的环境。

### 12.2. 创建虚拟环境

用于创建和管理虚拟环境的模块是 [`venv`](https://docs.python.org/zh-cn/3/library/venv.html#module-venv)。 [`venv`](https://docs.python.org/zh-cn/3/library/venv.html#module-venv) 将安装运行命令所使用的 Python 版本（即 [`--version`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-version) 选项所报告的版本）。 例如，使用 `python3.12` 执行命令将会安装 3.12 版。

要创建虚拟环境，请确定要放置它的目录，并将 [`venv`](https://docs.python.org/zh-cn/3/library/venv.html#module-venv) 模块作为脚本运行目录路径:

```python
# 在wsl中，必须先安装对应的包
kevin@Desktop:~$ python3 -m venv tutorial-env
The virtual environment was not created successfully because ensurepip is not
available.  On Debian/Ubuntu systems, you need to install the python3-venv
package using the following command.

    apt install python3.12-venv

You may need to use sudo with that command.  After installing the python3-venv
package, recreate your virtual environment.

Failing command: /home/kevin/tutorial-env/bin/python3
# 创建虚拟环境文件夹
python -m venv tutorial-env
# 激活虚拟环境
kevin@Desktop:~$ source tutorial-venv/bin/activate
(tutorial-venv) kevin@Desktop:~$
# 退出
(tutorial-venv) kevin@Desktop:~$ deactivate
kevin@Desktop:~$
```

### 12.3. 使用pip管理包

你可以使用一个名为 **pip** 的程序来安装、升级和移除软件包。 默认情况下 `pip` 将从 [Python Package Index](https://pypi.org/) 安装软件包。 你可以在你的 web 浏览器中查看 Python Package Index。

`pip` 有许多子命令: "install", "uninstall", "freeze" 等等。 （请在 [安装 Python 模块](https://docs.python.org/zh-cn/3/installing/index.html#installing-index) 指南页查看完整的 `pip` 文档。）

您可以通过指定包的名称来安装最新版本的包：

```python
(tutorial-venv) kevin@Desktop:~$ pip install novas
Collecting novas
  Downloading novas-3.1.1.6.tar.gz (141 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 141.1/141.1 kB 420.6 kB/s eta 0:00:00
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Building wheels for collected packages: novas
  Building wheel for novas (pyproject.toml) ... done
  Created wheel for novas: filename=novas-3.1.1.6-cp312-cp312-linux_x86_64.whl size=169296 sha256=b9748feabc913ad55d7668cafc34725bd753cede5ca47f11c2bf467986c29d24
  Stored in directory: /home/kevin/.cache/pip/wheels/24/5b/fe/e51d5145e5841ffb95a507accac76742cabd3998e86c948760
Successfully built novas
Installing collected packages: novas
Successfully installed novas-3.1.1.6
```

您还可以通过提供包名称后跟 `==` 和版本号来安装特定版本的包：

```python
(tutorial-venv) kevin@Desktop:~$ pip install requests==2.6.0
Collecting requests==2.6.0
  Downloading requests-2.6.0-py2.py3-none-any.whl.metadata (31 kB)
Downloading requests-2.6.0-py2.py3-none-any.whl (469 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 469.8/469.8 kB 683.2 kB/s eta 0:00:00
Installing collected packages: requests
Successfully installed requests-2.6.0
```

如果你重新运行这个命令，`pip` 会注意到已经安装了所请求的版本因而不做任何事。 你可以提供不同的版本号来获取相应版本，或者你可以运行 `python -m pip install --upgrade` 以将软件包升级到最新版本:

```python
(tutorial-venv) kevin@Desktop:~$ pip install --upgrade requests
Requirement already satisfied: requests in ./tutorial-venv/lib/python3.12/site-packages (2.6.0)
Collecting requests
  Downloading requests-2.32.3-py3-none-any.whl.metadata (4.6 kB)
Collecting charset-normalizer<4,>=2 (from requests)
  Downloading charset_normalizer-3.4.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (35 kB)
Collecting idna<4,>=2.5 (from requests)
  Downloading idna-3.10-py3-none-any.whl.metadata (10 kB)
Collecting urllib3<3,>=1.21.1 (from requests)
  Downloading urllib3-2.3.0-py3-none-any.whl.metadata (6.5 kB)
Collecting certifi>=2017.4.17 (from requests)
  Downloading certifi-2024.12.14-py3-none-any.whl.metadata (2.3 kB)
Downloading requests-2.32.3-py3-none-any.whl (64 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 64.9/64.9 kB 141.8 kB/s eta 0:00:00
Downloading certifi-2024.12.14-py3-none-any.whl (164 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 164.9/164.9 kB 173.7 kB/s eta 0:00:00
Downloading charset_normalizer-3.4.1-cp312-cp312-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (145 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 145.3/145.3 kB 160.2 kB/s eta 0:00:00
Downloading idna-3.10-py3-none-any.whl (70 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 70.4/70.4 kB 150.8 kB/s eta 0:00:00
Downloading urllib3-2.3.0-py3-none-any.whl (128 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 128.4/128.4 kB 174.7 kB/s eta 0:00:00
Installing collected packages: urllib3, idna, charset-normalizer, certifi, requests
  Attempting uninstall: requests
    Found existing installation: requests 2.6.0
    Uninstalling requests-2.6.0:
      Successfully uninstalled requests-2.6.0
Successfully installed certifi-2024.12.14 charset-normalizer-3.4.1 idna-3.10 requests-2.32.3 urllib3-2.3.0
```

`python -m pip uninstall` 后跟一个或多个要从虚拟环境中删除的包所对应的名称。

```python
(tutorial-venv) kevin@Desktop:~$ pip uninstall novas
Found existing installation: novas 3.1.1.6
Uninstalling novas-3.1.1.6:
  Would remove:
    /home/kevin/tutorial-venv/lib/python3.12/site-packages/novas-3.1.1.6.dist-info/*
    /home/kevin/tutorial-venv/lib/python3.12/site-packages/novas/*
Proceed (Y/n)? y
  Successfully uninstalled novas-3.1.1.6
```

`python -m pip show` 将显示有关某个特定包的信息:

```python
(tutorial-venv) kevin@Desktop:~$ pip show novas
Name: novas
Version: 3.1.1.6
Summary: The United States Naval Observatory NOVAS astronomy library
Home-page: http://www.usno.navy.mil/USNO/astronomical-applications/software-products/novas
Author: Eric G. Barron
Author-email: eric.barron@usno.navy.mil
License:
Location: /home/kevin/tutorial-venv/lib/python3.12/site-packages
Requires:
Required-by:
```

`python -m pip list` 将显示所有在虚拟环境中安装的包:

```python
(tutorial-venv) kevin@Desktop:~$ pip list
Package            Version
------------------ ----------
certifi            2024.12.14
charset-normalizer 3.4.1
idna               3.10
numpy              2.2.1
pip                24.0
requests           2.32.3
urllib3            2.3.0
```

`python -m pip freeze` 将产生一个类似的已安装包列表，但其输出会使用 `python -m pip install` 所期望的格式。 一个常见的约定是将此列表放在 `requirements.txt` 文件中:

```python
(tutorial-venv) kevin@Desktop:~$ pip freeze > requirements.txt
(tutorial-venv) kevin@Desktop:~$ ls
cuda-repo-wsl-ubuntu-12-4-local_12.4.0-1_amd64.deb  miniconda3        rofgmd.github.io  tutorial-env
kevin-web-server                                    requirements.txt  sam2              tutorial-venv
(tutorial-venv) kevin@Desktop:~$ cat requirements.txt
certifi==2024.12.14
charset-normalizer==3.4.1
idna==3.10
numpy==2.2.1
requests==2.32.3
urllib3==2.3.0
```

然后可以将 `requirements.txt` 提交给版本控制并作为应用程序的一部分提供。然后用户可以使用 `install -r` 安装所有必需的包：

```python
(tutorial-venv) kevin@Desktop:~$ pip install -r requirements.txt
Requirement already satisfied: certifi==2024.12.14 in ./tutorial-venv/lib/python3.12/site-packages (from -r requirements.txt (line 1)) (2024.12.14)
Requirement already satisfied: charset-normalizer==3.4.1 in ./tutorial-venv/lib/python3.12/site-packages (from -r requirements.txt (line 2)) (3.4.1)
Requirement already satisfied: idna==3.10 in ./tutorial-venv/lib/python3.12/site-packages (from -r requirements.txt (line 3)) (3.10)
Requirement already satisfied: numpy==2.2.1 in ./tutorial-venv/lib/python3.12/site-packages (from -r requirements.txt (line 4)) (2.2.1)
Requirement already satisfied: requests==2.32.3 in ./tutorial-venv/lib/python3.12/site-packages (from -r requirements.txt (line 5)) (2.32.3)
Requirement already satisfied: urllib3==2.3.0 in ./tutorial-venv/lib/python3.12/site-packages (from -r requirements.txt (line 6)) (2.3.0)
Collecting novas==3.1.1.3 (from -r requirements.txt (line 7))
  Downloading novas-3.1.1.3.tar.gz (136 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 136.6/136.6 kB 272.3 kB/s eta 0:00:00
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Building wheels for collected packages: novas
  Building wheel for novas (pyproject.toml) ... done
  Created wheel for novas: filename=novas-3.1.1.3-cp312-cp312-linux_x86_64.whl size=165495 sha256=97815c3a120ed05e0f1b01fcd04e0293bff6fed77c07c8a0abd29e5b99f22161
  Stored in directory: /home/kevin/.cache/pip/wheels/b9/2d/75/fa136fc888d1068a28bf6804ec8a0c24a59c5c7810f6c14b65
Successfully built novas
Installing collected packages: novas
```

## 13. 接下来？

阅读本教程可能会增强您对使用Python的兴趣 - 您应该热衷于应用Python来解决您的实际问题。你应该去哪里了解更多？

本教程是Python文档集的一部分。其他文档：

- [Python 标准库](https://docs.python.org/zh-cn/3/library/index.html#library-index):

  你应当浏览一下本手册，其中提供了有关标准库中的类型、函数和模块的完整（但简洁）的参考资料。 标准 Python 分发版包括 *许多* 附加代码。 这些模块可以完成读取 Unix 邮箱，通过 HTTP 获取文档，生成随机数，解析命令行选项，压缩数据以及许多其他任务。 浏览标准库参考将使你了解有哪些可用的功能。

- [安装 Python 模块](https://docs.python.org/zh-cn/3/installing/index.html#installing-index) 解释了怎么安装由其他Python开发者编写的模块。

- [Python 语言参考手册](https://docs.python.org/zh-cn/3/reference/index.html#reference-index): Python的语法和语义的详细解释。尽管阅读完非常繁重，但作为语言本身的完整指南是有用的。

更多Python资源：

- [https://www.python.org](https://www.python.org/): Python 主网站。 它包含代码、文档和指向全网 Python 相关网页的链接。
- [https://docs.python.org](https://docs.python.org/) ：快速访问Python的文档。
- [https://pypi.org](https://pypi.org/): The Python Package Index，以前也被昵称为 Cheese Shop [[1\]](https://docs.python.org/zh-cn/3/tutorial/whatnow.html#id2)，是可下载用户自制 Python 模块的索引。 当你要开始发布代码时，你可以在此处进行注册以便其他人能找到它。
- https://code.activestate.com/recipes/langs/python/ ：Python Cookbook是一个相当大的代码示例集，更多的模块和有用的脚本。特别值得一看的贡献收集在一本名为Python Cookbook（O'Reilly＆Associates，ISBN 0-596-00797-3）的书中。
- [https://pyvideo.org](https://pyvideo.org/) 收集了来自研讨会和用户组会议的 Python 相关视频的链接。
- [https://scipy.org](https://scipy.org/) ：Scientific Python 项目包含用于快速矩阵计算和操作的模块，以及用于诸如线性代数，傅里叶变换，非线性求解器，随机数分布，统计分析等的一系列包。

对于与Python相关的问题和问题报告，您可以发布到新闻组 *comp.lang.python* ，或者将它们发送到邮件列表python-[list@python.org](mailto:list@python.org)。新闻组和邮件列表是互通的，因此发布到一个地方将自动转发给另一个。每天有数百个帖子，询问（和回答）问题，建议新功能，以及宣布新模块。邮件列表档案可在 https://mail.python.org/pipermail/ 上找到。

在发问之前，请务必查看以下列表 [常见问题](https://docs.python.org/zh-cn/3/faq/index.html#faq-index) （或简写为 FAQ）。常见问题包含了很多一次又一次被提出的问题及其答案，所以可能已经包含了您的问题解决方案。

### 备注

[[1](https://docs.python.org/zh-cn/3/tutorial/whatnow.html#id1)]“Cheese Shop”是 Monty Python 的一个短剧：一位顾客来到一家奶酪商店，但无论他要哪种奶酪，店员都说没有货。

## 14. 交互式编辑和编辑历史

某些版本的 Python 解释器支持编辑当前输入行和编辑历史记录，类似 Korn shell 和 GNU Bash shell 的功能 。这个功能使用了 GNU Readline 来实现，一个支持多种编辑方式的库。这个库有它自己的文档，在这里我们就不重复说明了。

### 14.1. Tab 补全和编辑历史

在解释器启动的时候变量和模块名补全功能将 自动启用 以便在按下 Tab 键时发起调用补全函数；它会查找 Python 语句名称、当前局部变量和可用的模块名称。 对于带点号的表达式如 string.a，它会对该表达式最后一个 '.' 之前的部分求值然后根据结果对象的属性给出补全建议。 请注意如果具有 __getattr__() 方法的对象是该表达式的一部分这可能会执行应用程序定义的代码。 默认配置还会将你的编辑历史保存到你的用户目录下名为 .python_history 的文件。 该历史在下一次交互式解释器会话期间将继续可用。

## 15. 浮点算术：争议和限制

**请注意这种情况是二进制浮点数的本质特性：它不是 Python 的错误，也不是你代码中的错误。 你会在所有支持你的硬件中的浮点运算的语言中发现同样的情况（虽然某些语言在默认状态或所有输出模块下都不会 显示 这种差异）。**

二进制浮点运算会有许多这样令人惊讶的情况。 有关 "0.1" 的问题会在下面 "表示性错误" 一节中更精确详细地描述。 请参阅 Examples of Floating Point Problems 获取针对二进制浮点运算机制及在实践中各种常见问题的概要说明。 还可参阅 The Perils of Floating Point 获取其他常见意外现象的更完整介绍。

正如那篇文章的结尾所言，“对此问题并无简单的答案。” 但是也不必过于担心浮点数的问题！ Python 浮点运算中的错误是从浮点运算硬件继承而来，而在大多数机器上每次浮点运算得到的 2**53 数码位都会被作为 1 个整体来处理。 这对大多数任务来说都已足够，但你确实需要记住它并非十进制算术，且每次浮点运算都可能会导致新的舍入错误。

虽然病态的情况确实存在，但对于大多数正常的浮点运算使用来说，你只需简单地将最终显示的结果舍入为你期望的十进制数值即可得到你期望的结果。 str() 通常已足够，对于更精度的控制可参看 格式字符串语法 中 str.format() 方法的格式描述符。

对于需要精确十进制表示的使用场景，请尝试使用 decimal 模块，该模块实现了适合会计应用和高精度应用的十进制运算。

另一种形式的精确运算由 fractions 模块提供支持，该模块实现了基于有理数的算术运算（因此可以精确表示像 1/3 这样的数值）。

如果你是浮点运算的重度用户那么你应当了解一下 NumPy 包以及由 SciPy 项目所提供的许多其他数学和统计运算包。 参见 <https://scipy.org>。

## 16. 附录

当发生错误时，**解释器会打印错误消息和栈回溯**。 在交互模式下，将返回到主提示符；当输入是来自文件的时候，它将在打印栈回溯之后退出并附带一个非零的退出状态码。 （由 try 语句中 except 子句所处理的异常在此上下文中不属于错误。） 有些错误属于无条件致命错误，会导致程序附带非零状态码退出；这适用于内部一致性丧失以及某些内存耗尽的情况等。 所有错误消息都将被写入到标准错误流；来自被执行命令的正常输出测会被写入到标准输出。

将中断字符（通常为 Control-C 或 Delete ）键入主要或辅助提示符会取消输入并返回主提示符。 [1] 在执行命令时键入中断引发的 KeyboardInterrupt 异常，可以由 try 语句处理。

在 BSD 等类Unix系统上，Python 脚本可以像 shell 脚本一样直接执行，通过在第一行添加：

```python
#!/usr/bin/env python3
```

（假设解释器位于用户的 PATH ）脚本的开头，并将文件设置为可执行。 #! 必须是文件的前两个字符。在某些平台上，第一行必须以Unix样式的行结尾（'\n'）结束，而不是以Windows（'\r\n'）行结尾。注意，“散列字符”，或者说“磅字符”， '#' ，在Python中代表注释开始。

可以使用 chmod 命令为脚本提供可执行模式或权限。

```bash
chmod +x myscript.py
```