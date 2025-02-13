# Java学习

Java 是一种**编程语言**和**平台**。

Java 是一种高级、健壮、面向对象且安全的编程语言。

Java 是由*Sun Microsystems*（现为 Oracle 子公司）于 1995 年开发的。

James *Gosling*被称为 Java 之父。

**Java应用程序的类型**：

- 独立应用程序
  - 独立应用程序也称为桌面应用程序或基于窗口的应用程序。
  - 这些是我们需要在每台机器上安装的传统软件。
  - 独立应用程序的示例包括媒体播放器、防病毒软件等。
  - Java 中使用 **AWT** 和 **Swing** 来创建独立应用程序。
- Web应用程序
  - 在服务器端运行并创建动态页面的应用程序称为 Web 应用程序。
  - 目前，使用 Java 创建 Web 应用程序的技术有**Servlet、JSP、Struts、Spring、Hibernate、JSF**等。
- 企业应用
  - 本质上分布式的应用程序（例如银行应用程序等）称为企业应用程序。
  - 它具有高级别安全性、负载平衡和集群等优势。
  - 在 Java 中，**EJB**用于创建企业应用程序。
- 移动应用程序
  - 为移动设备创建的应用程序称为移动应用程序。
  - 目前，**Android** 和 **Java ME** 用于创建移动应用程序。

**Java平台 / 版本**

- Java SE（Java标准版）
  - 它是一个 Java 编程平台。
  - 它包括 Java 编程 API，例如 java.lang、java.io、java.net、java.util、java.sql、java.math 等。
  - 它包括核心主题，例如 OOP、String、Regex、Exception、内部类、多线程、I/O 流、网络、AWT、Swing、Reflection、Collection 等。
- Java EE（Java企业版）
  - 它是一个企业平台，主要用于开发 Web 和企业应用程序。
  - 它建立在 Java SE 平台之上。它包括 Servlet、JSP、Web 服务、EJB、JPA等主题。
- Java ME（Java微型版本）
  - 它是一个专用于移动应用程序的微平台。
- JavaFX
  - 它用于开发丰富的互联网应用程序。
  - 它使用轻量级用户界面 API。

## 1.Java基础

### 什么是OOP?

OOP 代表**面向对象编程**。

### 包

Java 中的包用于对相关类进行分组。

### 八种基本数据类型

- `byte`
- `short`
- `int`
- `long`
- `float`
- `double`
- `boolean`
- `char`

### 类型转换

隐式类型转换：（小转大）

当两种数据类型彼此兼容，并且目标类型的取值范围大于源类型时，会发生自动类型转换。

强制类型转换：（大转小）

这种转换可能会导致数据丢失或精度降低。

自动装箱：

基本数据类型向包装类型转换。

自动拆箱：

包装类型向基本数据类型转换。

### 运算符

- 算术运算符： `+`、`_`、`*`、`/`、`%`、`++`、`--` 
- 赋值运算符：`=`、`+=`、`-=`
- 比较运算符：`>`、`<`、`==`、`!=`、`>=`、`<=`
- 逻辑运算符：`&&`、`||`、`!`

### 数组

用**方括号**声明数组。

**遍历数组**

用`for`循环和数组下标来遍历数组。

或者，用For-Each循环遍历数组。

```java
for (type variable : arrayname) {
  ...
}
```

### 访问修饰符

- `public`
- `private`
- `protected` 同包可访问；子类继承父类时，子类可访问
- `default` 包访问权限

### 非访问修饰符

- `final`
- `static`
- `abstract`
- `transient`
- `synchronized`
- `volatile`

### 条件语句

`if`

```java
if (condition) {
  // block of code to be executed if the condition is true
} else {
  // block of code to be executed if the condition is false
}
```

`switch`

