# CSS Advanced 学习

## 1.CSS圆角

使用 `border-radius`属性，您可以为任何元素赋予“圆角”。

**提示：**`border-radius`属性实际上是

`border-top-left-radius`

`border-top-right-radius`

`border-bottom-right-radius`

`border-bottom-left-radius`

属性的简写属性 。

四个属性值顺序：左上、右上、右下、左下

三个属性值顺序：左上、右上和左下、右下

两个属性值顺序：左上和右下、右上和左下

一个属性值顺序：四个角

## 2.CSS图像边框

`border-image`属性允许您指定要使用的图像来代替元素周围的正常边框。

该属性由三部分组成：

- `source` 图像源

- `slice` 切片

用于指定如何将边框图像切割成九个部分，类似于九宫格的方式。

它的值可以是一个或四个数字，单位可以是像素（`px`）或百分比（`%`）。

一个数字表示四个边框（上、下、左、右）都使用相同的切片大小；四个数字则分别表示上、右、下、左四个边框的切片大小。

- `repeat` 重复

用于指定边框图像在边框上的重复方式，有`stretch`（拉伸）、`repeat`（重复）、`round`（平铺）和`space`（间隔平铺）四种方式。

```css
#borderimg1 {
  border: 10px solid transparent;
  padding: 15px;
  border-image: url(border.png) 20% round;
}
```

`transparent` 边框颜色设置为透明

**提示：**`border-image`属性实际上是 

`border-image-source`

`border-image-slice`

`border-image-width`

`border-image-outset` 外延 （长度）

`border-image-repeat`

属性的缩写。

## 3.CSS多重背景

`background-image` 为元素添加多个背景图片

多个背景以逗号分开，并且图像堆叠在一起，其中第一张图像最靠近观看者

例子：

```css
#example1 {
  background-image: url(1.gif), url(2.gif);
  background-position: right bottom, left top;
  background-repeat: no-repeat, repeat;
}
```

简写：

```css
#example1 {
  background: url(1.gif) right bottom no-repeat, url(2.gif) left top repeat;
}
```

`background-size` 指定背景图像的大小，大小可以用长度、百分比来指定

属性值：

`contain` 将背景图像缩放到尽可能大（但其宽度和高度都必须适合内容区域）。

根据背景图像和背景定位区域的比例，背景中可能有一些区域未被背景图像覆盖。

`cover` 缩放背景图像，使内容区域完全被背景图像覆盖（其宽度和高度等于或超过内容区域）。

背景图像的某些部分可能在背景定位区域中不可见。

当使用多个背景时，`background-size` 属性可以设置背景大小的多个值（使用逗号分隔）

**全尺寸背景图像**

```css
html {
  background: url(1.jpg) no-repeat center fixed;
  background-size: cover;
}
```

**background-origin 属性**

`background-origin`属性指定背景图像的位置。（在哪里开始）

属性有三个不同的值：

- border-box - 背景图像从边框的左上角开始
- padding-box-（默认）背景图像从填充边缘的左上角开始
- content-box - 背景图像从内容的左上角开始

**background-clip 属性**

`background-clip`属性指定背景的绘制区域。（在哪里停）

属性有三个不同的值：

- border-box - （默认）背景绘制在边框的外边缘
- padding-box - 背景绘制在填充的外边缘
- content-box - 背景绘制在内容框内

## 4.CSS颜色关键字

**`transparent`关键字**，使颜色透明

**注意：**关键字`transparent` 相当于 rgba(0,0,0,0)。RGBA 颜色值是带有 alpha 通道的 RGB 颜色值的扩展 - 它指定颜色的不透明度。

**`currentcolor`关键字**像一个变量，保存元素颜色属性的当前值

  它代表当前元素的颜色值。这个颜色值通常是通过`color`属性设置的，但也可以是继承自父元素的颜色值

**`inherit`关键字**，指定属性应该从其父元素继承其值

## 5.CSS渐变

CSS 定义了三种类型的渐变：

- **线性渐变**Linear Gradients**（向下/向上/向左/向右/对角线）**
- **径向渐变**Radial Gradients**（由其中心定义）**
- **圆锥渐变**Conic Gradients**（围绕中心点旋转）**

**CSS 线性渐变：**

要创建线性渐变，必须定义至少两个色标。色标是想要在其中呈现平滑过渡的颜色。还可以设置起点和方向（或角度）以及渐变效果。

语法：

**background-image: linear-gradient(*direction*, *color-stop1*, *color-stop2, ...*);**

**方向 - 从上到下（这是默认）**

```css
#grad {
  background-image: linear-gradient(red, yellow);
}
```

**方向 - 从左到右**

```css
#grad {
  background-image: linear-gradient(to right, red , yellow);
}
```

**方向 - 对角线**：指定水平和垂直起始位置来制作对角渐变

**使用角度**

语法：

**background-image: linear-gradient(*angle*, *color-stop1*, *color-stop2*);**

如果想要更好地控制渐变的方向，可以定义一个角度，而不是预定义的方向（向下、向上、向右、向左、向右下等）。0 度值相当于“向上”。90 度值相当于“向右”。180 度值相当于“向下”。

```css
#grad {
  background-image: linear-gradient(180deg, red, yellow);
}
```

使用多个颜色停止点

一个具有多个颜色停止点的线性渐变（从上到下）

```css
#grad {
  background-image: linear-gradient(red, yellow, green);
}
```

彩虹背景

```css
#grad {
  background-image: linear-gradient(to right, red,orange,yellow,green,blue,indigo,violet);
}
```

渐变还支持透明度，用于创建淡入淡出的效果

使用 rgba() 函数来定义颜色停止点，rgba() 函数中的最后一个参数可以是 0 到 1 之间的值，它定义颜色的透明度：0 表示完全透明，1 表示全色（不透明）

```css
#grad {
  background-image: linear-gradient(to right, rgba(255,0,0,0), rgba(255,0,0,1));
}
```

**重复线性渐变**

repeating-linear-gradient() 函数用于重复线性渐变

```css
#grad {
  background-image: repeating-linear-gradient(red, yellow 10%, green 20%);
}
```

---

**径向渐变：**

