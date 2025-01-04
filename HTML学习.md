# HTML学习

## 1.简单结构

`<!DOCTYPE html>` 声明为html5文档

`<html>`html页面根元素

`<head>`头部元素

包含`<meta>`标签、`<title>`标签、`<link>`标签、`<script>`标签(js)、`<style>`标签(css)

`<meta charset = "utf-8">`

`<body>`标签

包含`<h1>`标签、`<p>`标签、等等……

html标签和html元素是一个意思

## 2.html标题

`<h1>`~`<h6>`

## 3.html段落

`<p>`

## 4.html链接

`<a href = "https://www.github.com">github</a>`

## 5.html图像

`<img src = "/src/pic/demo.png" />`

## 6.html元素和属性

标签成对出现，开始标签和结束标签

元素的内容就是标签间的部分

大多数html元素都有属性

html标签可以嵌套

html属性写在标签内

大多数html标签有以下四种属性

`id` 定义html元素的唯一id

`class`为html元素指定一个或多个类名，在css中用类选择器来使用(点`.`后跟着类名)

`<style>`规定html元素的行内样式

`title`属性用于提供关于html元素的额外信息，这些信息通常以工具提示（tooltip）的形式显示。当用户将鼠标悬停在元素上时，浏览器会显示一个包含`title`属性值的小弹出框

## 7.注释

`<!-- -->`

## 8.一些标签

`<hr>`水平分割线

`<br>`换行

`<b>`加粗，`<strong>`标签具有强调的语义。它告诉浏览器和搜索引擎等，被包裹的内容是重要的、需要强调的部分

`<i>`斜体，`<em>`标签则带有强调的语义，不过它强调的是一种语气上的变化

## 9.表格

`<table>`标签

`<tr>`行，标题行(列头)`<th>`

`<td>`列

## 10.html列表

`<ul>`嵌套`<li>`无序列表

`<ol>`嵌套`<li>`有序列表

`<dl>`嵌套（`<dt>`嵌套`<dd>`）自定义列表

## 11.区块元素

`<div>`块级元素，块级元素在网页中会独占一行，从新的一行开始，并且会自动填满其父元素的宽度（除非设置了宽度属性）

`<span>`内联元素，内联元素不会独占一行，它会在一行中按照从左到右的顺序排列，并且其宽度和高度属性默认情况下不会生效，它的大小由其内容的大小决定

## 12.表单

`<form>`标签，`action`属性定义了表单提交的URL，`method`属性定义了提交数据的HTTP方法

`<label>`和`<input>`，标签和输入框

`<select>`下拉列表，`<option>`选项

不同的input标签

`<input type="text">`，文本域

`<input type="password">`，密码框

`<input type="radio">`，单选按钮

`<input type="checkbox">`，复选框

`<input type="submit">`，提交按钮

## 13.html框架

`<iframe>`，其实就是一个html网页**嵌套**另一个html网页

## 14.URL 统一资源定位器

**scheme`://`host.domain`:`port`/`path`/`filename**

- scheme - 定义因特网服务的类型。最常见的类型是 http

- host - 定义域主机（http 的默认主机是 www）

- domain - 定义因特网域名，比如 github.com
- :port - 定义主机上的端口号（http 的默认端口号是 80）
- path - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
- filename - 定义文档/资源的名称

## 15.XHTML

XHTML 是以 XML 格式编写的 HTML，更严格更纯净的 HTML 版本，2001年1月发布的 W3C 推荐标准

与 HTML 相比最重要的区别：

文档结构

- XHTML DOCTYPE 是*强制性的*
- `<html>` 中的 XML namespace 属性是*强制性的*
- `<html>`、`<head>`、`<title>` 以及 `<body>` 也是*强制性的*

元素语法

- XHTML 元素必须*正确嵌套*
- XHTML 元素必须始终*关闭*
- XHTML 元素必须*小写*
- XHTML 文档必须有*一个根元素*

属性语法

- XHTML 属性必须使用*小写*
- XHTML 属性值必须用*引号包围*
- XHTML 属性最小化也是*禁止的*

## 16.HTML5 【2014年10月】

新元素：

