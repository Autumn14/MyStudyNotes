# CSS学习

CSS（层叠样式表）是一种用于控制网页文档外观和布局的标记语言。

它具有一套基本的语法规则，例如通过选择器来定位 HTML 元素，然后使用属性和值来定义元素的样式

CSS 是我们用来设计网页样式的语言

## 1.CSS语法

CSS 规则由选择器和声明块组成

选择器指向您想要设置样式的 HTML 元素

声明块包含一个或多个用分号分隔的声明

每个声明都包含一个 CSS 属性名称和一个值，以冒号分隔

多个CSS声明之间以分号分隔

声明块之间用花括号括起来

`h1 {color:blue; font-size:12px;}`

## 2.CSS选择器

CSS 选择器用于“查找”（或选择）您想要设置样式的 HTML 元素。

我们可以将 CSS 选择器分为五类：

- 简单选择器（根据名称、ID、类选择元素）
- 组合选择器（根据元素之间的特定关系选择元素）
- 伪类选择器（根据特定状态选择元素）
- 伪元素选择器（选择元素的一部分并设置其样式）
- 属性选择器（根据属性或属性值选择元素）

**元素选择器：**

元素选择器根据元素名称选择 HTML 元素

**id 选择器：**

id 选择器使用 HTML 元素的 id 属性来选择特定元素

元素的 id 在页面内是唯一的，因此 id 选择器用于选择一个唯一的元素！