径向渐变由其中心定义。

要创建径向渐变，还必须定义至少两个颜色停止点（色标）。

语法：

**background-image: radial-gradient(*shape size* at *position, start-color, ..., last-color*);**

默认情况下，形状为椭圆形，尺寸为最远角，位置为中心。

**径向渐变 - 均匀分布的颜色停止点（这是默认设置）**

```css
#grad {
  background-image: radial-gradient(red, yellow, green);
}
```

**径向渐变 - 不同间距的颜色停止点**

```css
#grad {
  background-image: radial-gradient(red 5%, yellow 15%, green 60%);
}
```

**设置形状**

shape 参数定义形状。其值可以是圆形或椭圆形。默认值为椭圆形。

```css
#grad {
  background-image: radial-gradient(circle, red, yellow, green);
}
```

size 参数定义渐变的大小。它可以采用四个值：

- **最近侧**    **closest-side**
- **最远的一侧**     **farthest-side**
- **最近角**    **closest-corner**
- **最远的角落**    **farthest-corner**

```css
#grad1 {
  background-image: radial-gradient(closest-side at 60% 55%, red, yellow, black);
}
```

repeating-radial-gradient() 函数用于重复径向渐变：

```css
#grad {
  background-image: repeating-radial-gradient(red, yellow 10%, green 15%);
}
```

---

**圆锥渐变**

圆锥渐变是颜色过渡围绕中心点旋转的渐变。

要创建圆锥渐变，您必须定义至少两种颜色。

语法：

**background-image: conic-gradient([from *angle*] [at *position*,] *color* [*degree*]*, color* [*degree*]*, ...*);**

默认情况下，*角度*为 0 度，*位置*为中心。

如果没有指定*程度*，颜色将均匀分布在中心点周围。

```css
#grad {
  background-image: conic-gradient(red, yellow, green);
}
```

**圆锥渐变：五种颜色**

```css
#grad {
  background-image: conic-gradient(red, yellow, green, blue, black);
}
```

**圆锥渐变：三种颜色和度数**

```css
#grad {
  background-image: conic-gradient(red 45deg, yellow 90deg, green 210deg);
}
```

**饼图**

```css
#grad {
  background-image: conic-gradient(red, yellow, green, blue, black);
  border-radius: 50%;
}
```

**指定角度的圆锥渐变**

[from *angle*] 指定整个圆锥渐变的旋转角度。

```css
#grad {
  background-image: conic-gradient(from 90deg, red, yellow, green);
}
```

**指定中心位置的圆锥渐变**

[at *position* ] 指定了圆锥渐变的中心。

```css
#grad {
  background-image: conic-gradient(at 60% 45%, red, yellow, green);
}
```

**重复圆锥渐变**

`repeating-conic-gradient()`函数用于重复圆锥渐变

```css
#grad {
  background-image: repeating-conic-gradient(red 10%, yellow 20%);
  border-radius: 50%;
}
```

## 6.CSS阴影

为文本和元素添加阴影

- `text-shadow`
- `box-shadow`

**文本阴影**

指定水平阴影（2px）和垂直阴影（2px）

`text-shadow: 2px 2px;`

添加颜色

`text-shadow: 2px 2px red;`

添加模糊

`text-shadow: 2px 2px 5px red;`

多重阴影：用逗号分隔

**盒子阴影**

指定水平和垂直阴影。

阴影的默认颜色是当前文本颜色。

`box-shadow: 10px 10px;`

添加颜色

`box-shadow: 10px 10px lihgtblue;`

添加模糊

`box-shadow: 10px 10px 5px lightblue;`

添加扩散半径：

`spread`属性，正值会增加阴影的大小，负值则会减小阴影的大小。

`box-shadow: 10px 10px 5px 12px lightblue;`

添加内阴影：

`inset`属性，将阴影从外阴影（一开始）更改为内阴影

`box-shadow: 10px 10px 5px lihgtblue inset;`

添加多重阴影：用逗号分隔

实例：日历卡片

## 7.CSS文本效果

**文本溢出**

`text-overflow`属性，指定应如何向用户发出未显示的溢出内容的信号

属性值：`clip`，当文本内容超出容器的宽度时，`clip`属性值会直接截断文本，并且不显示省略号或其他提示信息。

属性值：`ellipsis`，这是比较常用的属性值。当文本内容超出容器宽度时，它会在文本的末尾显示省略号（...）来表示文本被截断。

属性值：`string自定义字符串`，可以用自定义的字符串来代替省略号显示在文本末尾，表示文本被截断。这个自定义字符串可以是任何文本内容，比如一个特殊符号或者一段简短的提示文字。

鼠标悬停显示溢出内容：

`div.wenbenk:hover { overflow: visible; }`

**自动换行**

`word-wrap`属性允许将长单词拆分并换到下一行

如果一个单词太长，无法在一个区域内显示出来，它就会溢出到区域外

word-wrap 属性允许你强制文本换行 - 即使这意味着在单词中间拆分文本

`word-wrap：break-word;`

? 分词

`word-break`属性指定换行规则

属性值`normal`，默认值，正常换行，如果单词过长，则会溢出。

属性值`keep-all`，尽量保持单词完整性换行

属性值`break-all`，强制换行

**书写模式**

`writing-mode`属性指定文本行是水平排列还是垂直排列

属性值`horizontal-tb`，水平，自上而下

属性值`vertial-rl`，垂直，自右向左

属性值`vertial-tl`，垂直，自左向右

属性值`sideways-rl`，横向，自右向左

属性值`sideways-tl`，横向，自左向右

## 8.Web字体

@font-face 规则

Web 字体允许 Web 设计人员使用用户计算机上未安装的字体。

当您找到/购买了您想要使用的字体时，只需将字体文件包含在您的网络服务器上，它将在需要时自动下载给用户。

您的“自己的”字体在 CSS 规则内定义`@font-face`。

**不同的字体格式**

**TrueType 字体 (TTF)**

TrueType 是 Apple 和 Microsoft 于 20 世纪 80 年代末开发的一种字体标准。TrueType 是 Mac OS 和 Microsoft Windows 操作系统中最常用的字体格式。

