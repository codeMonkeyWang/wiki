## HTML 30分钟入门教程

30分钟内让你明白HTML是什么，并对它有一些基本的了解。一旦入门后，你可以从网上找到更多更详细的资料来继续学习。
什么是HTML

HTML是英文Hyper Text Mark-up Language(超文本标记语言)的缩写，它规定了自己的语法规则，用来表示比“文本”更丰富的意义，比如图片，表格，链接等。浏览器（IE,FireFox等）软件知道HTML语言的语法，可以用来查看HTML文档。目前互联网上的绝大部分网页都是使用HTML编写的。
HTML是什么样的

简单地来说，HTML的语法就是给文本加上表明文本含义的标签(Tag)，让用户（人或程序）能对文本得到更好的理解。

下面是一个最简单的HTML文档：
>
<html>
  <head>
    <title>第一个Html文档</title>
  </head>
  <body>
    欢迎访问<a href="http://deerchao.net">deerchao的个人网页</a>!
  </body>
</html>

所有的HTML文档都应该有一个`<html>`标签，`<html>`标签可以包含两个部分:`<head>`和`<body>`。

`<head>`标签用于包含整个文档的一般信息，比如文档的标题（`<title>`标签用于包含标题），对整个文档的描述，文档的关键字等等。文档的具体内容就要放在`<body>`标签里了。`<a>`标签用于表示链接，在浏览器（如IE,Firefox等）中查看HTML文档时，点击`<a>`标签括起来的内容时，通常会跳转到另一个页面。这个要跳转到的页面的地址由`<a>`标签的href属性指定。上面的`<a href="http://deerchao.net">`中，href属性的值就是http://deerchao.net。
HTML文档可以包含的内容

通过不同的标签，HTML文档可以包含不同的内容，比如文本，链接，图片，列表，表格，表单，框架等。

HTML文档格式详细说明

前面介绍了HTML文档的基本格式，下面再做一个详细说明。
HTML文档可以用任何文本编辑器（比如记事本，UltraEdit等）创建，编辑，因为它的内容在本质也只是一些文本。
在HTML文本中，用尖括号括起来的部分称为标签。如果想在正文里使用尖括号（或者大与号小与号，总之是同一个东西），必须使用字符转义，也就是说转换字符的原有意义。<应该使用`&lt;`代替，>则使用`&gt;`，至于&符号本身,则应该使用`&amp;`替代（不得不说的是有很多HTML文档没有遵循这个规则，常用的浏览器也都能够分析出&到底是一个转义的开始，还是一个符号，但是这样做是不推荐的）。
标签本质上是对它所包含的内容的说明，可能会有属性，来给出更多的信息。比如`<img>`（图片）标签有src属性（用于指明图片的地址），width和height属性（用于说明图片的宽度和高度）。HTML里能使用哪些标签，这些标签分别可以拥有哪些属性，这些都是有规定的，知道了这里说的基本知识之后，学习HTML其实也就是学习这些标签了。本文后面会对常用的HTML标签做出简短的介绍。
标签通常有开始部分和结束部分（也被称为开始标签和结束标签），它们一起限定了这个标签所包含的内容。属性只能在开始标签中指定，属性值可以用单引号或双引号括起来。结束标签都以/加上标签名来表示。有时候，有些标签并不包含其它内容（只包括自己的属性，甚至连属性都没有），这种情况下，可以写成类似这样：`<img src="logo.gif" />`。注意最后的一个空格和一个反斜杠，它说明这个标签已经结束，不需要单独的结束标签了。
某些标签包含的内容中还可以有新的标签，新的标签名甚至可能还可以与包含它的标签的名称相同（哪些标签可以包含标签，可以包含哪些标签也是有规定的）。比如：

>
<div>
  <div>分类目录...</div>
  <div>当前分类内容列表...</div>
</div>
	
在这种情况下，最后出现的标签应该最先结束。
HTML文档里所有的空白符（空格，Tab，换行，回车）会被浏览器忽略，唯一的例外是空格，对空格的处理方式是所有连续的空格被当成一个空格，不管有一个，还是两个，还是100个。之所以有这样的规则是因为忽略空白符能让使用HTML的作者以他觉得最方便的格式来排列内容，比如可以在每个标签开始后增加缩进，标签结束后减少缩进。由于英语文本中空格用得很普遍（用于分隔单词），所以对空格做了这样的特殊处理。如果要显示连续的空格（比如为了缩进），应该用`&nbsp;`来代表空格。

## 常用标签介绍
### Link
> `<link media = "max-device-width"/>`

* `max-device-width`
* `print`
* `orientation`
* `landscape`
* `portrait`

### 文本

最常用的标签可能是<font>了，它用于改变字体，字号，文字颜色。

>
<font size="6">6</font>  
<font size="4">4</font>  
<font color="red" size="5">红色的5</font>   
<font face="黑体">黑体的字</font>   