```java
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

### 循环

`for`

```java
for (statement 1; statement 2; statement 3) {
  // code block to be executed
}
```

`whlie`

```java
while (condition) {
  // code block to be executed
}
```

`do/while`

```java
do {
  // code block to be executed
}
while (condition);
```

`break`和`continue`

## 2.类

类是对象的模板，而对象是类的实例。

类具有**属性**和**方法**。

创建对象：`new`关键字。

访问属性：语法（`.`）来访问属性。

### 类的封装

确保敏感数据对用户隐藏

- 将属性声明为`private`
- 提供公共的get和set方法来获取和更新成员变量的值

### 继承

子类 `extend` 超类

**用`final`修饰的类，不能被其他类继承**

java不支持多继承，但可以实现多个接口。

### 多态

继承发生时，也会出现多态性，这种多态表现为子类重写了父类的方法，表现出了不一样的特性

### 抽象

`abstract`关键字

修饰类，不能创建对象，可以通过子类继承来访问。

修饰方法，只能在抽象类中使用抽象方法，没有方法体，其方法由继承的子类提供。

抽象类可以同时拥有抽象方法和常规方法。

### 接口

实现抽象的另一种方法。

`interface`

完全的抽象类。

要访问接口方法，必须由另一个类实现`implements`接口。

### 枚举

一个特殊的类，代表了一组常量，类似final修饰的变量。

有自己的关键字`enum`而不是`class`

搭配`switch`使用

枚举有一个`values()`方法，它返回所有枚举值的数组，常常用于遍历。

## 3.变量

- 成员变量：定义在类的内部，方法的外部的变量。
- 局部变量：定义在方法、构造方法或者语句块内部的变量。
- 静态变量：用`static`修饰符修饰的变量。它属于类本身，而非类的某个实例。
- 常量：用`final`修饰符修饰的变量，其值，在初始化后不能修改。

## 4.方法

### 方法重载

同一个类中，方法名相同，参数、返回值不同。

是java中实现多态性的一种方式。

### 方法重写

子类继承父类的时候，方法名、参数和返回值都必须与父类相同，且修饰符不能比父类更严格。

也是java中实现多态性的一种方式。

### 递归

方法自己调用自己。

## 5.集合框架

框架：指提供了现成的类和接口的结构，可高效构建软件应用程序。

![](C:\Users\Rain7\Desktop\笔记md\javapic\jihekj.png)

### List

`List`接口代表一个有序的集合，元素可以重复。

### Queue

`Queue`接口代表一个队列，遵循先进先出（FIFO）的原则。

### Set

`Set`接口代表一个不包含重复元素的集合。

### ArrayList

用动态数组来存储不同数据类型的重复元素

**查询速度快**

### LinkedList

使用双向链表来存储元素

**操作速度快**

### Map

`Map`接口用于存储键 - 值（key - value）对。

![](C:\Users\Rain7\Desktop\笔记md\javapic\jhkjmap.png)

### HashMap

在 Java 8 之前，HashMap 内部主要是基于数组和链表实现的。

从 Java 8 开始，当链表的长度超过一定阈值（默认为 8），并且数组的长度大于等于 64 时，链表会转换为红黑树。以提高查找效率。

这种结构结合了数组的快速访问特性和链表（或红黑树）处理冲突的能力。

**哈希冲突**

哈希冲突（Hash Collision）是指在哈希表（Hash Table）中，不同的键（Key）通过哈希函数（Hash Function）计算得到了相同的哈希值（Hash Value），导致这些键在哈希表中的存储位置发生冲突的现象。

链地址法：

当两个不同的键具有相同的哈希值时，HashMap 将使用不同的链接来处理哈希冲突，将多个条目存储在同一个存储桶中并保留条目的链接列表。

这种方法的优点是实现简单，并且可以高效地处理冲突，对哈希函数的要求相对较低。

### TreeMap

TreeMap 是一个有序的键 - 值（key - value）存储容器，它会根据键的自然顺序或者自定义的比较器（Comparator）来对键进行排序。

TreeMap 的底层是基于红黑树（Red - Black Tree）实现的。

## 6.数据结构

### 数组

数组是一种简单而基础的数据结构，它是一组相同类型的数据元素的有序集合。

这些元素在内存中是连续存储的，通过一个索引（下标）来访问各个元素，索引从 0 开始。

**适用**于数据元素数量固定或者变化不大，且需要频繁访问元素的情况。例如，存储矩阵、图像的像素点、学生成绩表等。在这些场景中，数据的顺序和位置通常比较重要，而且访问特定位置的元素是主要操作。

### 链表

链表是由一系列节点（Node）组成的数据结构。

每个节点包含两部分：数据域（用于存储数据）和指针域（用于指向下一个节点）。

链表中的节点在内存中不一定是连续存储的，通过指针将各个节点连接起来。

**适用**于数据元素的插入和删除操作频繁的场景。例如，实现栈和队列（链式栈和链式队列）、动态内存分配（操作系统中的内存管理链表）、图的邻接表表示法等。在这些场景中，数据元素的数量可能经常变化，链表的灵活性可以更好地适应这种变化。

### 双向链表

它由一系列节点（Node）组成。

与单向链表不同的是，双向链表中的每个节点包含三个部分：

数据域（用于存储数据）、指向前一个节点的指针（prev）和指向后一个节点的指针（next）。

这种结构使得链表可以在两个方向上进行遍历。

### 红黑树

红黑树是一种自平衡的二叉查找树。

它在每个节点上增加了一个存储位来表示节点的颜色（红色或黑色），通过一系列的规则来保证树的平衡性。

这些规则包括：

- 每个节点要么是红色，要么是黑色；

- 根节点是黑色；

- 每个叶子节点（空节点）是黑色；

- 如果一个节点是红色的，则它的子节点必须是黑色；

- 从一个节点到该节点的子孙叶子节点的所有路径上包含相同数目的黑色节点。

红黑树在需要高效地进行查找、插入和删除操作，并且要求数据保持一定的顺序的场景中非常有用。

例如，在 Java 的`TreeMap`和`TreeSet`集合类中，底层数据结构就是红黑树，用于存储键 - 值对或者元素集合，并且能够保证元素按照一定的顺序排列，方便快速查找和范围查询。

## 7.反射

**反射：将类的属性和方法映射成相应的类。**

### 反射基本使用

获取 Class 类的三种方法:

- ClassName.class
- ObjectName.getClass ()
- Class.forName ("ClassName")

接下来的流程是:

- 用上述三种方式之一获取特定类的 `Class` 类
- 调用 `Class` 对象的 `getConstructor(Class<?>... parameterTypes)` **获取构造方法对象**
- 调用构造方法类 `Constructor` 的 `newInstance(Object... initargs)` **新建对象**
- 调用 `Class` 对象的 `getMethod(String name, Class<?>... parameterTypes)` **获取方法对象**
- 调用方法对象 `Method` 的 `invoke(Object obj, Object... args)` ，**调用对象上相应方法**

## 8.函数式接口

Lambda 表达式通常与函数式接口一起使用。Java 8 提供了许多内置的函数式接口，例如：

- `Runnable`: 无参数，无返回值。

  - **作用**：`Runnable` 接口表示一个可执行的任务，它没有参数，也没有返回值。通常用于创建线程，当线程启动时会执行 `run` 方法中的代码逻辑。

  - ```java
    // 传统方式：匿名内部类
    Runnable r1 = new Runnable() {
        @Override
        public void run() {
            System.out.println("Hello, World!");
        }
    };
    
    // Lambda 表达式
    Runnable r2 = () -> System.out.println("Hello, World!");
    
    r1.run(); // 输出: Hello, World!
    r2.run(); // 输出: Hello, World!
    ```

- `Consumer<T>`: 接受一个参数，无返回值。

  - **作用**：`Consumer<T>` 接口表示接受一个输入参数 `T`，并且不返回任何结果的操作。它通常用于对输入的数据进行消费处理，比如打印、存储等。

  - ```java
    // 传统方式：匿名内部类
    Consumer<String> c1 = new Consumer<String>() {
        @Override
        public void accept(String s) {
            System.out.println(s);
        }
    };
    
    // Lambda 表达式
    Consumer<String> c2 = s -> System.out.println(s);
    
    c1.accept("Hello"); // 输出: Hello
    c2.accept("World"); // 输出: World
    ```

- `Supplier<T>`: 无参数，返回一个值。

  - **作用**：`Supplier<T>` 接口表示一个供应商，不接受任何参数，但会返回一个类型为 `T` 的结果。常用于需要获取某个对象实例的场景，例如生成随机数、创建新对象等。

- `Function<T, R>`: 接受一个参数，返回一个值。

  - **作用**：`Function<T, R>` 接口表示接受一个类型为 `T` 的输入参数，并返回一个类型为 `R` 的结果。它常用于对输入数据进行转换处理，例如将字符串转换为整数、将对象转换为另一种对象等。

  - ```java
    // 传统方式：匿名内部类
    Function<Integer, String> f1 = new Function<Integer, String>() {
        @Override
        public String apply(Integer num) {
            return "Number: " + num;
        }
    };
    
    // Lambda 表达式
    Function<Integer, String> f2 = num -> "Number: " + num;
    
    System.out.println(f1.apply(10)); // 输出: Number: 10
    System.out.println(f2.apply(20)); // 输出: Number: 20
    ```

- `Predicate<T>`: 接受一个参数，返回布尔值。

  - **作用**：`Predicate<T>` 接口表示接受一个类型为 `T` 的输入参数，并返回一个布尔值。它常用于对输入数据进行条件判断，例如筛选列表中的元素、验证数据的有效性等。

  - ```java
    // 传统方式：匿名内部类
    Predicate<Integer> p1 = new Predicate<Integer>() {
        @Override
        public boolean test(Integer num) {
            return num > 0;
        }
    };
    
    // Lambda 表达式
    Predicate<Integer> p2 = num -> num > 0;
    
    System.out.println(p1.test(10)); // 输出: true
    System.out.println(p2.test(-5)); // 输出: false
    ```

多参数lambda表达式

```java
// 传统方式：匿名内部类
BiFunction<Integer, Integer, Integer> add1 = new BiFunction<Integer, Integer, Integer>() {
    @Override
    public Integer apply(Integer a, Integer b) {
        return a + b;
    }
};

// Lambda 表达式
BiFunction<Integer, Integer, Integer> add2 = (a, b) -> a + b;

System.out.println(add1.apply(5, 3)); // 输出: 8
System.out.println(add2.apply(10, 20)); // 输出: 30
```