**OpenType 字体 (OTF)**

OpenType 是一种可缩放计算机字体格式。它基于 TrueType 构建，是 Microsoft 的注册商标。OpenType 字体目前在主要计算机平台上广泛使用。

**Web 开放字体格式 (WOFF)**

WOFF 是一种用于网页的字体格式。它于 2009 年开发，现已成为 W3C 推荐标准。WOFF 本质上是 OpenType 或 TrueType，并带有压缩和附加元数据。其目标是支持在带宽受限的网络上将字体从服务器分发到客户端。

**Web 开放字体格式 (WOFF 2.0)**

TrueType/OpenType 字体提供比 WOFF 1.0 更好的压缩。

**SVG 字体/形状**

SVG 字体允许在显示文本时将 SVG 用作字形。SVG 1.1 规范定义了一个字体模块，允许在 SVG 文档中创建字体。您还可以将 CSS 应用于 SVG 文档，并且 @font-face 规则可应用于 SVG 文档中的文本。

**嵌入式 OpenType 字体 (EOT)**

EOT 字体是 Microsoft 设计的一种紧凑形式的 OpenType 字体，可用作网页上的嵌入字体。

**使用Web字体**

在`@font-face`规则中；首先为字体定义一个名称（例如 myFirstFont），然后指向字体文件。

**提示：**字体 URL 一定要使用小写字母。大写字母在 IE 中可能会产生意想不到的结果。

要将字体用于 HTML 元素，请通过以下属性引用字体的名称 (myFirstFont) `font-family`：

```css
@font-face {
  font-family: myFirstFont;
  src: url(sansation_light.woff);
}

div {
  font-family: myFirstFont;
}
```

**使用粗体文字**

必须添加另一条`@font-face`包含粗体文本描述符的规则：

```css
@font-face {
  font-family: myFirstFont;
  src: url(sansation_bold.woff);
  font-weight: bold;
}
```

## 9.CSS 2D变换

CSS 变换允许您移动、旋转、缩放和倾斜元素。

`transform`属性

`transform`属性值如下：

- `translate()`将元素从其当前位置移动（根据给定的 X 轴和 Y 轴的参数）

  `transform: translate(50px, 100px);`

- `rotate()`根据给定的度数顺时针或逆时针旋转元素（例如：20deg，负值将逆时针旋转）

  `transform: rotate(20deg);`

- `scaleX()`增加或减少元素的宽度

- `scaleY()`增加或减少元素的高度
- `scale()`增加或减少元素的大小（根据给出的宽度和高度参数）

  `transform: scale(2,3);` 宽度变为原始宽度的两倍，高度变为原始高度的三倍

- `skewX()`按给定的角度沿 X 轴倾斜元素
- `skewY()`按给定的角度沿 Y 轴倾斜元素
- `skew()`按给定的角度沿 X 轴和 Y 轴倾斜元素

  `transform: skem(20deg, 10deg);`

  如果未指定第二个参数，则其值为零。

- `matrix()`将所有二维变换方法合二为一

  matrix() 方法采用六个参数，包含数学函数，允许您旋转、缩放、移动（平移）和倾斜元素。

  参数如下：matrix(scaleX(), skewY(), skewX(), scaleY(), TranslationX(), TranslationY())

  `transform: matrix(1, -0.3, 0, 1, 0, 0);`

## 10.CSS 3D变换

利用 CSS`transform`属性，可以使用以下 3D 转换方法：

- `rotateX()`将元素绕其 X 轴以给定的角度旋转
- `rotateY()`将元素绕其 Y 轴以给定的角度旋转
- `rotateZ()`将元素绕其 Z 轴以给定的角度旋转

## 11.CSS过渡

CSS 过渡允许您在给定的时间内平滑地更改属性值。

- `transition`
- `transition-delay`
- `transition-duration`用于确定过渡效果持续的时间
- `transition-property`用于指定哪些 CSS 属性在其值发生变化时应该应用过渡效果
- `transition-timing-function`

要创建过渡效果，必须指定两件事：

- 想要添加效果的 CSS 属性
- 效果持续时间

**注意：**如果没有指定持续时间部分，则转换将不起作用，因为默认值为 0

`transition: width 2s;`宽度变化持续两秒

多个属性值

`transition: width 2s, height 4s;`宽度变化持续两秒，高度变化持续四秒

**指定过渡的速度曲线**

该`transition-timing-function`属性指定过渡效果的速度曲线。

transition-timing-function 属性可以具有以下值：

- `ease`- 指定一个过渡效果，先慢速开始，然后快速结束（这是默认设置）
- `linear`- 指定从开始到结束速度相同的过渡效果
- `ease-in`- 指定慢速启动的过渡效果
- `ease-out`- 指定缓慢结束的过渡效果
- `ease-in-out`- 指定缓慢开始和结束的过渡效果
- `cubic-bezier(n,n,n,n)`- 让您在三次贝塞尔函数中定义自己的值

**延迟过渡效果**

`transition-delay`属性指定过渡效果的延迟（以秒为单位）。

启动前有 1 秒的延迟`transition-deplay: 1s`

**过渡 + 变换**

`transition: width 2s, height 2s, transform 2s;`

**简写**

`transition: width 2s linear 1s;`

## 12.CSS动画

CSS 允许无需使用 JavaScript 即可实现 HTML 元素的动画！

- `@keyframes`
- `animation-name`动画名字
- `animation-duration`动画持续时间
- `animation-delay`延迟时间
- `animation-iteration-count`运行次数，`infinite`永不止息的运行下去
- `animation-direction`
- `animation-timing-function`
- `animation-fill-mode`
- `animation`

**什么是 CSS 动画？**

动画可以让元素逐渐从一种风格转变为另一种风格。

可以根据需要多次更改任意数量的 CSS 属性。

要使用 CSS 动画，必须首先为动画指定一些关键帧。

关键帧保存元素在特定时间将具有的样式。

**@keyframes 规则**

在@keyframes规则内指定 CSS 样式时，动画将在特定时间从当前样式逐渐变为新样式

要使动画正常工作，必须将动画绑定到元素。