`<canvas>`画布

`<video>`视频，和`<audio>`音频

特殊内容元素：

`<article>`元素用于表示文档、页面或者应用程序中独立的、完整的、可被外部引用的内容块。它可以是一篇博客文章、一个新闻报道、一个论坛帖子、一个用户评论等

`<header>`元素用于定义文档或者文档的一部分（如一个`<section>`或`<article>`元素）的头部部分。它通常包含标题、导航栏或者一些介绍性的内容，**`<header>`嵌套在`<article>`中**

`<section>`元素用于定义文档中的一个章节或者一个主题相关的内容区域

`<nav>`元素用于定义网页的导航区域

`<footer>`元素用于定义网页的底部区域

新的表单控件：

`<input type="date">`（日期选择器）

`<input type="time">`（时间选择器）

`<input type="email">`（电子邮件输入框）

`<input type="search">`（搜索输入框）

`<input type="url">`（URL输入框）

完全支持CSS3

## 17.SVG 

`<svg>`是什么？

- SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
- SVG 用于定义用于网络的基于矢量的图形
- SVG 使用 XML 格式定义图形
- SVG 图像在放大或改变尺寸的情况下其图形质量不会有损失
- SVG 是万维网联盟的标准

SVG 是一种使用 XML 描述 2D 图形的语言。

Canvas 通过 JavaScript 来绘制 2D 图形。

## 18.html5 MathML

`<math>……</math>`

更好的集成 MathML（数学标记语言）的方式，用于在网页中呈现复杂的数学公式和表达式

MathML 是一种基于 XML 的语言，专门用于描述数学符号和表达式，它允许精确地表示数学内容，包括公式、方程式、矩阵等多种数学对象。

`<math xmlns="http://www.w3.org/1998/Math/MathML">`

## 19.html拖放

Drag 和 Drop

设置被拖放元素（draggable）:

`<div draggable="true">元素</div>`

基本的文本元素外，图像（`<img>`）等其他元素也可以设置为可拖放的

定义拖放事件监听器：

对于拖放操作，有一系列的事件需要监听。主要包括`dragstart`、`drag`、`dragenter`、`dragover`、`dragleave`、`drop`和`dragend`等事件

**`dragstart`事件**：当开始拖动一个元素时触发

**`dragover`事件**：当被拖放的元素在目标元素（放置元素）上方移动时触发

**`drop`事件**：当被拖放的元素放置到目标元素上时触发

拖动什么 - ondragstart **事件**和 setData()

放到何处 - ondragover**事件**

进行放置 - ondrop**事件**

## 20.地理位置

**检查浏览器支持**：

```javascript
	if (navigator.geolocation) {
		console.log("浏览器支持地理位置定位");
	} else {
		console.log("浏览器不支持地理位置定位");
	}
```

**获取位置信息**：如果浏览器支持，就可以使用`navigator.geolocation.getCurrentPosition()`方法来获取用户的当前位置。这个方法接受两个回调函数作为参数，一个是成功获取位置后的回调函数，另一个是获取位置出错时的回调函数

**监视位置变化（watchPosition）**

## 21.video

HTML5 的`<video>`标签用于在网页中嵌入视频内容，它提供了一种标准的方式来播放视频，无需依赖浏览器插件（如 Flash），使得视频播放更加稳定、高效且具有更好的跨浏览器兼容性

`src`属性，指定视频文件的来源，可以是本地文件路径，也可以是网络上的视频链接

`controls`属性，该属性用于在视频播放器中显示控制条，包括播放 / 暂停按钮、音量调节、进度条等

`autoplay`属性，使视频在页面加载完成后自动开始播放

`loop`属性，循环播放

`muted`属性，静音播放

`poster`属性，用于指定视频播放前显示的封面图片，当视频还未开始播放或者在加载过程中，会显示这个封面图片。图片的路径可以是本地路径或者网络路径

支持的视频格式：

- MP4 = 带有 H.264 视频编码和 AAC 音频编码的 MPEG 4 文件
- WebM = 带有 VP8 或 VP9 视频编码和 Vorbis 或 Opus 音频编码的 WebM 文件
- Ogg = 带有 Theora 视频编码和 Vorbis 音频编码的 Ogg 文件