加粗，下划线，斜体字也是常用的文字效果，它们分别用`<b>`,`<u>`,`<i>`表示：

>
<b>Bold</b>  
<i>italic</i>    
<u>underline</u> 
<pre>原样显示 </pre>

`<del>` `<ins>` 用来添加删除线和下划线

>
<del>删除线</del>   
<ins>下划线</ins>


还有一些标签，用来指出包含的文本有特殊的意义，比如`<abbr>`（表示缩写），`<em>`（表示强调），`<strong>`（表示更强地强调）,`<cite>`（表示引用），`<address>`（表示地址）等等。这些标签不是为了定义显示效果而存在的，所以从浏览器里看它们可能没有任何效果，也可能不同的浏览器对这些标签的显示效果完全不同。
一篇很长的文章，如果有合适的小标题的话，就可以快速地对它的内容进行大致的了解。在HTML里，用来表示标题的标签有：`<h1>,<h2>,<h3>,<h4>,<h5>,<h6>`，它们分别表示一级标题，二级标题，三级标题...

>
<h1>HTML 30分钟教程</h1>
<h2>什么是HTML</h2>
...
<h2>HTML是什么样的</h2>
...


### 图片

`<hr>`标签用于在页面上添加横线。可以通过指定width和color属性来控制横线的长度和颜色。
点击查看效果
`<hr width="90%" color="red" />`
`<img>`标签用于在页面上添加图片，src属性指定图片的地址，如果无法打开src指定的图片，浏览器通常会在页面上需要显示图片的地方显示alt属性定义的文本。
`<img src="http://www.w3.org/Icons/valid-xhtml10" alt="图片简介" />`

### 链接

超级链接用`<a>`标签表示，`href`属性指定了链接到的地址。`<a>`标签可以包含文本，也可以包含图片。

>
<a href="http://deerchao.net">deerchao的个人网站</a>
<a href="http://validator.w3.org"><img src="http://www.w3.org/Icons/valid-xhtml10" alt="验证HTML" /></a>

### 分段与换行

由于HTML文档会忽略空白符，所以要想保证正常的分段换行的话，必须指出哪些文字是属于同一段落的，这就用到了标签`<p>`。

> <p>这是第一段。</p>
<p>这是第二段。</p>

也有人不用`<p>`，而用`<br>`。`<br>`只表示换行，不表示段落的开始或结束，所以通常没有结束标签。

> 
这是第一段。<br>
这是第二段。<br/>
这是第三段。

有时，要把文档看作不同的部分组合起来的，比如一个典型的页面可能包括三个部分：页头，主体，页脚。<div>标签专门用于标明不同的部分：

>
<div>页头内容</div>
<div>主体内容</div>
<div>页脚内容</div>

### 表格

HTML文档在浏览器里通常是从左到右，从上到下地显示的，到了窗口右边就自动换行。为了实现分栏的效果，很多人使用表格（`<table>`）进行页面排版（虽然HTML里提供表格的本意不是为了排版）。
`<table>`标签里通常会包含几个`<tr>`标签，`<tr>`代表表格里的一行。`<tr>`标签又会包含`<td>`标签，每个`<td>`代表一个单元格。

<table>
  <tr>
    <td>2000</td><td>悉尼</td>
  </tr>
  <tr>
    <td>2004</td><td>雅典</td>
  </tr>
  <tr>
    <td>2008</td><td>北京</td>
  </tr>
</table>

`<tr>`标签还可以被`<table>`里的`<thead>`或`<tbody>`或`<tfoot>`包含。它们分别代表表头，表正文，表脚。在打印网页的时候，如果表格很大，一页打印不完，`<thead>`和`<tfoot>`将在每一页出现。
`<th>`和`<td>`非常相似，也用在`<tr>`里边，不同的是`<th>`代表这个单元格是它所在的行或列的标题。   
标题使用`<caption>`
*   `<td rowspan="2"> </td>` //占用两行的位置
*   `<colspan="2"> ` //占用两列

<table>
	<caption> 这是个标题</caption>
  <thead>
    <tr><th>时间</th><th>地点</th></tr>
  </thead>
  <tbody>
    <tr><td>2000</td><td>悉尼</td></tr>
    <tr><td>2004</td><td>雅典</td></tr>
    <tr><td>2000</td><td>北京</td></tr>
  </tbody>
</table>



### 列表

表格用于表示二维数据（行，列），一维数据则用列表表示。列表可以分为无序列表（`<ul>`），有序列表（`<ol>`）和定义列表（`<dl>`）。前两种列表更常见一些，都用`<li>`标签包含列表项目。
无序列表表示一系列类似的项目，它们之间没有先后顺序。

<ul>
  <li>苹果</li>
  <li>桔子</li>
  <li>桃</li>
</ul>

有序列表中各个项目间的顺序是很重要的，浏览器通常会自动给它们产生编号。