以下示例将“example”动画绑定到 `<div>` 元素。动画将持续 4 秒，并将 `<div>` 元素的背景颜色从“红色”逐渐更改为“黄色”：

```css
/* The animation code */
@keyframes example {
  from {background-color: red;}
  to {background-color: yellow;}
}

/* The element to apply the animation to */
div {
  width: 100px;
  height: 100px;
  background-color: red;
  animation-name: example;
  animation-duration: 4s;
}
```

**注意：**该`animation-duration`属性定义动画需要多长时间才能完成。如果`animation-duration`未指定该属性，则不会发生动画，因为默认值为 0s（0 秒）。 

在上面的例子中，我们使用关键字“from”和“to”（代表 0％（开始）和 100％（完成））指定了样式何时改变。

也可以使用百分比。通过使用百分比，您可以添加任意数量的样式更改。

以下示例将在动画完成 25％、50％ 以及 100％ 时更改 `<div>` 元素的背景颜色：

```css
/* The animation code */
@keyframes example {
  0%   {background-color: red;}
  25%  {background-color: yellow;}
  50%  {background-color: blue;}
  100% {background-color: green;}
}

/* The element to apply the animation to */
div {
  width: 100px;
  height: 100px;
  background-color: red;
  animation-name: example;
  animation-duration: 4s;
}
```

**反向或交替循环运行动画**

`animation-direction`属性指定动画是否应正向播放、反向播放或交替播放。

animation-direction 属性可以具有以下值：

- `normal`- 动画正常播放（向前）。这是默认设置
- `reverse`- 动画以反向播放（向后）
- `alternate `- 动画先正向播放，然后倒向播放
- `alternate-reverse`- 动画先向后播放，然后向前播放

**指定动画的速度曲线**

`animation-timing-function`属性指定动画的速度曲线。

animation-timing-function 属性可以具有以下值：

- `ease`- 指定动画以慢速开始，然后快速，然后缓慢结束（这是默认设置）
- `linear`- 指定从开始到结束速度相同的动画
- `ease-in`- 指定慢速启动的动画
- `ease-out`- 指定以缓慢的速度结束的动画
- `ease-in-out`- 指定慢速开始和结束的动画
- `cubic-bezier(n,n,n,n)`- 让你在三次贝塞尔函数中定义自己的值

**指定动画的填充模式**

CSS 动画不会在播放第一个关键帧之前或播放最后一个关键帧之后影响元素。animation-fill-mode 属性可以覆盖此行为。

`animation-fill-mode`属性指定动画未播放时（开始前、结束后或两者）目标元素的样式。

animation-fill-mode 属性可以具有以下值：

- `none`- 默认值。动画在执行之前或之后不会对元素应用任何样式
- `forwards`- 元素将保留最后一个关键帧设置的样式值（取决于动画方向和动画迭代次数）
- `backwards`- 元素将获取第一个关键帧设置的样式值（取决于动画方向），并在动画延迟期间保留该值
- `both`- 动画将遵循向前和向后的规则，在两个方向上扩展动画属性

**简写**

```css
div {
  animation-name: example;
  animation-duration: 5s;
  animation-timing-function: linear;
  animation-delay: 2s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

/* 简写 */
div {
  animation: example 5s linear 2s infinite alternate;
}
```

## 13.CSS工具提示

当用户将鼠标指针移到元素上时，工具提示通常用于指定有关某些内容的额外信息

## 14.图像样式

**圆形图像**

使用`border-radius`属性创建圆形图像

**缩略图**

使用`border`属性来创建缩略图

**响应式图片**

```css
img {
  max-width: 100%;
  height: auto;
}
```

## 15.CSS滤镜（过滤器）

`filter`属性用于为元素添加视觉效果（如模糊和饱和度）。

在过滤器属性中，您可以使用以下 CSS 函数：

- `blur()`模糊，长度单位
- `brightness()`亮度，百分比
- `contrast()`对比度，百分比
- `drop-shadow()`阴影
- `grayscale()`灰度，百分比，0无效果，1完全灰度
- `hue-rotate()`颜色旋转
- `invert()`反转图像颜色，百分比，0无效果，1完全反转
- `opacity()`透明度，百分比，0完全透明，1无影响
- `saturate()`饱和度，百分比，0不饱和，1无影响，2饱和过度
- `sepia()`暖色，百分比，0无效果，1完全暖色

## 16.CSS图像镜像

`box-reflect`属性用于创建图像反射。

`box-reflect`属性的值可以是：

`below`下

`above`上

`left`左

`right`右

**偏移**

要指定图像和反射之间的间隙，请将间隙的大小添加到`box-reflect`属性中

**渐变**

镜像属性后加上渐变属性即可

## 17.CSS对象适应

`object-fit`属性用于指定如何调整 `<img>` 或 `<video>` 的大小以适合其容器

`object-fit`属性可以采用下列值之一：

- `fill`- 这是默认设置。图像会调整大小以填充给定尺寸。如有必要，图像会拉伸或压缩以适应
- `contain`- 图像保持其纵横比，但调整大小以适应给定的尺寸
- `cover`- 图像保持其纵横比并填充给定尺寸。图像将被剪裁以适合
- `none`- 图像未调整大小
- `scale-down`- 图像缩小到最小版本`none`或` contain`

## 18.CSS对象位置

`object-position`属性用于指定 `<img>` 或 `<video>` 在其容器内的位置。

`object-position: 80% 100%;`

与`object-fit`一起适应

## 19.CSS遮罩

可以创建一个遮罩层放置在元素上方，以部分或全部隐藏元素的各个部分

`mask-image`属性指定遮罩层图像

遮罩层图像可以是 PNG 图像、SVG 图像、CSS 渐变或 SVG  元素

要使用 PNG 或 SVG 图像作为遮罩层，请使用 url() 值传入遮罩层图像。

遮罩图像需要有透明或半透明区域。黑色表示完全透明。

`mask-repeat`属性指定是否或如何重复蒙板图像。`no-repeat` 值表示蒙板图像不会重复（蒙板图像仅显示一次）

使用渐变作为遮罩，代码则是将渐变代码作为属性值写在`mask-image`中

## 20.CSS按钮

`background-color`属性来改变按钮的背景颜色