**`<source>`标签**，视频源

**获取视频播放状态和进度信息**：

可以通过`videoElement.readyState`属性获取视频的准备状态（如`0`表示未初始化，`1`表示已加载元数据，`2`表示已加载部分数据，`3`表示已加载足够数据可以开始播放，`4`表示全部加载完成）。

通过`videoElement.currentTime`属性可以获取当前播放时间，通过`videoElement.duration`属性可以获取视频总时长。

## 22.Audio

HTML5 的`<audio>`标签用于在网页中嵌入音频内容

`src`属性，用于指定音频文件的来源，和`<video>`标签类似

`controls`属性，这个属性用于在音频播放器中显示控制条，包括播放 / 暂停按钮、音量调节等

`autoplay`属性，自动播放

`loop`属性，循环播放

`muted`属性，静音播放

**`<source>`标签**，音频源

**支持的音频格式**：

- **MP3（MPEG - 1 Audio Layer 3）**：这是一种非常流行的音频格式，被广泛支持
- **WAV（Waveform Audio File Format）**：这是一种无损音频格式，通常用于高质量的音频存储和播放
- **Ogg Vorbis**：这是一种开放标准的音频格式，具有较好的压缩比和音质

**获取音频播放状态和进度信息**：

可以通过`audioElement.readyState`属性获取音频的准备状态（如`0`表示未初始化，`1`表示已加载元数据，`2`表示已加载部分数据，`3`表示已加载足够数据可以开始播放，`4`表示全部加载完成）

通过`audioElement.currentTime`属性可以获取当前播放时间，通过`audioElement.duration`属性可以获取音频总时长

## 23.表单控件

新的表单控件：

`<input type="date">`（日期选择器）

`<input type="time">`（时间选择器）

`<input type="email">`（电子邮件输入框）

`<input type="search">`（搜索输入框）

`<input type="url">`（URL输入框）

之前写过的，下面还有：

`<input type="color">`（颜色选择器）

`<input type="datetime">`（日期时间输入框）

`<input type="datetime-local">`（年月日时间选择器 (无时区)）

`<input type="month">`（年月选择器 (无时区)）

`<input type="week">`（年周选择器 (无时区)）

`<input type="number" min="1" max="5">`（数字选择器）

## 24.表单新元素

**`<datalist>`元素**：输入选择器

`<datalist>`元素用于为`<input>`元素提供一个预定义的选项列表，当用户在`<input>`元素中输入时，浏览器会根据输入的内容显示匹配的选项，帮助用户更快地完成输入

它主要用于创建自动完成的输入框，提升用户体验，通常用于表单中，如搜索框、输入地名、产品名称等场景

**`<output>`元素**：

`<output>`元素用于在网页中表示计算或用户操作的结果。

它通常与 JavaScript 一起使用，用于显示表单数据经过计算后的结果、脚本执行后的输出等。

`oninput`事件，计算不同输出数据

~~**`<keygen>`元素**：~~

标签规定用于表单的密钥对生成器字段，由于安全问题已~~被弃用~~

## 25.表单属性

**`<form>` /` <input>` 的`autocomplete` 属性：**

自动填充，属性值有`on`和`off`

**`<form>` 的`novalidate` 属性：**

用于设置浏览器不对表单进行验证

**`<input>` 的`autofocus` 属性：**

自动聚焦，属性值为布尔属性

**`<input>` 的`form`属性：**

表明属于的form，即使不在表单form内，属性值是字符串（表单的id）

**`<input>` 的`formenctype` 属性：**

描述了表单提交到服务器的数据编码 (只对form表单中 `method="post"` 表单)，submit的属性

**`<input>` 的`formmethod` 属性：**

定义了表单提交的方式，覆盖了 `<form>` 元素的 `method` 属性，可以与 `type="submit"` 和 `type="image"` 配合使用

**`<input>`的 `formnovalidate` 属性：**

不验证提交，属性是一个 布尔属性，与 `type="submit"` 一起使用

**`<input>`的 `formtarget` 属性：**