<ol>
  <li>打开冰箱门</li>
  <li>把大象赶进去</li>
  <li>关上冰箱门</li>
</ol>

<dl>
	<dt> 计算机</dt>
	<dd>一种很叼的机器</dd>
</dl>

### 表单
* `<form>` 
	* action
	* method = "POST"
* `<input>`
	* placeholder = "xxxxx" //提示信息
	* requiored //bool 指示必须填写的选项
	* type = "radio",名称要一致
	
	``` html 
	<input type="radio" name="beantype" value="whole"> Whole bean<br>
	<input type="radio" name="beantype" value="ground" checked> Ground
	
	```
	
	* type = "number"
	
	``` html
	<input type="number" name="bags" min="1" max="10">
	```
	
	* type = "text"

		``` html
		<input type="text" name="name" value="" placeholder="Buckaroo Banzai" required>
		```
		 
		* type = "tel" //text变种，在移动设备上会弹出定制键盘
	`<input type="tel" name="phone" value="" placeholder="310-555-1212" required> `
	
		* type = "email"
		* type = "url"
		* type = "password"
		* type = "file" //必须使用post方法
	
	* type="checkbox" 

	``` html
    <input type="checkbox" name="extras[]" value="giftwrap"> Gift wrap<br>
    <input type="checkbox" name="extras[]" value="catalog" checked>
    Include catalog with order
	```
	* type = "date"
	`<input type="date" name="date"> `

	* type = "submit"
	`<input type="submit" value="Order Now">`

	* type = "range"
	`input type ="range" min="0" max = "20" step ="2"`
	* type = "color"
	`input type = "color"`

* `<textarea>`

``` html
<textarea name="comments" rows = "10" cols = "48">
```

* `<select>`
	* 增加 multiple 可以变为多选

``` html
<select name="beans" multiple>
  <option value="House Blend">House Blend</option>
  <option value="Bolivia">Shade Grown Bolivia Supremo</option>
  <option value="Guatemala">Organic Guatemala</option>
  <option value="Kenya">Kenya</option>
</select>
```	

* `<label>`
	* 增加for属性
* `<fieldset>`
	* `<legend>`

``` html

	<fieldset>
		<legend>Order details</legend>
		...
	</fieldset>
```



### 框架

最后谈一下框架，曾经非常流行的技术，框架使一个窗口里能同时显示多个文档。主框架页里面没有`<body>`标签，取代它的是`<frameset>`。
`<frameset>`标签的属性Rows和Cols用于指定框架集(frameset)里有多少行（列），以及每行（列）的高度（宽度）。
`<frameset>`标签可以包含`<frame>`标签，每个`<frame>`标签代表一个文档（src属性指定文档的地址）。
如果觉得这样的页面还不够复杂的话，还可以在`<frameset>`标签里包含`<frameset>`标签。

	<frameset rows="15%,*">
	     <frame src="top.html" name=title scrolling=no>
	     <frameset cols="20%,*">
	          <frame src="left.html" name=sidebar>
	          <frame src="right.html" name=recipes>
	     </frameset>
	</frameset>

## div and pan


## HTML5
* `<header> `页眉
* `<footer>` 页脚
* `<time>` 时间
	* `datetime="2015-11-11 09:00"`
* `<nav>` 导航
* `<article>` 主题
* `<aside>` 侧边栏
* `<section>` 单独区块
* `<video>` 视频
	* `<source>`
		* src
	* `<object>` //用来支持flash
	* autoplay 自动播放
	* controls //提供控件 bool
	* width
	* src
	* poster=“test.png” //海报
	* loop //bool
	* preload
		* metadata 加载原始数据
		* none //不加载
		* auto //交给浏览器
* `<progress>` 进度
* `<mark>` 突出显示文本
* `<meter>`
* `<audio>`
* `<figure>`
* `<canvas>`
	
``` html
	<video controls autoplay width="512" height="288">
		<source src="video/tweetsip.mp4">
		<source src="video/tweetsip.webm">
		<source src="video/tweetsip.ogv">
		<p>Sorry, your browser doesn't support the video element.</p>
	</video>
```


## 30分钟以后怎么办

这篇文章只是让从没有接触过HTML的人对HTML有个初步的印象，所以很多东西都没有谈到。本文并没有列出HTML中所有的标签，对于列出的标签也没有介绍它们的全部属性。另外，没有提到的东西里还包括我觉得非常重要的CSS, JavaScript, XHTML, XML, Web Standards，以及它们与HTML的关系。不过这些也不太可能在30分钟内学会，好在只要入了门，就能利用网上很多资源继续学习。当然，如果有一本纸质书，就更好了，这方面我推荐`<<HTML与XHTML权威指南>>`。

---
### 参考：
[HTML 30分钟入门教程](http://deerchao.net/tutorials/html/html.htm)