`font-size`属性来改变按钮的字体大小

`padding`属性来更改按钮的填充

`border-radius`属性为按钮添加圆角

`border`属性为按钮添加彩色边框

`:hover`选择器可以改变按钮悬停的样式

`transition-duration`属性来确定“悬停”效果的速度

`box-shadow`属性为按钮添加阴影

`opacity`属性为按钮添加透明度（创建“禁用”外观）

`cursor`属性值为`not-allowed`，这样当您将鼠标悬停在按钮上时就会显示“禁止停车标志”

`width`属性可以更改按钮的宽度

`float:left`按钮之间相邻浮动

`display:block`而不是`float:left`将按钮分组到彼此下方，而不是并排放置

## 21.CSS分页

使用 CSS 创建响应式分页

`.active`活动页，或者说当前页的特殊样式

`:hover` 选择器在鼠标移动到每个页面链接上时更改其颜色

`border-radius`想要一个圆形的“活动”和“悬停”按钮

`transition`到页面链接以创建悬停时的过渡效果

`border`属性为分页添加边框

**圆角边框**

**提示：**在分页中的第一个和最后一个链接添加圆角边框

**链接之间的空间**

**提示：**`margin`如果不想对页面链接进行分组

`font-size`调整字体大小

`text-align:center`调整对齐方式

分页的另一种变体是所谓的“面包屑”

## 22.CSS多列

CSS 多列布局允许轻松定义多列文本 - 就像报纸一样

- `column-count`列数
- `column-gap`列之间的间隙
- `column-rule-style`列之间的样式（似边框）
- `column-rule-width`列之间线的宽度
- `column-rule-color`列之间线的颜色
- `column-rule`简写（宽度、样式和颜色）
- `column-span`指定元素应跨越多少列
- `column-width`指定列宽

## 23.CSS用户界面

- `resize`指定元素是否（以及如何）可由用户调整大小
  -  `horizontal` 仅允许用户调整元素的宽度
  -  `vertical` 仅允许用户调整元素的高度
  -  `both` 允许用户调整高度和宽度
  - `none` 在许多浏览器中， `<textarea>` 默认是可调整大小的。在这里，我们使用了 resize 属性来禁用可调整大小功能：

- `outline-offset` 轮廓偏移
  - **注意：**轮廓不同于边框！与边框不同，轮廓绘制在元素边框之外，可能与其他内容重叠。此外，轮廓不是元素尺寸的一部分；元素的总宽度和高度不受轮廓宽度的影响。
  - 使用`outline-offset`属性在边框和轮廓之间添加空间

## 24.CSS变量

`var()`函数用于插入 CSS 变量的值

CSS 变量可以访问 DOM，这意味着您可以创建具有本地或全局范围的变量、使用 JavaScript 更改变量以及根据媒体查询更改变量。

使用 CSS 变量的一个好方法是设计颜色。您可以将颜色放入变量中，而不必一遍又一遍地复制和粘贴相同的颜色。

`var()`函数的语法如下：

**var(--*name, value*)**

| Value   | Description                                                  |
| :------ | :----------------------------------------------------------- |
| *name*  | Required. The variable name (must start with two dashes)     |
| *value* | Optional. The fallback value (used if the variable is not found) |

**注意：**变量名必须以两个破折号（--）开头，并且区分大小写！

**var() 的工作原理**

首先：CSS 变量可以具有全局或局部范围。

全局变量可以通过整个文档访问/使用，而局部变量只能在声明它的选择器内使用。

要创建具有全局作用域的变量，请在`:root` 选择器内声明它。`:root`选择器与文档的根元素匹配。

要创建具有局部范围的变量，请在将要使用它的选择器内声明它。

```css
:root {
  --blue: #1e90ff;
}

body { 
    background-color: var(--blue); 
}
```

使用 var() 的优点是：

- 使代码更容易阅读（更容易理解）
- 使更改颜色值变得更加容易

---

**使用局部变量覆盖全局变量**

全局变量可以通过整个文档访问/使用，而局部变量只能在声明它的选择器内使用

有时我们希望变量仅在页面的特定部分发生变化

**如果在局部想要更改全局声明的变量，则只需要在局部重新声明同名的变量，即可实现覆盖的效果**

---

**使用 JavaScript 更改变量**

CSS 变量可以访问 DOM，这意味着您可以使用 JavaScript 更改它们。

```javascript
var r = document.querySelector(':root');

function myFunction_get() {
  var rs = getComputedStyle(r);
  alert("The value of --blue is: " + rs.getPropertyValue('--blue'));
}

function myFunction_set() {
  r.style.setProperty('--blue', 'lightblue');
}
```

---

**在媒体查询中使用变量**

现在我们想要改变媒体查询中的变量值。

**提示：**媒体查询是关于为不同的设备（屏幕、平板电脑、手机等）定义不同的样式规则。

`@media`规则

## 25.CSS @property 规则

CSS @property 规则

`@property`规则用于直接在样式表中定义自定义 CSS 属性，而无需运行任何 JavaScript。

`@property`规则具有数据类型检查和约束，设置默认值，并定义属性是否可以继承值。

定义自定义属性的示例：

```css
@property --myColor {
  syntax: "<color>";
  inherits: true;
  initial-value: lightgray;
}
```

上面的定义表明--myColor是一个颜色属性，它可以从父元素继承值，其默认值是lightgray。

要在 CSS 中使用自定义属性，我们使用以下`var()` 函数：

```css
body {
  backgound-color: var(--myColor);
}
```

使用`@property`的好处：

- **类型检查：**必须指定自定义属性的数据类型，例如 `<number>`、`<color>`、`<length>` 等。这可以防止错误并确保正确使用自定义属性
- **设置默认值：**为自定义属性设置默认值。这可确保如果稍后分配了无效值，浏览器将使用定义的后备值
- **设置继承行为：**必须指定自定义属性是否可以从其父元素继承值

**通过类型检查和后备值避免错误**

## 26.CSS盒子尺寸

`box-sizing`属性允许我们将填充和边框包含在元素的总宽度和高度中

默认情况下，元素的宽度和高度计算如下：