要选择具有特定 id 的元素，请写入井号 (#) 字符，后跟元素的 id

**注意：** id名称不能以数字开头！

**类选择器：**

类选择器选择具有特定类属性的 HTML 元素

要选择具有特定类的元素，请写一个句点 (.) 字符，后跟类名

还可以指定只有特定的 HTML 元素才会受到类的影响：

`p.center{}`  选择，带有` class="center"` 的 `<p>` 元素

HTML 元素也可以引用多个类：

`<p class="center large"></p>`

**注意：**class名称不能以数字开头！

**通用选择器：**

通用选择器 (*) 选择页面上的所有 HTML 元素

**分组选择器：**

分组选择器选择所有具有相同样式定义的 HTML 元素

`h1, h2, p {}`

最好对选择器进行分组，以最小化代码

要对选择器进行分组，请用逗号分隔每个选择器

**上面5个都是简单选择器**

## 3.添加CSS

**外部CSS：**

使用外部样式表，只需更改一个文件即可改变整个网站的外观！

每个 HTML 页面都必须在头部部分的 `<link> `元素内包含对外部样式表文件的引用

`<link rel="stylesheet" href="mystyle.css">`

外部.css 文件不应包含任何 HTML 标签

**内部CSS：**

如果单个 HTML 页面具有独特的样式，则可以使用内部样式表

内部样式在 HTML 页面的 `<head>` 部分内的 `<style>` 元素中定义

**内联 CSS：**

内联样式可用于为单个元素应用独特的样式

要使用内联样式，请将 style 属性添加到相关元素

style 属性可以包含任何 CSS 属性

**多个样式表，执行顺序**

如果在不同的样式表中为相同的选择器（元素）定义了一些属性，则将使用最后读取的样式表中的值，**代码写的顺序（link标签和style标签的前后顺序，后面的生效）**

当为 HTML 元素指定多种样式时，将使用哪种样式？

页面中的所有样式将按照以下规则“级联”到一个新的“虚拟”样式表中，其中数字 1 具有最高优先级：

1. 内联样式（HTML 元素内）
2. 外部和内部样式表（位于头部）
3. 浏览器默认

因此，内联样式具有最高优先级，并将覆盖外部和内部样式以及浏览器默认设置

## 4.CSS注释

CSS 注释位于`<style>`元素内部，`/* */` 

可以在代码中的任意位置添加注释

## 5.CSS颜色

颜色使用预定义的颜色名称或 RGB、HEX、HSL、RGBA、HSLA 值指定

例如，Tomato颜色，以下表示

**rgb(255, 99, 71)**

**#ff6347**

**hsl(9, 100%, 64%)** 色轮上的度数 饱和度 亮度

**rgba(255, 99, 71, 0.5)** 后面是透明度

**hsla(9, 100%, 64%, 0.5)** 后面是透明度

HEX 十六进制颜色 ：

  十六进制颜色用#RRGGBB 指定，其中 RR（红色）、GG（绿色）和 BB（蓝色）十六进制整数指定颜色的组成部分

HSL 值：

  hsl(*色调*，*饱和度*，*亮度*)

## 6.CSS背景

- `background-color: lightblue;` 背景颜色
- `opacity: 0.3;` 透明度 0.0 ~ 1.0 （1.0为不透明，值越小，越透明）
- `background-image: url("bkimg.jpg")` 背景图片
- `background-repeat: repeat-x;`

默认情况下，该`background-image`属性会在水平和垂直方向上重复图像

但有些图像应该只水平或垂直重复，否则它们会看起来很奇怪

属性值：`repeat-x` `repest-y` `no-repeat`

- `background-position: right top;`指定背景图像的位置，右上角

- `background-attachment: fixed;`指定背景图像是否应滚动或固定，`fixed`固定的，`scroll`滚动的
- `background: lightblue url(bkimg.jpg) no-repeat right top` 简写

使用简写属性时，属性值的顺序为：

- `background-color`
- `background-image`
- `background-repeat`
- `background-attachment`
- `background-position`

## 7.CSS边框

该`border-style`属性指定显示什么类型的边框

**边界**

允许使用以下值：

- `dotted`- 定义虚线边框
- `dashed`- 定义虚线边框
- `solid`- 定义实线边框
- `double`- 定义双边框
- `groove`- 定义 3D 凹槽边框。效果取决于边框颜色值
- `ridge`- 定义 3D 脊状边框。效果取决于边框颜色值
- `inset`- 定义 3D 插入边框。效果取决于边框颜色值
- `outset`- 定义 3D 起始边框。效果取决于边框颜色值
- `none`- 无边界定义
- `hidden`- 定义隐藏边框

`border-style`属性可以有一到四个值（分别表示上边框、右边框、下边框和左边框）

可以这样写：`border-style: dotted dashed solid double;`

**边框宽度**

`border-width`属性指定四个边框的宽度

宽度可以设置为特定尺寸（以 px、pt、cm、em 等为单位），或者使用三个预定义值之一：`thin`细、`medium`中 、`thick`粗

`border-width` 属性可以有一到四个值（分别表示上边框、右边框、下边框和左边框）

上、右、下、左

逆时针

**边框颜色**

`border-color`属性用于设置四个边框的颜色，也可以是四个值，同边框宽度

**单边属性**

`border-top-style: dotted;`
`border-right-style: solid;`
`border-bottom-style: dotted;`
`border-left-style: solid;`

四个属性值：上、右、下、左

三个属性值：上、左右、下

两个属性值：上下、左右

一个属性值：四边

**简写**

`border`属性是以下各个边框属性的简写属性：

- `border-width`
- `border-style`（必需的）
- `border-color`

`border: 5px solid red;`

单边属性：`border-left: 6px solid red;`

**圆角边框**

`border-radius: 5px;`

## 8.CSS边距

CSS 具有用于指定元素每边边距的属性：

- `margin-top`
- `margin-right`
- `margin-bottom`
- `margin-left`

所有边距属性均可具有以下值：

- 自动 - 浏览器计算边距
- *长度*- 指定边距，单位为 px、pt、cm 等。
- *%* - 指定包含元素宽度的百分比边距
- inherit - 指定边距应从父元素继承

**提示：**允许使用负值

四个属性值：上、右、下、左

三个属性值：上、左右、下

两个属性值：上下、左右

一个属性值：四边

属性值：`auto` 使元素在其容器内水平居中

属性值：`inherit` 边距从父元素继承

**边距折叠：**

元素的顶部和底部边距有时会折叠为一个边距，该边距等于两个边距中的最大边距

左右边距不会发生这种情况！只有顶部和底部边距才会发生这种情况！

## 9.CSS填充

填充用于在任何定义的边框内围绕元素内容创建空间

可以理解为，`margin`是外边距，`padding`是内边距

CSS 具有用于指定元素每侧填充的属性：

- `padding-top`
- `padding-right`
- `padding-bottom`
- `padding-left`

属性值和`margin`类似

**`padding`和`width`**

CSS如果同时指定了`width`宽度和`padding`内边距，那么元素的实际宽度是指定的宽度加上左右内边距的宽度总和

`box-sizing`属性:

指定`box-sizing`属性，导致元素保持指定宽度`width`，如果同时设置了内边距`padding`，那么可用的内部空间将变小

`box-sizing: border-box;`

## 10.CSS宽度和高度

`height`和属性`width`用于设置元素的高度和宽度

高度和宽度属性不包括填充、边框或边距

`height`和属性`width`具有以下值：

- `auto`- 这是默认设置。浏览器计算高度和宽度
- `length`- 以 px、cm 等为单位定义高度/宽度。
- `%`- 定义包含块的高度/宽度百分比
- `initial`- 将高度/宽度设置为默认值
- `inherit`- 高度/宽度将从其父值继承

**最大宽度**

`max-width`

默认值是无，意味着没有最大宽度

设置最大宽度的意思是，如果浏览器的窗口小于这个设定值的时候，会出现一个水平滚动条

同理，还有`min-width`、`max-height`和`min-height`属性

## 11.盒子模型

盒子模型本质上是一个包围每个 HTML 元素的盒子

它由内容、填充、边框和边距组成

![](C:\Users\Rain7\Desktop\笔记md\图片\hzmd.png)

不同部分的说明：

- **内容**- 框的内容，其中显示文本和图像
- **填充**- 清除内容周围的区域。填充是透明的。
- **边框**- 围绕填充和内容的边框
- **边距**- 清除边框外的区域。边距是透明的。

**计算元素的宽度和高度**

**重要提示：**

使用 CSS 设置元素的宽度和高度属性时，

`width`和`height`只设置**内容区域**的宽度和高度。

要计算元素的总宽度和高度，还必须包括填充和边框。

元素的**总宽度**按如下方式计算：**不算margin**

元素总宽度 = 宽度 + 左内边距 + 右内边距 + 左边框 + 右边框

元素的**总高度**按如下方式计算：**不算margin**

元素总高度 = 高度 + 顶部填充 + 底部填充 + 顶部边框 + 底部边框

**注意：**边距属性也会影响框在页面上占用的总空间，但边距不包含在框的实际大小中。框的总宽度和高度止于边框。

## 13.CSS轮廓 

Outline 轮廓是在元素边框外绘制的线

轮廓是在元素周围、边框外面绘制的线，使元素“脱颖而出”

CSS 具有以下轮廓属性：

- `outline-style`
- `outline-color`
- `outline-width`
- `outline-offset`
- `outline`

**注意：**轮廓不同于边框，与边框不同，轮廓绘制在元素边框之外，可能与其他内容重叠。此外，轮廓不是元素尺寸的一部分；元素的总宽度和高度不受轮廓宽度的影响。

轮廓样式`outline-style: dotted` 属性值与边框样式的属性值类似

轮廓宽度`outline-width`属性指定轮廓的宽度，可以设置为：

- thin（通常为 1px）
- medium（通常为 3px）
- thick（通常为 5px）
- 特定尺寸（以 px、pt、cm、em 等为单位）

轮廓颜色`outline-color`

**简写**：`outline`属性是用于设置以下单独轮廓属性的简写属性：

- `outline-width`
- `outline-style`（必需的）
- `outline-color`

**轮廓偏移：**

`outline-offset`属性在元素的轮廓和边缘/边框之间添加空间。

元素与其轮廓之间的空间是透明的。

`outline-offset: 15px;`

指定了边框边缘外 15px 的轮廓

## 14.CSS文本

CSS 具有许多用于格式化文本的属性

**文本颜色**`color`

**文本对齐**`text-align`

  属性值`center`居中、`left`左对齐、`right`右对齐

  以及`justify`两端对齐

**文本最后对齐**`text-align-last`

**文本方向**`direction`和`unicode-bidi`

 `direction: rtl;`
 `unicode-bidi: bidi-override;`强制元素内部的所有文本按照指定的`direction`属性值进行排列

This is right-to-left text direction.这是一个右向左对齐的重定向

**垂直对齐：**设置文本中图像的垂直对齐方式

`vertical-align: baseline`基线对齐

在文本行中，基线是一条虚拟的线，文字通常是沿着这条线进行排列的

`vertical-align: text - top`文本顶部对齐

图像的顶端会和同一行中最高的文本字符的顶端对齐

`vertical-align: text - bottom`文本底部对齐

图像的底端会和同一行中最低的文本字符的底端对齐

`vertical-align: sub`下标对齐

使图像的基线与父元素的下标基线对齐

`vertical-align: super`上标对齐

使图像的基线与父元素的上标基线对齐

**文本修饰**

`text-decoration-line`给文本添加装饰线

  `overline`上划线

  `line-through`删除线

  `underline`下划线

  `overline underline`上下划线

**注意：**不建议给非链接的文本加下划线，因为这通常会让读者感到困惑。

`text-decoration-color`装饰线颜色

`text-decoration-style`装饰线样式，属性值同边框样式

`text-decoration-thickness`装饰线粗细，属性同边框宽度

**简写**

`text-decoration`属性是以下属性的简写：

- `text-decoration-line`（必需的）
- `text-decoration-color`（选修的）
- `text-decoration-style`（选修的）
- `text-decoration-thickness`（选修的）

例如：`text-decoration: underline red double 5px;`

**tips：**HTML 中的所有链接默认都带有下划线。有时您会看到链接的样式没有下划线。`text-decoration: none;`用于从链接中删除下划线

**文本转换**

文本转换`text-transform`

  `uppercase`大写

  `lowercase`小写

  `capitalize`首字母大写

**文本间距**

文本缩进`text-indent: 50px`

字母间距`letter-spacing: 5px`

行高`line-height: 0.8`

字间距`word-spacing: -2px`单词之间的间距

控制空白字符（包括空格、制表符、换行符）`white-space`

`normal`这是`white-space`属性的默认值。在`normal`模式下，浏览器会将连续的空白字符（如空格、制表符、换行符）合并为一个空格，并且会自动换行文本，以适应容器的宽度

`nowrap`文本不会自动换行。当文本内容超出容器宽度时，它会继续在同一行显示，直到遇到一个`<br>`标签才会换行。连续的空白字符同样会被合并为一个空格。

`pre`空白字符会被保留，就像在`<pre>`HTML 标签中一样，文本会按照源代码中的格式进行显示，包括空格、制表符和换行符。并且文本不会自动换行，只有在遇到换行符（在代码中写入的`\n`或者 HTML 中的`<br>`）时才会换行。

`pre-wrap`空白字符会被保留，和`pre`属性类似。但是和`pre`不同的是，文本会在必要时自动换行，以适应容器的宽度。这结合了`pre`保留空白和`normal`自动换行的特点。

`pre-nowrap`空白字符会被保留，但是文本不会自动换行，类似于`pre`和`nowrap`的结合。它会按照源代码中的空白字符和换行符来显示文本，并且不会因为容器宽度而自动换行。

**文本阴影**

`text-shadow: 2px 2px 5px red;`

分别是：水平阴影、垂直阴影、模糊和颜色

## 15.CSS字体

CSS 中有五种通用字体系列：

1. **Serif**字体在每个字母的边缘都有一条细线。它们营造出一种正式而优雅的感觉。
2. **Sans-serif**字体线条干净（没有小笔画）。它们营造出现代简约的外观。
3. **Monospace**字体 - 此类字体的所有字母都具有相同的固定宽度。它们营造出一种机械感。 
4. **Cursive**字体模仿人类的笔迹。
5. **Fantasy**字体是装饰性/有趣的字体。

![](C:\Users\Rain7\Desktop\笔记md\图片\fontnor.png)

**字体样式**

使用`font-family`属性来指定文本的字体

`font-family`属性应包含多个字体名称作为“后备”系统，以确保浏览器/操作系统之间的最大兼容性

例如：`font-family: "Times New Roman", Times, serif;`

`font-style`属性主要用于指定斜体文本

此属性有三个值：

- normal - 文本正常显示
- italic - 文本以斜体显示
- oblique - 文本“倾斜”（倾斜与斜体非常相似，但支撑力较差）

`font-weight`属性指定字体的粗细

  `normal`默认

  `bold`加粗

  还可以设定100~900间的数字值，更精确的控制字体粗细

`font-variant`属性指定文本是否应以小型大写字体显示

 `normal`

 `small-caps`在小型大写字体中，所有小写字母都会转换为大写字母。但是，转换后的大写字母的字体大小会比文本中原来的大写字母小。

**字体大小**

`font-size`属性设置文本的大小

**注意：**如果您未指定字体大小，则普通文本（如段落）的默认大小为 16px（16px=1em）。

px em 百分比

响应式字体大小：文本大小可以用单位设置`vw`，即“视口宽度”。

例如：`font-size:10vw`

**Google字体**

添加Google 字体

`<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Sofia">`

要使用多种 Google 字体，只需用管道字符 ( `|`) 分隔字体名称

`<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Audiowide|Sofia|Trirong">`

**字体搭配**

Georgia 和 Verdana

  Georgia 和 Verdana 是经典的组合。它还符合网络安全字体标准。

  使用“Georgia”字体作为标题，使用“Verdana”字体作为文本。

Helvetica 和 Garamond

  Helvetica 和 Garamond 是另一种使用网页安全字体的经典组合

  标题使用“Helvetica”字体，文本使用“Garamond”字体。

**简写**

该`font`属性是以下属性的简写：

- `font-style`
- `font-variant`
- `font-weight`
- `font-size/line-height`
- `font-family`

例如：`font: italic small-caps bold 12px/30px Georgia, serif;`

**注意：**`font-size`是`font-family` 必需的。如果缺少其他值之一，则使用其默认值。

## 16.CSS图标

通过使用图标库，可以轻松地将图标添加到您的 HTML 页面。

将指定图标类的名称添加到任何内联 HTML 元素（如`<i>`或 `<span>`）。

例如：Font Awesome 图标，Bootstrap 图标，Google 图标

## 17.CSS链接

使用 CSS，链接可以采用多种不同方式的样式。

例如，文字链接和按钮链接

`<a href="index.html" target="_blank">This is a link</a>`

此外，根据链接所处的**状态，**可以采用不同的样式。

这四个链接状态是：

- `a:link`- 正常的、未访问过的链接
- `a:visited`- 用户访问过的链接
- `a:hover`- 当用户鼠标悬停在链接上时
- `a:active`- 点击链接

在为多个链接状态设置样式时，有一些顺序规则：

- `a:hover` 必须位于 `a:link` 和 `a:visited` 之后
- `a:active` 必须位于 `a:hover` 之后

`text-decoration`属性主要用于删除链接的下划线

`background-color`属性可用于指定链接的背景颜色

小手光标`cursor:pointer`

## 18.CSS列表

在 HTML 中，有两种主要类型的列表：

- 无序列表 (`<ul>`) - 列表项用项目符号标记
- 有序列表 (`<ol>`) - 列表项用数字或字母标记

CSS 列表属性允许您：

- 为有序列表设置不同的列表项标记
- 为无序列表设置不同的列表项标记
- 将图像设置为列表项标记
- 为列表和列表项添加背景颜色

`list-style-type`属性指定列表项标记的类型，属性值如下：

  `none` 此属性值用于移除列表项的标记。当设置为`none`时，无论是有序列表（`<ol>`）还是无序列表（`<ul>`），其默认的标记（如数字、圆点等）都不会显示。

  `disc` 这是无序列表（`<ul>`）的默认属性值。它会在每个列表项前面显示一个实心圆点（●）作为标记。这种标记简单明了，适用于大多数普通的无序列表场景，如文章中的简单列举内容。

  `circle` 也是用于无序列表，它会在每个列表项前面显示一个空心圆圈（○）作为标记。相较于`disc`，`circle`标记的视觉效果更加柔和，适用于一些需要更精致或低调的列表展示场景。

  `square` 同样用于无序列表，会在每个列表项前面显示一个实心方块（■）作为标记。这种标记比`disc`更加醒目，在需要强调列表项或者列表内容比较重要时可以使用。

  `decimal` 这是有序列表（`<ol>`）的默认属性值。它会以十进制数字（1、2、3 等）作为列表项的标记，用于表示有顺序的内容列举，如步骤说明、排名等场景。

  `decimal-leading-zero` 用于有序列表，会以带有前导零的十进制数字（01、02、03 等）作为列表项的标记。这种标记在一些需要对编号进行格式化的场景中很有用，比如在文档的章节编号或者有严格编号规范的列表中。

 `lower-roman` 用于有序列表，会以小写罗马数字（i、ii、iii 等）作为列表项的标记。这种标记在书籍的前言、目录等部分或者一些具有古典风格的文档中经常使用。

 `upper-roman` 用于有序列表，会以大写罗马数字（I、II、III 等）作为列表项的标记。和`lower - roman`类似，它也适用于具有古典风格或需要强调编号的有序列表场景，不过视觉上更加醒目。

 `lower-alpha` 用于有序列表，会以小写英文字母（a、b、c 等）作为列表项的标记。这种标记在一些简单的列举或者需要与数字编号区分开来的有序内容中很有用。

  `upper-aplha` 用于有序列表，会以大写英文字母（A、B、C 等）作为列表项的标记。和`lower - alpha`类似，但视觉效果更加强烈，适用于需要突出列表项编号的场景。

**使用图像作为列表项标记**

`list-style-image`属性指定图像作为列表项标记:

例如：`list-style-image: url("ulpic.png");`

**定位列表项标记**

`list-style-position`属性指定列表项标记（项目符号）的位置

`list-style-position: outside;` 表示项目符号将位于列表项之外。列表项每行的开头将垂直对齐。这是默认值。

`list-style-position: inside;` 表示项目符号将位于列表项内。由于它是列表项的一部分，因此它将成为文本的一部分，并将文本推到开头。

**删除默认设置**

`list-style-type:none`属性还可用于删除标记/项目符号。请注意，列表还具有默认边距和填充。要删除它，请将`margin:0`和添加`padding:0`到 `<ul>` 或 `<ol>`

例如：

```css
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
```

**简写**

使用简写属性时，属性值的顺序为：

- `list-style-type`（如果指定了 list-style-image，当图像由于某种原因无法显示时将显示此属性的值）
- `list-style-position`（指定列表项标记是否应出现在内容流的内部或外部）
- `list-style-image`（指定图像作为列表项标记）

例如：

```css
ul {
  list-style: square inside url("ulpic.png");
}
```

**带颜色的样式列表**

添加到 `<ol>` 或 `<ul>` 标签的任何内容都会影响整个列表，而添加到 `<li>` 标签的属性将影响单个列表项

`background: blue`

## 19.CSS表格

使用 CSS 可以大大改善 HTML 表格的外观：

**表格边框**

要在 CSS 中指定表格边框，请使用`border`属性。

**折叠表格边框**  (删除双边框)

`border-collapse`属性设置表格边框是否应折叠为单个边框

`border-collapse: collapse;`

**表格大小**

表格的宽度和高度由`width`和`height`属性定义。

**表格对齐**

`text-align` 水平对齐 【左右】

`vertical-align` 垂直对齐 【上下】

**表格样式**

填充：`padding`

水平分割线：`border-bottom`

**表格悬停样式**

使用`:hover`在`<tr>` 上的选择器在鼠标悬停时突出显示表格行

例如：`tr:hover {background-color: coral;}`

**条纹桌**

对于条纹表，使用选择器并向所有偶数（或奇数）表行`nth-child()`添加：`background-color`

`tr:nth-child(even) {background-color: #f2f2f2;}`

**表格颜色**

下面的示例指定了 `<th>` 元素的背景颜色和文本颜色：

```css
th {
  background-color: #04AA6D;
  color: white;
}
```

**响应式表格**

如果屏幕太小而无法显示全部内容，响应式表格将显示水平滚动条：

`overflow-x:auto`在 `<table>` 元素周围添加一个容器元素（如 `<div>`）以使其具有响应性：

**注意：**在 OS X Lion（在 Mac 上）中，滚动条默认是隐藏的，只有在使用时才显示（即使设置了“overflow:scroll”）。

## 20.CSS布局

### display

`display`属性是控制布局的最重要的 CSS 属性

`display`属性用于指定元素在网页上的显示方式

每个 HTML 元素都有一个默认显示值，具体取决于元素类型。大多数元素的默认显示值为`block`或 `inline`。

该`display`属性用于改变HTML元素的默认显示行为。

`block` 块级元素 （例如`<div>`）

块级元素始终从新行开始并占据整个可用宽度（尽可能向左和向右延伸）

`inline` 内联元素 （例如`<span>`）

内联元素不会从新行开始，并且仅占用必要的宽度

**布局：无**

`display: none;`通常与 JavaScript 一起使用来隐藏和显示元素，而无需删除和重新创建它们。

**覆盖默认显示值**

每个元素都有一个默认显示值。但是，可以覆盖此值。

将内联元素更改为块元素或反之亦然，可以使页面看起来具有特定的样子，同时仍然遵循网络标准。

一个常见的例子是制作`<li>`水平菜单的内联元素：

```css
li {
  display: inline;
}
```

**注意：**设置元素的显示属性只会改变**元素的显示方式**，而不会改变元素的类型。因此，内联元素中`display: block;`不允许包含其他块元素。

例如：将 `<span>` 元素显示为块元素：

```css
span {
  display: block;
}
```

**隐藏元素**

`display`可以通过将属性设置为`none`来隐藏元素。

`display: none;`元素将被隐藏，页面将显示，就像元素不存在一样

`visibility:hidden;` 元素将被隐藏，但是，元素仍将占用与之前相同的空间，仍会影响布局

**DIV最大宽度**

设置`width`块级元素的 将阻止其延伸到其容器的边缘。然后，您可以将边距设置为自动`margin: auto`，以使元素在其容器内水平居中。元素将占据指定的宽度，剩余空间将在两个边距之间平均分配。

**注意：**`<div>`当浏览器窗口小于元素的宽度时，就会出现上述问题。然后浏览器会在页面上添加一个水平滚动条。

在这种情况下，使用`max-width`可以改善浏览器对小窗口的处理。这对于使网站在小型设备上可用非常重要。（div会显示全）

### 定位

`position`属性指定元素使用的定位方法类型（静态、相对、固定、绝对或粘性）

有五种不同的位置值：

- `static` 静态

HTML 元素默认定位为静态。

静态定位元素不受顶部、底部、左侧和右侧属性的影响。

带有`position: static;`的元素不以任何特殊方式定位，它始终根据页面的正常流程进行定位。

- `relative` 相对

带有`position: relative;`的元素是相对于其正常位置进行定位的。

设置相对定位元素的 top、right、bottom 和 left 属性将导致其调整远离正常位置。其他内容将不会调整以适应元素留下的任何间隙。

- `fixed` 固定

元素`position: fixed;`相对于**视口**进行定位，这意味着即使页面滚动，它始终停留在同一位置。top、right、bottom 和 left 属性用于定位元素。

- `absolute` 绝对

带有定位的元素`position: absolute;`是相对于最近的定位祖先(positioned ancestor)进行定位的（而不是像固定那样相对于视口进行定位）。

但是，如果绝对定位元素没有定位祖先，它将使用文档主体，并随着页面滚动而移动。

? 绝对定位是和相对定位一起使用的

**注意：**绝对定位元素脱离了正常的流动，并且可以与元素重叠。

- `sticky` 粘性

带有`position: sticky;`的元素的定位基于用户的滚动位置。

粘性元素在`relative`和`fixed`之间切换，具体取决于滚动位置。它处于相对位置，直到在视口中达到给定的偏移位置 - 然后它“粘”在原处（如 position:fixed）。

**注意：**必须至少指定`top`、`right`或`bottom`中的一个`left`才能使粘性定位起作用。

**例如：**`top: 0` 滚动的时候**粘**在上面

### Z 索引

`z-index`属性指定元素的堆叠顺序

当元素定位时，它们可以重叠其他元素

`z-index`属性指定元素的堆叠顺序（哪个元素应放置在其他元素的前面或后面）

元素可以具有正或负的堆叠顺序

**注意：** `z-index`仅适用于

定位元素

  position：absolute

  position：relative

  position：fixed 

  position：sticky

弹性项目

  display：flex 元素的直接子元素

如果两个定位元素相互重叠且未指定`z-index`，**则 HTML 代码中最后** 定义的元素将显示在顶部。

### 溢出 overflow

`overflow`属性控制当内容太大而无法容纳在某个区域时如何处理

`overflow`属性具有以下值：

- `visible`- 默认。**溢出**部分不会被裁剪。内容渲染在元素框的外面
- `hidden`- **溢出**部分将被**剪裁**（隐藏），其余内容将不可见
- `scroll`- 溢出部分被裁剪，并且添加了**滚动**条以查看剩余内容
- `auto`- 类似于`scroll`，但它只在**必要时添加滚动条**

**注意：**该`overflow`属性仅适用于具有指定高度的块元素。

**注意：**在 OS X Lion（在 Mac 上）中，滚动条默认是隐藏的，只有在使用时才显示（即使设置了“overflow:scroll”）。

`overflow-x`和属性`overflow-y`指定是否仅在水平方向还是垂直方向（或两者）更改内容溢出：

`overflow-x`指定如何处理内容的左/右边缘。
`overflow-y`指定如何处理内容的顶部/底部边缘。

这两个属性的属性值也是上面四个属性值

### 浮动和清除

`float`属性指定元素如何浮动

`clear`属性指定哪些元素可以浮动在清除元素旁边以及在哪一侧

`float`属性用于定位和格式化内容，例如让图像在容器中浮动到文本左侧。

`float`属性可以具有下列值之一：

- `left`- 元素浮动到其容器的左侧
- `right`- 元素浮动到其容器的右侧
- `none`- 元素不浮动（将显示在文本中出现的位置）。这是默认设置
- `inherit`- 该元素继承其父元素的浮点值

通常情况下，div 元素会显示在彼此的上方。但是，如果我们使用`float: left`，便可以让元素彼此浮动相邻

---

当我们使用该`float`属性时，并且我们想要下面的下一个元素（不在右边或左边），我们将必须使用`clear` 属性。

`clear`属性指定浮动元素旁边的元素应发生什么。

`clear`属性可以具有下列值之一：

- `none`- 元素不会被推到左浮动元素或右浮动元素下方。这是默认设置
- `left`- 该元素被推到左浮动元素下方
- `right`- 该元素被推到右浮动元素下方
- `both`- 该元素被推到左浮动元素和右浮动元素的下方
- `inherit`- 该元素从其父元素继承了明确值

清除浮动时，应将清除与浮动匹配：如果元素向左浮动，则应向左清除。浮动元素将继续浮动，但清除的元素将出现在网页上浮动元素的下方。

**clearfix**

如果浮动元素比包含元素高，它将“溢出”到其容器之外。然后我们可以添加一个 clearfix hack 来解决这个问题

例如：

```css
.clearfix {
  overflow: auto;
}
```

`overflow: auto`只要能够控制边距和填充（否则您可能会看到滚动条），clearfix 就可以很好地工作。 但是**，新式（new）、现代的（modern） clearfix hack**使用起来更安全，以下代码适用于大多数网页：

```css
.clearfix::after {
  content: "";
  clear: both;
  display: table;
}
```

`::after` 伪元素

`box-sizing`

### 内联块

`display: inline-block` 

相比`display: inline`，主要的区别在于`display: inline-block`允许设置元素的宽度和高度。

此外，使用` display: inline-block`时，顶部和底部的边距/填充会受到尊重，但使用`display: inline`则不会。

与`display: block`相比，主要区别在于`display: inline-block`不在元素后添加换行符，因此该元素可以位于其他元素旁边。

**内联块对于宽度和高度的设置**

**与块相比，内联块又是内联的**

使用 inline-block 创建导航链接

`display: inline-block`的一个常见用途是创建水平导航链接，列表项水平显示，而不是垂直显示。

### 对齐

**居中对齐元素：**

要水平居中块元素（例如 `<div>`），使用`margin: auto;`

设置元素的宽度将防止其延伸到其容器的边缘。

然后元素将占据指定的宽度，剩余空间将在两个边距之间平均分配

**注意：**`width`如果未设置该属性（或设置为 100%），则居中对齐无效。

**居中对齐文本：**

要将文本置于元素的中心，请使用`text-align: center;`

**将图像置于中心：**

要使图像居中，请设置左边距和右边距`auto`并将其变成一个`block`元素（`display: block;`）

**左对齐和右对齐 - position**

对齐元素的一种方法是使用`position: absolute;`（`left: 0px;`或`right: 0px`）

**注意：**绝对定位元素脱离了正常流，并且可以与元素重叠。

**左对齐和右对齐 - float**

对齐元素的另一种方法是使用`float`属性

**clearfix**

**注意：**如果某个元素比包含它的元素高，并且它是浮动的，它将溢出其容器。您可以使用“clearfix hack”来修复此问题

**垂直居中 - padding**

一个简单的解决方案是使用 top 和 bottom `padding`

例如：`padding: 70px 0;`

要垂直和水平居中，请使用`padding`和`text-align: center`

**垂直居中 - 使用 line-height**

另一个技巧是使用`line-height`，与属性值相等的属性`height`

`line-height: 200px;`
`height: 200px;`

**垂直居中 - transform**

如果`padding`和`line-height` 不是选项，则另一种解决方案是使用定位和`transform`属性

`transform: translate(-50%, -50%);`

**垂直居中 - 使用 Flexbox**

注意，IE10 及更早版本不支持 flexbox

 `display: flex;`
 `justify-content: center;`

## 21.CSS组合器

一个 CSS 选择器可以包含多个简单选择器。在简单选择器之间，我们可以包含一个组合器。

CSS 中有四种不同的组合器：

- 后代组合器（空格）
- 子组合器 (>)
- 下一个兄弟组合器 (+)
- 后续兄弟组合器 (~)

**后代组合器：**

后代组合器匹配指定元素的所有后代元素。`div p {}`

**子组合器 (>)：**

子组合器选择指定元素的所有子元素。`div > p {}`

**下一个兄弟组合器 (+)：**

下一个同级组合器用于选择紧接着另一个特定元素的元素。

兄弟元素必须具有相同的父元素，“相邻”表示“紧随其后”。`div + p {}`

  **下一个**  指一个

**后续兄弟组合器 (~)：**

后续兄弟组合器选择指定元素的下一个兄弟的所有元素。`div ~ p{}`

  **后续**  指所有

## 22.CSS伪类

什么是伪类？

伪类用于定义元素的特殊状态。

例如，它可用于：

- 当用户将鼠标移到元素上时设置元素的样式
- 对访问过的和未访问过的链接设置不同的样式
- 当元素获得焦点时设置其样式
- 样式有效/无效/必需/可选的表单元素

**语法：**

```css
selector:pseudo-class {
  property: value;
}
```

锚点伪类：

链接可以以不同的方式显示：

```css
/* unvisited link */
a:link {
  color: red;
}

/* visited link */
a:visited {
  color: green;
}

/* mouse over link */
a:hover {
  color: hotpink;
}

/* selected link */
a:active {
  color: blue;
}
```

**注意：** `a:hover`必须位于CSS 定义`a:link`之后 `a:visited`才能生效！`a:active`必须位于 `a:hover`CSS 定义之后才能生效！伪类名不区分大小写。

伪类和HTML类：

伪类可以与 HTML 标签上的类相结合

例如：`a.demo:hover {}` 其中，`demo`是html文档中`<a>`标签的class的属性值。

悬停伪类：

`:hover`

:first-child 伪类：

`:first-child`伪类与作为另一个元素的第一个子元素的指定元素匹配。

`p:first-child` p标签的第一个

:lang 伪类

`:lang`伪类允许您为不同的**语言定义特殊规则**。

## 23.CSS伪元素

CSS 伪元素用于设置元素特定部分的样式。

例如，它可用于：

- 为元素的第一个字母或行设置样式
- 在元素之前或之后插入内容
- 设置列表项标记的样式
- 设置对话框后面的视图框的样式

**语法：**

```css
selector::pseudo-element {
  property: value;
}
```

**::first-line 伪元素**

`::first-line`伪元素用于给文本的第一行添加特殊样式。

**注意：**伪元素`::first-line`只能应用于块级元素。

下列属性适用于`::first-line` 伪元素：

- 字体属性
- 颜色属性
- 背景属性
- 字间距
- 字距
- 文字修饰
- 垂直对齐
- 文本转换
- 行高
- 清除

**双冒号（`::`）是 CSS3 引入的用于伪元素的新语法，为了区分伪元素和伪类**

**::first-letter 伪元素**

`::first-letter`伪元素用于给文本的首字母添加特殊样式。

**注意：**伪元素`::first-letter`只能应用于块级元素。

以下属性适用于 ::first-letter 伪元素： 

- 字体属性
- 颜色属性 
- 背景属性
- 边距属性
- 填充属性
- 边框属性
- 文字修饰
- 垂直对齐（仅当“float”为“none”时）
- 文本转换
- 行高
- 漂浮
- 清除

**伪元素和 HTML 类**

伪元素可以与 HTML 类结合。

例如：`p.demo::first-letter {}`

**多个伪元素**

还可以将多个伪元素组合起来。

例如： `p::first-letter {} 和 p::first-line {}`

**::before 伪元素**

`::before`伪元素可用于在元素内容之前插入一些内容。

元素的前面

**::after 伪元素**

`::after`伪元素可用于在元素内容之后插入一些内容。

**::marker 伪元素**

`::marker`伪元素选择列表项的标记。

**::selection 伪元素**

`::selection`伪元素与用户选择的元素部分匹配。

例如鼠标光标选中文字

## 24.CSS不透明度/透明度

`opacity`属性指定元素的不透明度/透明度。

透明悬停效果

`opacity`属性通常与选择器一起使用`:hover` ，以改变鼠标悬停时的不透明度

例如：

```css
img {
  opacity: 0.5;
}

img:hover {
  opacity: 1.0;
}
```

使用 RGBA 实现透明度：

RGBA 颜色值指定为：rgba(red, green, blue, *alpha* )。

alpha *参数*是 0.0（完全透明）和 1.0（完全不透明）之间的数字。

## 25.CSS导航栏

对于任何网站来说，拥有易于使用的导航都很重要。

使用 CSS，您可以将无趣的 HTML 菜单转换为美观的导航栏。

**导航栏 = 链接列表**

导航栏需要标准 HTML 作为基础。

在我们的示例中，我们将根据标准 HTML 列表构建导航栏。

导航栏基本上是一个链接列表，因此使用 `<ul>` 和 `<li>` 元素非常有意义

**垂直导航栏**

`li a { display: block; }`

a标签是内联的，要设置为块

**水平导航栏**

`li { diplay: inline; }`

li标签是块，要设置为内联

## 26.CSS属性选择器

**`[attribute]`选择器** 属性选择器

`[attribute]选择器`用于选择具有指定属性的元素。

**选择**  **具有其中属性的元素**

例如：

```css
a[target] {
  background-color: yellow;
}
```

**[attribute="value"] 选择器** 属性值选择器

`[attribute="value"]选择器`用于选择具有指定属性和值的元素。

例如：

```css
a[target="_blank"] {
  background-color: yellow;
}
```

**[attribute~="value"]选择器** 属性值近似(包含)选择器

`[attribute~="value"]选择器`用于选择属性值包含指定单词的元素。

**[attribute|="value"]选择器** 属性值扩展(跟随)选择器

`[attribute|="value"]选择器`用于选择具有指定属性的元素，其值可以正好是指定的值，或者是指定的值后跟连字符（-）。

例如：

```css
[class|="top"] {
  background: yellow;
}
```

**注意：**该值必须是一个完整的单词，可以是单独的，如 class="top"，也可以后跟连字符 (-)，如 class="top-text"。

**[attribute^="value"] 选择器** 属性值开头选择器

`[attribute^="value"]选择器`用于选择具有指定属性的元素，其值**以指定的值开头**。

例如：选择所有类属性值以“top”开头的元素：

```css
[class^="top"] {
  background: yellow;
}
```

**注意：**该值不必是一个完整的单词！

**[attribute$="value"] 选择器** 属性值结尾选择器

`[attribute$="value"]选择器`用于选择属性值以指定值结尾的元素。

例如：

```css
[class$="test"] {
  background: yellow;
}
```

**注意：**该值不必是一个完整的单词！ 

**[attribute*="value"]选择器** 属性值包含选择器

`[attribute*="value"]选择器`用于选择属性值包含指定值的元素。

例如：

```css
[class*="te"] {
  background: yellow;
}
```

**注意：**该值不必是一个完整的单词！ 

**样式表单**

属性选择器对于没有类或 ID 的表单样式很有用

## 27.CSS计数器

**使用计数器自动编号**

CSS 计数器就像“变量”。变量值可以通过 CSS 规则增加（将跟踪变量使用的次数）。

为了使用 CSS 计数器，我们将使用以下属性：

- `counter-reset`- 创建或重置计数器
- `counter-increment`- 增加计数器值
- `content`- 插入生成的内容
- `counter()`或`counters()`函数 - 将计数器的值添加到元素

要使用 CSS 计数器，必须首先使用 创建它`counter-reset`。

例如：为页面创建一个计数器（在 body 选择器中），然后为每个 `<h2>` 元素增加计数器值，并将“Section <*计数器的值*>:”添加到每个 `<h2>` 元素的开头

```css
body {
  counter-reset: section;
}

h2::before {
  counter-increment: section;
  content: "Section " counter(section) ": ";
}
```

**嵌套计数器**

例如：为页面 (section) 创建一个计数器，并为每个 `<h1>` 元素 (subsection) 创建一个计数器。“section”计数器将通过“Section <*节计数器的值*>.”为每个 `<h1>` 元素进行计数，“subsection”计数器将通过“<*节计数器的值*>.<*子节计数器的值*>”为每个 `<h2>` 元素进行计数

```css
body {
  counter-reset: section;
}

h1 {
  counter-reset: subsection;
}

h1::before {
  counter-increment: section;
  content: "Section " counter(section) ". ";
}

h2::before {
  counter-increment: subsection;
  content: counter(section) "." counter(subsection) " ";
}
```

## 28.CSS网站布局

![](C:\Users\Rain7\Desktop\笔记md\图片\weblayout.png)

有很多不同的布局设计可供选择。但是，上面的结构是最常见的结构之一。

## 29.CSS单位

CSS 有几种不同的单位来表达长度。

许多 CSS 属性采用“长度”值，例如`width`、`margin`、`padding`、 `font-size`等。

**长度**是一个数字，后跟长度单位，例如`10px`、 `2em`等。

**绝对长度** 

绝对长度单位是固定的，用任何一个单位表示的长度都会显示为完全相同的尺寸。

不建议在屏幕上使用绝对长度单位，因为屏幕尺寸差异很大。但是，如果输出介质已知，例如用于打印布局，则可以使用这些单位。

| Unit | Description                  |
| :--- | :--------------------------- |
| cm   | centimeters                  |
| mm   | millimeters                  |
| in   | inches (1in = 96px = 2.54cm) |
| px * | pixels (1px = 1/96th of 1in) |
| pt   | points (1pt = 1/72 of 1in)   |
| pc   | picas (1pc = 12 pt)          |

\* 像素 (px) 是相对于查看设备的。对于低 dpi 设备，1px 是显示屏的一个设备像素（点）。对于打印机和高分辨率屏幕，1px 意味着多个设备像素。

**相对长度**

相对长度单位指定相对于另一个长度属性的长度。

相对长度单位在不同的渲染媒介之间具有更好的扩展性。



| Unit | Description                                                  |
| :--- | :----------------------------------------------------------- |
| em   | Relative to the font-size of the element (2em means 2 times the size of the current font) |
| ex   | Relative to the x-height of the current font (rarely used)   |
| ch   | Relative to width of the "0" (zero)                          |
| rem  | Relative to font-size of the root element                    |
| vw   | Relative to 1% of the width of the viewport*                 |
| vh   | Relative to 1% of the height of the viewport*                |
| vmin | Relative to 1% of viewport's* smaller dimension              |
| vmax | Relative to 1% of viewport's* larger dimension               |
| %    | Relative to the parent element                               |

**提示：** em 和 rem 单位在创建完美可扩展的布局时非常有用！
\* 视口 = 浏览器窗口大小。如果视口宽度为 50 厘米，则 1vw = 0.5 厘米。

## 30.CSS特异性

什么是特异性？

如果有两个或多个 CSS 规则指向同一个元素，则特异性最高的选择器将“获胜”，并且其样式声明将应用于该 HTML 元素。

将特殊性视为一种层次结构，它决定了哪种样式声明最终应用于元素。

**优先级**

| Priority                     | Example                     | Description                                                  |
| :--------------------------- | :-------------------------- | :----------------------------------------------------------- |
| Inline style                 | `<h1 style="color: pink;">` | Highest priority, directly applied with the style attribute  |
| Id selectors                 | #navbar                     | Second highest priority, identified by the unique id attribute of an element |
| Classes and pseudo-classes   | .test, :hover               | Third highest priority, targeted using class names           |
| Attributes                   | [type="text"]               | Low priority, applies to attributes                          |
| Elements and pseudo-elements | h1, ::before, ::after       | Lowest priority, applies to HTML elements and pseudo-elements |

**更多特异性规则示例**

**同等特殊性：最新规则优先**- 如果在外部样式表中两次写入相同的规则，则最新规则优先

**代码写在下面，更靠后的更优先**

## 31.CSS重要规则

什么是!important 规则

CSS 中的规则`!important`用于为属性/值添加比正常情况下更重要的重要性。

事实上，如果您使用该`!important`规则，它将覆盖该元素上该特定属性的所有先前的样式规则！

例如：

```css
#myid {
  background-color: blue;
}

.myclass {
  background-color: gray;
}

p {
  background-color: red !important;
}
```

解释：在上面的例子中，尽管 ID 选择器和类选择器的特异性更高，但所有三个段落都将获得红色背景颜色。在这两种情况下，`!important`规则都会覆盖` background-color`属性。

注意：

覆盖规则的唯一方法`!important` 是在源代码中以相同（或更高）特异性在声明中包含另一条`!important` 规则 - 问题就从这里开始！这会使 CSS 代码混乱，并且调试会很困难，特别是如果您有一个大型样式表！

**提示：**了解该`!important` 规则很有用。您可能会在某些 CSS 源代码中看到它。但是，除非绝对必要，否则请不要使用它。

**`!important` 的合理用法**

一种使用方法`!important`是，如果您必须覆盖无法以任何其他方式覆盖的样式。如果您正在使用内容管理系统 (CMS) 并且无法编辑 CSS 代码，则可能出现这种情况。然后，您可以设置一些自定义样式来覆盖某些 CMS 样式。

另一种使用方法`!important`是：假设您希望页面上的所有按钮都具有特殊外观。在这里，按钮采用灰色背景颜色、白色文本以及一些填充和边框。（特例）

## 32.CSS数学函数

CSS 数学函数允许将数学表达式用作属性值

**calc() 函数**

该`calc()`函数执行计算以用作属性值。

语法：calc(*expression*)

| Value        | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| *expression* | Required. A mathematical expression. The result will be used as the value. The following operators can be used: + - * / |

**max() 函数**

该`max()`函数使用逗号分隔的值列表中的最大值作为属性值。

语法：max(*value1*, *value2*, ...)

| Value                   | Description                                                  |
| :---------------------- | :----------------------------------------------------------- |
| *value1*, *value2*, ... | Required. A list of comma-separated values - where the largest value is chosen |

**min() 函数**

该`min()`函数使用逗号分隔的值列表中的最小值作为属性值。

语法：min(*value1*, *value2*, ...)

| Value                   | Description                                                  |
| :---------------------- | :----------------------------------------------------------- |
| *value1*, *value2*, ... | Required. A list of comma-separated values - where the smallest value is chosen |