指定一个名称或一个关键字来指明表单提交数据接收后的展示，覆盖 `<form>`元素的`target`属性，与 `type="submit"` 和 `type="image"` 配合使用

**`<input>` 的`height` 和 `width` 属性：**

规定用于 image 类型的 `<input>` 标签的图像高度和宽度，只适用于 image 类型的`<input>` 标签

**`<input>`的 `list` 属性：**

规定输入域的 datalist，datalist 是输入域的选项列表，datalist的**归属列表**

**`<input>`的 `min` 和 `max` 属性：**

min、max 和 step 属性用于为包含数字或日期的 input 类型规定限定（约束）

**注意:** min、max 和 step 属性适用于以下类型的 `<input>` 标签：date pickers、number 以及 range

**`<input>`的 `multiple` 属性：**

`multiple` 属性是一个布尔属性，规定`<input>` 元素中可选择多个值

`<input>`的 `pattern` 属性：

描述了一个正则表达式用于验证 `<input>` 元素的值

**`<input>`的 `placeholder` 属性：**

输入框底的提示，暗的，值为字符串提前显示在输入框下

**`<input>` 的 `required` 属性：**

属性是一个布尔属性，规定必须在提交之前填写输入域（不能为空）

**必需字段/必填字段**

**`<input>`的 `step` 属性：**

为输入域规定合法的数字间隔，数字间隔输入选择器

step 属性可以与 max 和 min 属性创建一个区域值

step 属性与以下type类型一起使用: number、range、date、datetime,、datetime-local、month、time 和 week

## 26.语义元素

![](C:\Users\Rain7\Desktop\笔记md\图片\yuyiys.png)

`<aside>`侧边栏

## 27.html5 Web存储

使用HTML5可以在本地存储用户的浏览数据。

早些时候,本地存储使用的是 cookie。但是Web 存储需要更加的安全与快速. 这些数据不会被保存在服务器上，但是这些数据只用于用户请求网站数据上.它也可以存储大量的数据，而不影响网站的性能.

数据以 键/值 对存在, web网页的数据只允许该网页访问使用。

localStorage 和 sessionStorage 

客户端存储数据的两个对象为：

- localStorage - 用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去除。
- sessionStorage - 用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。

不管是 localStorage，还是 sessionStorage，可使用的API都相同，常用的有如下几个（以localStorage为例）：

- 保存数据：`localStorage.setItem(key,value);`
- 读取数据：`localStorage.getItem(key);`
- 删除单个数据：`localStorage.removeItem(key);`
- 删除所有数据：`localStorage.clear();`
- 得到某个索引的key：`localStorage.key(index);`

## 28.HTML5 Web IndexedDB 数据库

IndexedDB 是一种基于浏览器的 NoSQL 数据库，用于在客户端持久化存储大量结构化数据。

IndexedDB 允许通过键值对存储复杂的数据对象（如对象、数组、文件等），并支持事务、索引、版本控制和复杂查询操作。

IndexedDB 是异步的，不会阻塞主线程，适合离线应用程序、缓存等场景。

IndexedDB 非常适合需要存储大量结构化数据的应用程序，尤其是那些希望支持离线模式或处理复杂查询的 Web 应用。

IndexedDB 特性

- **键值对存储**：数据以键值对的形式存储在对象存储（object store）中。
- **事务支持**：所有数据操作必须在事务内完成，以确保数据一致性和完整性。
- **异步 API**：所有操作都是异步的，不会阻塞 UI 线程，使用事件回调或 Promises 来处理结果。
- **版本控制**：数据库使用版本号来管理数据库的架构（如创建或修改对象存储）。
- **索引**：支持对数据的字段建立索引，以加快查询速度。
- **离线支持**：数据可以持久化存储并在断网情况下继续访问，非常适合构建离线 Web 应用。

**IndexedDB 使用场景：**

- 离线存储：IndexedDB 允许你存储数据以便在没有网络连接时访问，这对于离线 Web 应用至关重要。
- 缓存：可以用于存储大量缓存数据（如文件、图片、视频），提升应用的加载速度。
- 复杂数据处理：适用于需要存储和处理大量结构化数据的场景，尤其是需要索引和查询功能。
- 本地数据库：IndexedDB 可以作为前端应用的本地数据库，存储用户数据、配置信息、应用状态等。