宽度 + 内边距 + 边框 = 元素的实际宽度
高度 + 内边距 + 边框 = 元素的实际高度

这意味着：当您设置元素的宽度/高度时，该元素通常看起来比您设置的更大（因为元素的边框和填充被添加到元素指定的宽度/高度）。

**`box-sizing`属性允许我们将填充和边框包含在元素的总宽度和高度中**

如果在元素上设置`box-sizing: border-box;`，则填充和边框将包含在宽度和高度中

由于使用的效果`box-sizing: border-box;`要好得多，许多开发人员希望他们页面上的所有元素都能以这种方式工作。

则会这样写：

```css
* {
  box-sizing: border-box;
}
```

## 27.CSS媒体查询

CSS2 中引入的规则`@media`使得可以为不同的媒体类型定义不同的样式规则。

CSS3 中的媒体查询扩展了 CSS2 媒体类型的思想：它们不再查找设备类型，而是查找设备的功能。

媒体查询可用于检查许多事情，例如：

- 视口的宽度和高度
- 视口方向（横向或纵向）
- 解决

使用媒体查询是一种向台式机、笔记本电脑、平板电脑和手机（如 iPhone 和 Android 手机）提供定制样式表的流行技术。

**CSS 媒体类型**

| Value  | Description                                           |
| :----- | :---------------------------------------------------- |
| all    | Used for all media type devices                       |
| print  | Used for print preview mode                           |
| screen | Used for computer screens, tablets, smart-phones etc. |

**CSS 常见媒体功能**

| Value       | Description                                        |
| :---------- | :------------------------------------------------- |
| orientation | Orientation of the viewport. Landscape or portrait |
| max-height  | Maximum height of the viewport                     |
| min-height  | Minimum height of the viewport                     |
| height      | Height of the viewport (including scrollbar)       |
| max-width   | Maximum width of the viewport                      |
| min-width   | Minimum width of the viewport                      |
| width       | Width of the viewport (including scrollbar)        |

**媒体查询语法**

媒体查询由媒体类型组成，可以包含一个或多个媒体特征，这些特征可以解析为真或假。

```css
@media not|only mediatype and (media feature) and (media feature) {
  CSS-Code;
}
```

mediatype是可选的（如果省略，*它将*被设置为 all）。但是，如果您使用**not**或**only**，您还必须指定 *mediatype*。

如果指定的媒体类型与显示文档的设备类型匹配，并且媒体查询中的所有媒体功能都为真，则查询结果为真。当媒体查询为真时，将应用相应的样式表或样式规则，遵循正常的级联规则。

**not**、**only**和**and**关键字的含义：

**not：**这个关键字颠倒了整个媒体查询的含义。

**only：**此关键字可防止不支持媒体查询的旧版浏览器应用指定的样式。 **它对现代浏览器无效。**

**and：**这个关键字结合了一种媒体类型和一个或多个媒体特征。

## 28.CSS 弹性盒子

**Flexbox** 布局模块

在 Flexbox 布局模块之前，有四种布局模式：

- Block，块，用于网页中的部分
- Inline，内联，用于文本
- Table，表，用于二维表格数据
- Positioned，定位，用于元素的明确位置

灵活的框布局模块，可以更轻松地设计灵活的响应式布局结构，而无需使用浮动或定位。

**弹性框元素**

要开始使用 Flexbox 模型，您需要首先定义一个 Flex 容器。

`display`通过将属性设置为以下内容， 弹性容器将变得灵活`flex`：

```css
.flex-container {
  display: flex;
}
```

弹性容器的属性如下：

- `flex-direction`想要堆叠弹性项目的方向
  - `row`默认，该属性值表示主轴方向为水平方向，并且子元素从左到右排列。这是最常见的布局方式，类似于文本的默认排列方向。在这种模式下，交叉轴是垂直方向，与主轴垂直相交。
  - `row-reverse`主轴方向仍然是水平方向，但子元素的排列顺序是从右到左。这种方式与`row`相反，适用于需要反向排列元素的场景，比如某些从右向左阅读的语言环境或者需要特殊视觉效果的布局。
  - `column`主轴方向变为垂直方向，子元素从上到下排列。这种布局方式适合创建垂直方向的布局，如侧边栏或者垂直的内容列表。此时交叉轴是水平方向。
  - `column-reverse`主轴方向为垂直方向，但子元素的排列顺序是从下到上。这与`column`相反，可用于一些特殊的设计需求，比如在某些艺术设计或者需要逆序展示垂直元素的场景中。
- `flex-wrap`指定弹性项目是否应换行
  - `nowrap`默认，不换行
  - `wrap`换行
  - `wrap-reverse`反方向换行
- `flex-flow`上面两个属性（方向和换行）的简写
- `justify-content`对齐
  - `flex-start`表示子元素在主轴的起始位置对齐
  - `flex-end`子元素在主轴的末尾位置对齐
  - `center`子元素在水平方向居中对齐
  - `space-between`子元素在主轴方向上均匀分布，并且第一个子元素在主轴起始位置，最后一个子元素在主轴末尾位置。相邻子元素之间的间隔相等，这个间隔的大小是根据容器剩余空间和子元素数量动态计算的。
  - `space-around`子元素在主轴方向上均匀分布，并且每个子元素的两侧都有相同的间隔。这个间隔的大小也是根据容器剩余空间和子元素数量动态计算的，但与`space - between`不同的是，`space - around`在容器两端也会有间隔，使得子元素看起来像是被间隔 “包围” 着。
- `align-items`对齐
  - `center`将弹性项目对齐到容器的中间
  - `flex-start` 将弹性项目对齐到容器的顶部
  - `flex-end`将弹性项目与容器的底部对齐
  - `stretch`会拉伸弹性项目以填充容器（这是默认值）
  - `baseline`将弹性项目与其基线对齐
- `align-content` 对齐flex line(弹性线)
  - `space-between`显示弹性线之间相等间距
  - `space-around`显示弹性线及其前、中、后的空间
  - `stretch`拉伸柔性线以占据剩余空间（这是默认值）
  - `center`在容器的中间显示弹性线

---

**子元素（项目）**

