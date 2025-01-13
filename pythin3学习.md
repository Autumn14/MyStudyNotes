# Python3 学习

## 1.下载安装

去官网下载安装包

然后点击安装就好，记得勾选添加到环境变量

## 2.开发工具

软件  vscode

插件  python

插件  Fitten Code  

注：第三个是AI编程助手，可以使用微信登录

## 3.基本语法

### 编码

默认情况下，Python 3 源码文件以 **UTF-8** 编码，所有字符串都是 unicode 字符串。 

当然你也可以为源码文件指定不同的编码：

```python
# -*- coding: cp-1252 -*-
```

### 标识符

- 第一个字符必须是字母表中字母或下划线 **_** 。
- 标识符的其他的部分由字母、数字和下划线组成。
- 标识符对大小写敏感。

在 Python 3 中，可以用中文作为变量名，非 ASCII 标识符也是允许的了。

### python保留字

保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字：

```python
# 输出python保留字
import keyword
keyword.kwlist
print(keyword.kwlist)
```

### 注释

Python中单行注释以 **#** 开头

### 行与缩进

python最具特色的就是使用缩进来表示代码块，不需要使用大括号 **{}** 。

缩进的空格数是可变的，但是同一个代码块的语句必须包含相同的缩进空格数。

### 多行语句

Python 通常是一行写完一条语句，但如果语句很长，我们可以使用反斜杠 `\` 来实现多行语句

### 数字类型

python中数字有四种类型：整数、布尔型、浮点数和复数。

- **int** (整数), 如 1, 只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。
- **bool** (布尔), 如 True。
- **float** (浮点数), 如 1.23、3E-2
- **complex** (复数) - 复数由实部和虚部组成，形式为 a + bj，其中 a 是实部，b 是虚部，j 表示虚数单位。如 1 + 2j、 1.1 + 2.2j

### 字符串

- Python 中单引号 **'** 和双引号 **"** 使用完全相同。
- 使用三引号(**'''** 或 **"""**)可以指定一个多行字符串。
- 转义符 **\**。
- 反斜杠可以用来转义，使用 **r** 可以让反斜杠不发生转义。 如 **r"this is a line with \n"** 则 **\n** 会显示，并不是换行。
- 按字面意义级联字符串，如 **"this " "is " "string"** 会被自动转换为 **this is string**。
- 字符串可以用 **+** 运算符连接在一起，用 ***** 运算符重复。
- Python 中的字符串有两种索引方式，从左往右以 **0** 开始，从右往左以 **-1** 开始。
- Python 中的字符串不能改变。
- Python 没有单独的字符类型，一个字符就是长度为 1 的字符串。
- 字符串切片 **str[start:end]**，其中 start（包含）是切片开始的索引，end（不包含）是切片结束的索引。
- 字符串的切片可以加上步长参数 step，语法格式如下：`str[start:end:step]`

### 空行

函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。

类和函数入口之间也用一行空行分隔，以突出函数入口的开始。

空行与代码缩进不同，空行并不是 Python 语法的一部分。书写时不插入空行，Python 解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。

**记住：**空行也是程序代码的一部分。

### 等待用户输入

执行下面的程序在按回车键后就会等待用户输入：

```python
#!/usr/bin/python3
 
input("\n\n按下 enter 键后退出。")
```

以上代码中 ，**\n\n** 在结果输出前会输出两个新的空行。一旦用户按下 **enter** 键时，程序将退出。

### 同一行显示多条语句

Python 可以在同一行中使用多条语句，语句之间使用分号 **;** 分割，以下是一个简单的实例：

```python
#!/usr/bin/python3
 
import sys; x = 'hello'; sys.stdout.write(x + '\n')
```

### 多个语句构成代码组

像if、while、def和class这样的复合语句，首行以关键字开始，以冒号( : )结束，该行之后的一行或多行代码构成代码组。

我们将首行及后面的代码组称为一个子句(clause)。

如下实例：

```python
if expression : 
   suite
elif expression : 
   suite 
else : 
   suite
```

### print 输出

**print** 默认输出是换行的，如果要实现不换行需要在变量末尾加上 **end=""**：

### import与from…import

在 python 用 `import` 或者 `from...import` 来导入相应的模块。

将整个模块(somemodule)导入，格式为： `import somemodule`

从某个模块中导入某个函数,格式为： `from somemodule import somefunction`

从某个模块中导入多个函数,格式为： `from somemodule import firstfunc, secondfunc, thirdfunc`

将某个模块中的全部函数导入，格式为： `from somemodule import \*`

### 命令行参数

`python -h`

## 4.基本数据类型

Python 中的变量不需要声明。

每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。

在 Python 中，变量就是变量，它没有类型，我们所说的"类型"是变量所指的内存中对象的类型。

等号（=）用来给变量赋值。

等号（=）运算符左边是一个变量名,等号（=）运算符右边是存储在变量中的值。

### 多个变量赋值

Python允许你同时为多个变量赋值。

```python
a = b = c = 1
```

```python
a, b, c = 1, 2, "python"
```

### 标准数据类型

Python3 中常见的数据类型有：

- Number（数字）
- String（字符串）
- bool（布尔类型）
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）

Python3 的六个标准数据类型中：

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

此外还有一些高级的数据类型，如: 字节数组类型(bytes)。

### Number（数字）

Python3 支持 **int、float、bool、complex（复数）**。

在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。

内置的 type() 函数可以用来查询变量所指的对象类型。

isinstance 和 type 的区别在于：

- type()不会认为子类是一种父类类型。
- isinstance()会认为子类是一种父类类型。

```python
a,b,c = 20, 2.2, true
print(type(a),type(b),type(c))
isinstance(a, int)
```

**注意：**Python3 中，bool 是 int 的子类，True 和 False 可以和数字相加，**True==1、False==0** *会返回* **True**，但可以通过`is` *来判断类型。*

当你指定一个值时，Number 对象就会被创建

您也可以使用del语句删除一些对象引用。