**IndexedDB 的优势：**

- 大容量存储：支持更大数据存储（常常可以达到几百 MB 或更多），比 localStorage 的 5MB 限制大得多。
- 丰富的数据操作：支持事务、索引、查询、批量处理等复杂操作。
- 离线支持：数据保存在用户设备上，可以离线访问并同步到服务器。

**IndexedDB 的劣势：**

- API 复杂：相比 localStorage 等简单的客户端存储，IndexedDB API 相对复杂，需要更多的代码。
- 异步处理：操作异步执行，初学者可能会不习惯处理回调或 Promise。
- IndexedDB 非常适合需要存储大量结构化数据的应用程序，尤其是那些希望支持离线模式或处理复杂查询的 Web 应用。

## 29.HTML5 Web Workers

web worker 是运行在后台的 JavaScript，不会影响页面的性能。

当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。

web worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行。

**Web Workers 和 DOM**

由于 web worker 位于外部文件中，它们无法访问下列 JavaScript 对象：

- window 对象
- document 对象
- parent 对象

## 30.HTML5 服务器发送事件(Server-Sent Events)

HTML5 服务器发送事件（server-sent event）允许网页获得来自服务器的更新。

Server-Sent 事件指的是网页自动获取来自服务器的更新。

以前也可能做到这一点，前提是网页不得不询问是否有可用的更新。通过服务器发送事件，更新能够自动到达。

例子：Facebook/Twitter 更新、股价更新、新的博文、赛事结果等。

**EventSource 对象**

onopen事件：当通往服务器的连接被打开

onmessage事件：当接收到消息

onerror事件：当发生错误

## 31.HTML5 WebSocket

WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议

WebSocket 协议本质上是一个基于 TCP 的协议

## 32.代码规范

**使用正确的文档类型：**

文档类型声明位于HTML文档的第一行`<!DOCTYPE html>`

**使用小写元素名**

**关闭所有 HTML 元素**

**关闭空的 HTML 元素：**`<meta charset="utf-8" />`

使用小写属性名

**属性值：**

HTML5 属性值可以不用引号。

属性值我们推荐使用引号

**图片属性：**

图片通常使用 **alt** 属性。 在图片不能显示时，它能替代图片显示。

**空格和等号：**

等号前后可以使用空格。

**避免一行代码过长:**

每行代码尽量少于 80 个字符，(使用 HTML 编辑器，左右滚动代码是不方便的)

**空行和缩进：**

不要无缘无故添加空行

为每个逻辑功能块添加空行，这样更易于阅读

缩进使用两个空格，不建议使用 TAB

比较短的代码间不要使用不必要的空行和缩进

**省略 `<html>` 和 `<body>`：**

在标准 HTML5 中， `<html>` 和 `<body>` 标签是可以省略的

**省略 `<head>`：**

在标准 HTML5 中， `<head>`标签是可以省略的

默认情况下，浏览器会将 `<body>` 之前的内容添加到一个默认的 `<head>` 元素上

**元数据：**

HTML5 中 `<title>` 元素是必须的，标题名描述了页面的主题

**HTML 注释**

注释可以写在 `<!--  -->`中:

**样式表**

样式表使用简洁的语法格式 ( type 属性不是必须的):

`<link rel="stylesheet" href="styles.css">`

**在 HTML 中载入 JavaScript**

使用简洁的语法来载入外部的脚本文件 ( type 属性不是必须的 ):

`<script src="myscript.js">`

**使用小写文件名**

**文件扩展名**

HTML 文件后缀可以是 **.html** (或 **.htm**)。

CSS 文件后缀是 **.css** 。

JavaScript 文件后缀是 **.js** 。

**.htm 和 .html 的区别**

.htm 和 .html 的扩展名文件本质上是没有区别的，浏览器和 Web 服务器都会把它们当作 HTML 文件来处理

他们的区别在于：

.htm 应用在早期 DOS 系统，系统现在或者只能有三个字符

在 Unix 系统中后缀没有特别限制，一般用 .html