弹性容器的直接子元素自动成为弹性（flex）项目。

弹性项目的属性包括：

- `order`指定弹性项目的顺序，必须是数字，默认值为 0。
- `flex-grow`指定弹性项目相对于其余弹性项目的增长量，权重
- `flex-shrink`指定弹性项目相对于其余弹性项目收缩的程度，值必须是数字，默认值为 1。
- `flex-basis`指定弹性项目的初始长度。
- `flex`简写属性，` flex-grow`、`flex-shrink`、`flex-basis`
- `align-self`指定灵活容器内选定项目的对齐方式，`align-self `属性将覆盖容器`align-items`属性设置的默认对齐方式

---

**响应式弹性框**

@media 规则

## 29.CSS响应式

**什么是响应式网页设计？**

响应式网页设计使您的网页在所有设备上看起来都很好。

响应式网页设计仅使用 HTML 和 CSS。

响应式网页设计不是一个程序或者 JavaScript。

当您使用 CSS 和 HTML 来调整内容大小、隐藏、缩小、放大或移动内容以使其在任何屏幕上看起来不错时，这称为响应式网页设计。

---

**什么是视口？**

视口是网页中用户可见的区域。

视口随设备而变化，在手机上会比在电脑屏幕上小。

在平板电脑和手机出现之前，网页仅适用于电脑屏幕，并且网页通常具有静态设计和固定大小。

然后，当我们开始使用平板电脑和手机上网时，固定尺寸的网页太大，无法适应屏幕。为了解决这个问题，这些设备上的浏览器会缩小整个网页以适应屏幕。

这并不完美！！但可以快速修复。

**设置视口**

HTML5 引入了一种方法，让网页设计师通过标签来控制视口 `<meta>`。

`<meta>`您应该在所有网页中包含以下视口元素：

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

这为浏览器提供了如何控制页面尺寸和缩放的指令。

`width=device-width`部分将页面的宽度设置为跟随设备的屏幕宽度（这将根据设备而变化）

`initial-scale=1.0`部分设置浏览器首次加载页面时的初始缩放级别

**根据视口调整内容大小**

用户习惯在桌面和移动设备上垂直滚动网站 - 但不会水平滚动！

因此，如果用户被迫水平滚动或缩小才能查看整个网页，则会导致糟糕的用户体验。

需要遵循的一些附加规则：

**1. 请勿使用较大的固定宽度元素 -**例如，如果图像的显示宽度大于视口，则会导致视口水平滚动。请记住调整此内容以适应视口的宽度。

**2. 不要让内容依赖特定的视口宽度来良好地呈现**- 由于不同设备的屏幕尺寸和 CSS 像素宽度差异很大，因此内容不应依赖特定的视口宽度来良好地呈现。

**3. 使用 CSS 媒体查询为小屏幕和大屏幕应用不同的样式**- 为页面元素设置较大的绝对 CSS 宽度会导致元素对于较小设备的视口来说太宽。相反，请考虑使用相对宽度值，例如 width: 100%。此外，请谨慎使用较大的绝对定位值。这可能会导致元素超出小型设备的视口。

---

**什么是网格视图？**

许多网页都是基于网格视图的，这意味着页面被分为几列：

在设计网页时使用网格视图非常有用。它使在页面上放置元素变得更容易。

响应式网格视图通常有 12 列，总宽度为 100%，并且会随着您调整浏览器窗口大小而缩小和扩大。

**构建响应式网格视图**

让我们开始构建一个响应式网格视图。

首先确保所有 HTML 元素都已将`box-sizing`属性设置为 `border-box`。这可确保元素的总宽度和高度中包含填充和边框。

在您的 CSS 中添加以下代码：

```css
* {
  box-sizing: border-box;
}
```

我们希望使用具有 12 列的响应式网格视图，以便对网页进行更好的控制。

首先我们必须计算一列的百分比：100%/12 列 = 8.33%。

然后我们为 12 列中的每一列创建一个类，`class="col-"`并使用一个数字来定义该部分应跨越多少列

**媒体查询**

媒体查询是CSS3中引入的一项CSS技术。

`@media`仅当某个条件为真时，它才使用该规则来包含一组 CSS 属性。

如果浏览器窗口小于或等于 600px，背景颜色将为浅蓝色：

```css
@media only screen and (max-width: 600px) {
  body {
    background-color: lightblue;
  }
}
```

**添加断点**

我们制作了一个有行和列的网页，它具有响应性，但在小屏幕上看起来并不好。

媒体查询可以帮到我们。我们可以添加一个断点，设计中的某些部分在断点两侧的行为会有所不同。

**始终为移动设备优先进行设计**

移动优先意味着在为桌面或任何其他设备进行设计之前，先为移动设备进行设计（这将使页面在较小的设备上显示速度更快）。

这意味着我们必须对 CSS 进行一些更改。

当宽度小于 768px 时，我们不应该更改样式*，而应该在宽度**大于*768px时更改设计。这将使我们的设计移动优先

**另一个断点**

您可以根据需要添加任意数量的断点。

我们还将在平板电脑和手机之间插入一个断点。

**典型的设备断点**

屏幕和设备的数量众多，高度和宽度各不相同，因此很难为每种设备创建精确的断点。为简单起见，您可以针对以下五组设备

```css
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...}
```

**方向：纵向 / 横向**

媒体查询还可用于根据浏览器的方向改变页面的布局。

您可以拥有一组仅在浏览器窗口的宽度大于其高度时才适用的 CSS 属性，即所谓的“横向”方向

**使用媒体查询隐藏元素**

媒体查询的另一个常见用途是隐藏不同屏幕尺寸上的元素

```css
/* If the screen size is 600px wide or less, hide the element */
@media only screen and (max-width: 600px) {
  div.example {
    display: none;
  }
}
```

**使用媒体查询更改字体大小**

您还可以使用媒体查询来更改不同屏幕尺寸上的元素的字体大小

**响应式网页设计 -图片**

如果`width`属性设置为百分比，并且该`height`属性设置为“自动”，则图像将响应并放大和缩小

在许多情况下，更好的解决方案是使用属性 `max-width`

**使用 max-width 属性**

如果`max-width`属性设置为 100%，则图像会在必要时缩小，但绝不会放大到大于其原始尺寸

**背景图像**

背景图像也可以响应调整大小和缩放。

`background-size`属性设置为“contain”，背景图像将缩放，并尝试适应内容区域。但是，图像将保持其纵横比（图像宽度和高度之间的比例关系）

`background-size`属性设置为“100% 100%”，背景图片会拉伸覆盖整个内容区域

`background-size`属性设置为“cover”，背景图像将缩放以覆盖整个内容区域。请注意，“cover”值保持纵横比，并且背景图像的某些部分可能会被剪裁

**不同设备使用不同图像**

大图像在大型计算机屏幕上可能非常完美，但在小型设备上却毫无用处。既然必须缩小图像，为什么还要加载大图像呢？为了减少负载或出于任何其他原因，您可以使用媒体查询在不同设备上显示不同的图像。

您可以使用媒体查询`min-device-width`，而不是`min-width`，它检查设备宽度，而不是浏览器宽度。这样，当您调整浏览器窗口大小时，图像将不会改变

**HTML `<picture> `元素**

HTML`<picture>`元素为 Web 开发人员提供了更灵活的指定图像资源的能力。

该元素最常见的用途`<picture>` 是用于响应式设计中的图像。无需根据视口宽度放大或缩小一张图片，可以设计多张图片以更好地填充浏览器视口。

元素的`<picture>`工作原理与`<video>`和 `<audio>`元素类似。您可以设置不同的源，第一个符合偏好的源就是正在使用的源

```html
<picture>
  <source srcset="img_smallflower.jpg" media="(max-width: 400px)">
  <source srcset="img_flowers.jpg">
  <img src="img_flowers.jpg" alt="Flowers">
</picture>
```

`srcset`属性是必需的，并定义图像的来源。

**响应式网页设计 -视频**

`max-width`

**响应式网页设计 -框架**

有许多免费的 CSS 框架提供响应式设计。

例如：Bootstrap

**响应式网页设计 -模板**

网站模板

可以自由地在所有项目中修改、保存、共享和使用它们

## 30.CSS网格

CSS 网格布局模块提供了基于网格的布局系统，具有行和列，使得设计网页变得更容易，而无需使用浮动和定位。

网格元素

网格布局由一个父元素和一个或多个子元素组成。

当 HTML 元素的属性`display`设置为 `grid`或`inline-grid`时，该元素将成为网格容器。

```css
.grid-container {
  display: grid;
}
```

网格容器的所有直接子项都会自动成为*网格项目*。

网格列：网格项的垂直线称为*列*。column

网格行：网格项的水平线称为*行*。row

网格间隙：每列/行之间的空间称为*间隙*。column gap

您可以使用以下属性之一来调整间隙大小：

- `column-gap`
- `row-gap`
- `gap`

**网格线**

列与列之间的线称为*列线*。column lines

行与行之间的线称为*行线*。row lines

**CSS网格容器**

要使 HTML 元素表现为网格容器，必须将`display`属性设置为` grid`或`inline-grid`。

网格容器由放置在列和行内的网格项组成。

**grid-template-columns 属性**

`grid-template-columns`属性定义网格布局中的列数，并且可以定义每列的宽度。

属性值是一个空格分隔的列表，其中每个值定义相应列的宽度。

`grid-template-columns`属性还可用于指定列的大小（宽度）

**grid-template-rows 属性**

`grid-template-rows`属性定义每行的高度。

属性值是一个空格分隔的列表，其中每个值定义相应行的高度。

**justify-content 属性**

`justify-content`属性用于对齐容器内的整个网格。

**注意：**网格的总宽度必须小于容器的宽度，该`justify-content`属性才能发挥作用。

**align-content 属性**

`align-content`属性用于*垂直*对齐容器内的整个网格。

**注意：**网格的总高度必须小于容器的高度，该`align-content`属性才能生效。

---

**网格项**

网格*容器*包含网格*项*。

默认情况下，容器的每一行每一列都有一个网格项，但您可以设置网格项的样式，使它们跨越多列和/或多行

**grid-column 属性**

`grid-column`属性定义在哪一列放置项目。

定义项目从哪里开始，以及项目从哪里结束。

**注意：**属性是和属性`grid-column`的简写属性。`grid-column-start``grid-column-end`

要放置一个项目，您可以参考*行号*，或者使用关键字“span”来定义该项目将跨越多少列。

**grid-row 属性：**

`grid-row`属性定义在哪一行放置项目。

定义项目从哪里开始，以及项目从哪里结束。

**注意：**属性是和属性`grid-row`的简写属性。`grid-row-start``grid-row-end`

要放置项目，您可以参考*行号*，或使用关键字“span”来定义该项目将跨越多少行

**grid-area 属性**

属性`grid-area`可用作 `grid-row-start`、`grid-column-start`和`grid-row-end`属性的简写属性`grid-column-end`。

**命名网格项**

`grid-area`属性还可用于为网格项分配名称。

`grid-template-areas`命名的网格项可以通过网格容器的属性来引用。

每行由撇号 (' ') 定义

每行中的列在撇号内定义，并以空格分隔。

**注意：**句点符号表示没有名称的网格项。

**物品的顺序**

网格布局允许我们将项目放置在我们喜欢的任何位置。

HTML 代码中的第一个项目不必作为网格中的第一个项目出现。

## 31.Sass

**什么是 Sass？**

- **Sass**代表**语法**上**很棒**的 **样式表**
- Sass 是 CSS 的扩展
- Sass 是一个 CSS 预处理器
- Sass 与所有版本的 CSS 完全兼容
- Sass 减少 CSS 的重复，从而节省时间
- Sass 由 Hampton Catlin 设计，并由 Natalie Weizenbaum 于 2006 年开发
- Sass 可以免费下载和使用

**为什么要使用 Sass？**

样式表越来越大、越来越复杂，维护起来也越来越困难。这时 CSS 预处理器就可以派上用场了。

Sass 允许您使用 CSS 中不存在的功能，如变量、嵌套规则、混合、导入、继承、内置函数和其他内容。

Sass 官方网站  https://sass-lang.com/

