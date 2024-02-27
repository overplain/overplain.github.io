---
title: html css笔记
abbrlink: c2394247
date: 2022-12-24 19:10:23
tags:
cover: https://images.pexels.com/photos/14413791/pexels-photo-14413791.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1
categories: 学习笔记
---

# html

## html基本结构

> ```html
> <!-- 文档声明，声明当前网页的版本 -->
> <!doctype html> 
> 
> <!-- html的根标签（元素），网页中的所有内容都要写根元素的里边 -->
> 
> <html>
> 
> <!-- head是网页的头部，head中的内容不会在网页中直接出现，主要用来帮助浏览器或搜索引擎来解析网页-->
> 
> <head>
>     <!-- meta标签用来设置网页的元数据，这里meta用来设置网页的字符集，避免乱码问题 -->
>     <meta charset="utf-8">
>     <!-- title中的内容会显示在浏览器的标题栏，搜索引擎会主要根据title中的内容来判断网页的主要内容 -->
>     <title>网页的标题</title>
> </head>
> 
> <!-- body是htm1的子元素，表示网页的主体，网页中所有的可见内容都应该写在body里 --><body>
> 
>    <!-- h1网页的一级标题 --> 
> 
>  <h1>网页的大标题</h1>
> 
> </body>
> 
> </html>
> ```



##  字符实体与语义标签

###  字符实体

有些时候，在HTML中不能直接书写一些特殊符号，如：  

多个连续的空格（在网页中编写的多个空格默认情况会自动被浏览器解析为一个空格）  

比如字母两侧的大于小于号（可能会被认为是标签并解析）  

如果我们需要在网页中书写这些特殊的符号，则需要使用html中的实体（转义字符）实体的语法：&实体的名字;，如：  

![image-20230106155112829](https://cdn.jsdelivr.net/gh/overplain/pico/img/202301061551679.png)



* meta主要用于设置网页中的一些元数据，元数据并不是给用户看的

* charset ：指定网页的字符集

* name ：指定的数据的名称

* keywords：表示网站的关键字，可以同时指定多个关键字，关键字间使用,隔开

* description：表示网站的描述信息

* content ：指定的数据的内容，会作为搜索结果的超链接上的文字显示

* title标签的内容会作为搜索结果的超链接上的文字显示

****

### 语义标签

#### 块元素 

> 标题	一共有六级标题

从h1 ~ h6重要性递减，h1最重要，h6最不重要

h1在网页中的重要性仅次于title标签

一般情况下一个页面中只会有一个h1

一般情况下标题标签只会使用到h1 ～ h3，h4 ～ h6很少用      

* ```<hgroup>	标题组	多层次的标题。它将一组<h1> ～ <h6>元素分组 ```
* ![image-20230106155131518](https://cdn.jsdelivr.net/gh/overplain/pico/img/202301061551867.png)

行内元素与块元素：

块元素（block element）

- 在网页中一般通过块元素来对页面进行布局

行内元素（inline element）

-  行内元素主要用来包裹文字

- 一般情况下会在块元素中放行内元素，而不会在行内元素中放块元素

- 如<p>元素中不能放任何的块元素，不过块元素中基本上什么都能放



### 布局标签

F12看源码

第一栏elements

header表示网页的头部（页眉）

main表示网页的主体部分（一个页面中只会有一个main）

footer表示网页的底部（页脚）

nav表示网页中的导航

aside和主体相关的其他内容（侧边栏）

article表示一个独立的文章

section表示一个独立的区块，上边的标签都不能表示时使用section

![image-20230106155147504](https://cdn.jsdelivr.net/gh/overplain/pico/img/202301061551759.png)

### 列表

在html中可以创建列表，html列表一共有三种：

- 有序列表，使用ol标签来创建有序列表，使用li表示列表项

 ```html
<ol>

  <li>Mix flour, baking powder, sugar, and salt.</li>

  <li>In another bowl, mix eggs, milk, and oil.</li>

  <li>Stir both mixtures together.</li>

  <li>Fill muffin tray 3/4 full.</li>

  <li>Bake for 20 minutes.</li>

</ol> 
 ```

![image-20230106155206425](https://cdn.jsdelivr.net/gh/overplain/pico/img/202301061552866.png)

- 无序列表，使用`ul`标签来创建无序列表，使用`li`表示列表项

```html
<ul>
    <li>Milk</li>
    <li>Cheese
        <ul>
            <li>Blue cheese
                <ul>
                    <li>Sweet blue cheese</li>
                    <li>Sour blue cheese</li>
                </ul>
            </li>
            <li>Feta</li>
        </ul>
    </li>
</ul>

```

列表元素之间是可以互相嵌套的

![image-20230106155218093](https://cdn.jsdelivr.net/gh/overplain/pico/img/202301061552180.png)

- 定义列表，使用dl标签来创建定义列表，使用dt表示定义的内容，使用dd来对内容进行解释说明

```html
<dl>
    <dt>Beast of Bodmin</dt>
    <dd>A large feline inhabiting Bodmin Moor.</dd>

    <dt>Morgawr</dt>
    <dd>A sea serpent.</dd>

    <dt>Owlman</dt>
    <dd>A giant owl-like creature.</dd>
</dl>
```

### 超链接

超链接可以让我们从一个页面跳转到其他页面，或者是当前页面的其他的位置

使用a标签来定义超链接，href属性指定跳转的目标路径，值可以是一个外部网站的地址，也可以写一个内部页面的地址

超链接是也是一个行内元素，在a标签中可以嵌套除它自身外的任何元素

#### 外部地址

- Linking to an absolute URL：链接一个绝对路径
- Linking to an email address：链接一个email地址
- Linking to telephone numbers：链接电话号码
- Using the download attribute to save a `<canvas>` as a PNG：下载图片

```html
<ul>
  <li><a href="https://www.baidu.com">Website</a></li>
  <li><a href="mailto:example@outlook.com">Email</a></li>
  <li><a href="tel:+123456789">Phone</a></li>
</ul>
```

#### 内部地址

当我们需要跳转一个服务器内部的页面时，一般我们都会使用相对路径，会以./或../开头

- ./ 表示当前文件所在目录，可以省略不写

- ../表示当前文件所在目录的上一级目录

```html
<a href="./test1.html">超链接1</a><br>
<a href="../test2.html">超链接2</a><br>
<a href="./test3/test3.html">超链接3</a><br>
<a href="../test4/test4.html">超链接4</a>
```

#### 新建页面

target属性，用来指定超链接打开的位置可选值：

- _self在当前页面中打开超链接，默认值

- _blank在新建页面中打开超链接

```html
<a href="./test1.html">超链接1——默认</a><br>
<a href="./test1.html" target="_self">超链接1——当前页面</a><br>
<a href="./test1.html" target="_blank">超链接1——新建页面</a><br>
```

### 锚点跳转

可以将`#`作为超链接的路径的占位符使用。

`<a href="#">`这是一个新的超链接`</a>`

可以使用javascript:; 来作为href的属性，此时点击这个超链接什么也不会发生

`<a href="javascript:;">`这是一个新的超链接`</a>`

可以直接将超链接的`href`属性设置为`#`，这样点击超链接以后页面不会发生跳转，而是转到当前页面的顶部的位置

可以跳转到页面的指定位置（锚点），只需将`href`属性设置`#目标元素的id属性值`（唯一不重复）

id属性（唯一不重复的）

- 每一个标签都可以添加一个id属性
- id属性就是元素的唯一标识，同一个页面不能出现重复的id属性

### 图片

图片标签用于向当前页面中引入一个外部图片

img标签是一个自结束标签，这种元素属于替换元素（块和行内元素之间，具有两种元素的特点）

属性:

- src：属性指定的是外部图片的路径（路径规则和超链接是一样的）
- alt：图片的描述，这个描述默认情况下不会显示，有些浏览器会在图片无法加载时显示，搜索引擎会根据alt中的内容来识别图片
- width：图片的宽度（单位是像素）
- height ：图片的高度（单位是像素）[宽度和高度中如果只修改了一个，则另一个会等比例缩放]

图片的格式：

jpeg(jpg)

- 支持的颜色比较丰富
- 不支持透明效果
- 不支持动图
- 一般用来显示照片

gif

- 支持的颜色比较单一
- 支持简单透明
- 支持动图

png

- 支持的颜色丰富
- 支持复杂透明
- 不支持动图
- 专为网页而生

webp

- 这种格式是谷歌新推出的专门用来表示网页中的图片的一种格式

- 具备其他图片格式的所有优点，而且文件还特别的小
- 缺点：兼容性不好

base64

- 将图片使用base64编码，这样可以将图片转换为字符，通过字符的形式来引入图片
  图片格式的选择

- 图片效果一样的，选文件小的

- 图片效果不一样的，选图片效果好的

- 尽可能的兼顾和平衡图片效果和文件大小

### 内联框架

用于向当前页面中引入一个其他页面

- src指定要引入的网页的路径
- frameborder 指定内联框架的边框

```html
<iframe src="https://www.qq.com" width="800" height="600" frameborder="0"></iframe>
```

### 音视频

#### 音频

audio标签用来向页面中引入一个外部的音频文件

音视频文件引入时，默认情况下不允许用户自己控制播放停止

属性：

- controls是否允许用户控制播放
- autoplay音频文件是否自动播放
  - 如果设置了autoplay，则音乐在打开页面时会自动播放
    但是目前来讲大部分浏览器都不会自动对音乐进行播放

- loop音乐是否循环播放

```<audio src="./source/audio.mp3" controls autoplay loop></audio>```

#### SOURCE

除了通过`src`属性来指定外部文件的路径以外，还可以通过`<source>`元素来指定文件的路径

```html
    对不起，您的浏览器不支持播放音频！请升级浏览器！
	<source src="./source/audio.mp3">
	<source src="./source/audio.ogg">
</audio>```
```

用source可以显示文字提示不支持

多个可以更严谨防止浏览器不支持一个格式

``````html
<embed src="./source/audio.mp3" type="audio/mp3" >
``````

embed和那句话任选其一就行了 它能兼容所有【非常流氓！！！

#### 视频

使用`video`标签来向网页中引入一个视频，使用方式和`audio`基本上是一样的

```html
<video controls>
    <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.webm" type="video/webm">
    <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" type="video/mp4">
    <embed src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" type="video/mp4">
</video>
```

通过iframe引入视频

``````html
<iframe frameborder="0" src="http://">
``````

# CSS

## css语法与选择器

### 简介

使用css来修改元素的样式

- 内联样式，行内样式 

  - 在标签内部通过`Style`属性来设置元素的样式
- `<p style="color:">内联样式（行内样式）</p>`

问题：使用内联样式，样式只能对一个标签生效。如果希望影响到多个元素，必须在每一个元素中都复制一遍；并且当样式发生变化时，我们必须要一个一个的修改，非常的不方便。（注意：开发时绝对不要使用内联样式）

- 内部样式表
  - 将样式编写到`head`中的`style`标签里然后通过css的选择器来选中元素并为其设置各种样式可以同时为多个标签设置样式，并且修改时只需要修改一处即可。内部样式表更加方便对样式进行复用

```html
<style>
p{
    color:green; 
    font-size:50px;
}
</style>
```

问题：我们的内部样式表只能对一个网页起作用，它里边的样式不能跨页面进行复用

- 外部样式表
  - 可以将css样式编写到一个外部的CSS文件中，然后通过`link`标签来引入外部的CSS文件

```html
<link rel="stylesheet" href="./style.css">
```

外部样式表需要通过`link`标签进行引入，意味着只要想使用这些样式的网页都可以对其进行引用使样式，可以在不同页面之间进行复用

将样式编写到外部的CSS文件中，可以使用到浏览器的缓存机制，从而加快网页的加载速度，提高用户的体验。

### CSS基本语法

#### 注释

- css中的注释
  - 只能使用`/*`和`*/`包裹。即不管是单行注释，还是多行注释，都是以`/*`开头，以`*/`结尾

- html中的注释
  - 只能使用`<!--`和`-->`包裹。即不管是单行注释，还是多行注释，都是以`<!--`开头，以`-->`结尾

- JS注释
  - 单行注释使用`//`。多行注释使用`/*`和`*/`包裹，以`<!--`开头，以`-->`结尾

#### 基本语法

*选择器 声明块*

- 选择器：

通过选择器可以选中页面中的指定元素

比如p的作用就是选中页面中所有的p元素声明块

- 声明块：

通过声明块来指定要为元素设置的样式

声明块由一个一个的声明组成，声明是一个名值对结构

一个样式名对应一个样式值，名和值之间以:连接，以;结尾

```css
h1{
    color: green;
}
```

### CSS选择器

#### 通配选择器

- 作用：选中页面中的所有元素
- 语法：`*`
- 例子：`*{}`

```css
*{
    color: red;
}
```

#### 元素选择器

也叫类型选择器、标签选择器

- 作用：根据标签名来选中指定的元素
- 语法：`elementname{}`
- 例子：`p{}` `h1{}` `div{}`

```css
p{
    color: red; 
}

h1{
    color: green;
}
```

#### ID选择器

作用：根据元素的id属性值选中一个元素

语法：#id属性值{}

例子：#box{} #red{}

```css
#red{
	color:red;
}
```

#### 类选择器

- 作用：根据元素的class属性值选中一组元素
- 语法：`.classname`
- 例子：`.blue{}`

```css
.blue{
    color: blue;
}
.size{
    font-size: 20px;
}
```

class`是一个标签的属性，它和`id`类似，不同的是`class

- 可以重复使用，
- 可以通过`class`属性来为元素分组，
- 可以同时为一个元素指定多个`class`属性

```css
<p class="blue size"> 类选择器（Class selector）</p>
```

#### 属性选择器

作用：根据元素的属性值选中一组元素
语法1：[属性名] 选择含有指定属性的元素
语法2：[属性名=属性值] 选择含有指定属性和属性值的元素
语法3：[属性名^=属性值] 选择属性值以指定值开头的元素
语法4：[属性名$=属性值] 选择属性值以指定值结尾的元素
语法5：[属性名*=属性值] 选择属性值中含有某值的元素
例子：`p[title]{}` `p[title=e]{}` `p[title^=e]{}` `p[title$=e]{}` `p[title*=e]{}`

### 复合选择器

#### 交集选择器

- 作用：选中同时复合多个条件的元素
- 语法：`选择器1选择器2选择器3选择器n{}`
- *注意点：交集选择器中如果有元素选择器，必须使用元素选择器开头*

```css
div.red{
    font-size: 30px;
}

.a.b.c{
    color: blue;
}

```

#### 并集选择器

- 作用：同时选择多个选择器对应的元素
- 语法：`选择器1,选择器2,选择器3,选择器n{}`
- 例子：`#b1,.p1,h1,span,div.red{}`

```css
h1,span{
    color: green;
}
```

### 关系选择器

- 父元素：直接包含子元素的元素叫做父元素
- 子元素：直接被父元素包含的元素是子元素
- 祖先元素：直接或间接包含后代元素的元素叫做祖先元素；一个元素的父元素也是它的祖先元素
- 后代元素：直接或间接被祖先元素包含的元素叫做后代元素；子元素也是后代元素
- 兄弟元素：拥有相同父元素的元素是兄弟元素

#### 子元素选择器

- 作用：选中指定父元素的指定子元素
- 语法：`父元素 > 子元素`
- 例子：`A > B`

```css
div.box > p > span{
    color: orange;
}
```

#### 后代元素选择器   

- 作用：选中指定元素内的指定后代元素
- 语法：`祖先 后代`
- 例子：`A B`

```css
div span{
    color: skyblue;
}
```

#### 兄弟元素选择器

- 作用：选择下一个兄弟
- 语法：`前一个 + 下一个` `前一个 + 下一组`
- 例子1：`A1 + A2`（选择下一个兄弟）
- 例子2： `A1 ~ An`（选择下边所有的兄弟）

```css
p + span{
    color: red;
}

p ~ span{
    color: red;
}
```

### 伪类选择器

伪类（不存在的类，特殊的类）

伪类用来描述一个元素的特殊状态，比如：第一个子元素、被点击的元素、鼠标移入的元素.…

伪类一般情况下都是使用`:`开头

- `:first-child` 第一个子元素
- `:last-child` 最后一个子元素
- `:nth-child()` 选中第n个子元素
  - n：第n个，n的范围0到正无穷
  - 2n或even：选中偶数位的元素
  - 2n+1或odd：选中奇数位的元素

以上这些伪类都是根据所有的子元素进行排序的

- `:first-of-type` 同类型中的第一个子元素
- `:last-of-type` 同类型中的最后一个子元素
- `:nth-of-type()` 选中同类型中的第n个子元素

这几个伪类的功能和上述的类似，不同点是他们是在同类型元素中进行排序的

- `:not()`否定伪类，将符合条件的元素从选择器中去除

```css
/* ul下所有li，黑色 */
ul>li {
    color: black;
}

/* ul下第偶数个li，黄色 */
ul>li:nth-child(2n) {
    color: yellow;
}

/* ul下第奇数个li，绿色 */
ul>li:nth-child(odd) {
    color: green;
}

/* ul下第一个li，红色 */
ul>li:first-child {
    color: red;
}

/* ul下最后一个li，黄色 */
ul>li:last-child {
    color: orange;
}
```

![image-20230111203813718](https://cdn.jsdelivr.net/gh/overplain/pico/img/202301112038812.png)

```css
ul > li:not(:nth-of-type(3)){
    color:yellowgreen;
}
/*not()就是取消这一行的颜色*/
```

- `:link` 未访问的链接(正常的链接)
- `:visited`已访问的链接
  - 由于隐私的原因，所以`visited`这个伪类只能修改链接的颜色
- `:hover` 鼠标悬停的链接（用来表示鼠标移入的状态）
- `:active` 鼠标点击的链接（用来表示鼠标点击）

```css
/* unvisited link */
a:link {
  color: red;
}

/* visited link */
a:visited {
  color: yellow;
}

/* mouse over link */
a:hover {
  color: green;
}

/* selected link */
a:active {
  color: blue;
}
```

### 伪元素选择器

伪元素，表示页面中一些特殊的并不真实的存在的元素（特殊的位置）

伪元素使用`::`开头

- `::first-letter` 表示第一个字母
- `::first-line` 表示第一行
- `::selection` 表示选中的内容
- `::before` 元素的开始
- `::after` 元素的最后
- `::before`和`::after` 必须结合`content`属性来使用

``` css
/* 段落首字母设置大小为30px */
p::first-letter{
    font-size: 30px;
}

/* 段落第一行设置为黄色背景 */
p::first-line{
    background-color: yellow;
}

/* 段落选中的部分变绿色 */
p::selection{
    background-color: green；
}

/* div前加上内容 */
div::before{
    content: 'BEFORE';
    color: red;
}

/* div后加上内容 */
div::after{
    content: 'AFTER';
    color: blue;
}

```

## 样式继承及颜色长度单位介绍

### 继承

样式的继承，我们为一个元素设置的样式同时也会应用到它的后代元素上

继承是发生在祖先后后代之间的

继承的设计是为了方便我们的开发，利用继承我们可以将一些通用的样式统一设置到共同的祖先元素上，

这样只需设置一次即可让所有的元素都具有该样式

注意:并不是所有的样式都会被继承：

比如背景相关的，布局相关等的这些样式都不会被继承。

- 样式的冲突

​	-当我们通过不同的选择器，选中相同的元素，并且为相同的样式设置不同的值时，此时就发生了样式的冲突。

发生样式冲突时，应用哪个样式由选择器的权重（优先级）决定

- 选择器的权重：

  内联样式		1,0,0,0

  id选择器		0,1,0,0

  类和伪类选择器		0,0,1,0

  元素选择器		0,0,0,1

  通配选择器		0,0,0,0

  继承的样式		没有优先级

比较优先级时，需要将所有的选择器的优先级进行相加计算，最后优先级越高，则越优先显示(分组选择器是单独计算的

选择器的累加不会超过其最大的数量级，类选择器在高也不会超过id选择器

如果优先级计算后相同,此时则优先使用靠下的样式

可以在某一个样式的后边添加`!important`，则此时该样式会获取到最高的优先级，甚至超过内联样式，

*注意：在开发中一定要慎用！*

### 长度单位

长度单位:

- 像素

​	- 屏幕（显示器）实际上是由一个一个的小点点构成的

​	- 不同屏幕的像素大小是不同的，像素越小的屏幕显示的效果越清晰-所以同样的200px在不同的设备下显示效果不一样

- 百分比

​	-也可以将属性值设置为相对于其父元素属性的百分比

​	-设置百分比可以使子元素跟随父元素的改变而改变

em

em是相对于元素的字体大小来计算的，`1em = <self>.font-size`，也就说em值会根据元素本身的字体大小的改变而改变

rem

rem是相对于根元素的字体大小来计算，`1em = <root>.font-size`，也就说em值会根据根元素的字体大小的改变而改变

(em改变字体大小就能改变内容大小

```css
 .box4 {
        font-size: 20px;
        width: 10rem; /*当时用rem时，不管怎么改本元素的font-size都是不会变的。需要定义root元素的font-size才可以 */
        height: 10rem;
        background-color: red;
    }
```

### 颜色单位

在css中可以直接使用颜色名来设置各种颜色

比如:red、orange、yellow、 blue、green ... 但是在css中直接使用颜色名是非常的不方便

- RGB值:

RGB通过三种颜色的不同浓度来调配出不同的颜色

R red,G green , B blue

每一种颜色的范围在0 - 255 (0% - 100%)之间

语法:RGB(红色,绿色,蓝色)

- RGBA：

就是在rgb的基础上增加了一个a表示不透明度

需要四个值，前三个和rgb一样，第四个表示不透明度

1表示完全不透明 0表示完全透明 .5半透明

- 十六进制的RGB值:

语法:#红色绿色蓝色

颜色浓度通过00-ff

如果颜色两位两位重复可以进行简写

#aabbcc --> #abc

- HSL值 HSLA值

H 色相(0 - 360)

S 饱和度，颜色的浓度 0% - 100%

L 亮度，颜色的亮度 0% -100%

## 盒模型

### 文档流

网页是一个多层的结构，一层摞着一层

通过css可以分别为每一层来设置样式

作为用户来讲只能看到最顶上一层

这些层中，最底下的一层称为文档流，文档流是网页的基础

​		我们所创建的元素默认都是在文档流中进行排列

对于我们来元素主要有两个状态在文档流中

- 不在文档流中（脱离文档流）

- 元素在文档流中有什么特点:

  - 块元素

    块元素会在页面中独占一行(自上向下垂直排列）

    默认宽度是父元素的全部（会把父元素撑满）

    默认高度是被内容撑开（子元素）

  - 行内克素

    行内元素不会独占页面的一行，只占自身的大小

    行内元素在页面中左向右水平排列（书写习惯一致）

    如果一行之中不能容纳下所有的行内元素，则元素会换到第二行继续自左向右排列（书写习惯一致）

    行内元素的默认宽度和高度都是被内容撑开

### 盒模型

![image-20230113213021324](https://cdn.jsdelivr.net/gh/overplain/pico/img/202301141442677.png)

- 盒模型、盒子模型、框模型

  - css将页面中所有元素都设置为了一个矩形的盒子

  - 讲元素设置为矩形的盒子后，对页面的布局就变成将不同的盒子放到不同的位置
  - *盒子可见框的大小，由内容区、内边距和边框共同决定，所以在计算盒子大小时，需要将这三个区域加到一起计算*

每一个盒子由以下几个部分组成：

**可见框由内容区、边框、内边距组成**

#### 内容区（content）

- 元素中的所有的子元素和文本内容都在内容区中
- 内容去的大小由width和height两个属性来设置
- **width设置内容区的宽度**
- **height设置内容区的高度**

```html
.box1{
    width: 200px; 
    height: 200px; 
    background-color: #bfa;
}
```

#### 内边距（padding）

- 内边距，也叫填充，是内容区和边框之间的空间

  - `padding-top` 上内边距
  - `padding-right` 右内边距
  - `padding-bottom`下内边距
  - `padding-left` 左内边距
- padding内边距的简写属性，可以同时指定四个方向的内边距，规则和边框中属性值设置一样
- **内边距的设置会影响到盒子的大小，背景颜色会延伸到内边距上**
- **文字、子元素只会出现在内容区内不会出现在内边距上**

```css
<style>
    .outer{
        width: 200px;
        height: 200px;
        border: 10px orange solid;
        padding-right: 100px;
        padding-bottom: 100px;
        padding-left: 100px;
    }

    .inner {
        width: 200px;
        height: 200px;
        background-color: greenyellow;
    }
</style>

<div class="outer">
    <div class="inner"></div>
</div>

```



#### 边框（border）

- 边框属于盒子边缘，边框里边属于盒子内部，出了边框都是盒子的外部
- **边框也会影响盒子的大小**
- 设置边框至少需要三个样式
- **border-width 边框的宽度：默认3px**(可以省略不写)
  border-top-width 上边框的宽度
  border-right-width 右边框的宽度
  border-bottom-width 下边框的宽度
  border-left-width 左边框的宽度
- **border-color 边框的颜色：默认使用color的颜色值**
  border-top-color 上边框的颜色
  border-right-color 右边框的颜色
  border-bottom-color 下边框的颜色
  border-left-color 左边框的颜色
- **border-style 边框的样式：没有默认值，必须指定**
  border-top-style 上边框的样式
  border-right-style 右边框的样式
  border-bottom-style 下边框的样式
  border-left-style 左边框的样式

```css
.box1{
    border-width: 10px;
    border-color: red;
    /* 
    	solid  实线 
    	dotted 点状虚线 
    	dashed 虚线 
    	double 双线 
    */
    border-style: solid;
}
```

- 不论是`border-width` 、 `border-color` 、`border-style` 还是其衍生出来的属性写法，都可以指定每个方向的边框情况

  设定几个值就决定了对应方向的宽度、颜色或样式

  - 四个值：`上 右 下 左`
  - 三个值：`上 左右 下`
  - 两个值：`上下 左右`
  - 一个值：`上下左右`
  - 【顺时针方向设置】

- border简写属性：通过该属性可以同时设置边框所有的相关样式，并且没有顺序要求

  - `border-top` 上边框的宽度、颜色和样式
  - `border-right` 右边框的宽度、颜色和样式
  - `border-bottom` 下边框的宽度、颜色和样式
  - `border-left` 左边框的宽度、颜色和样式
  - 可以不要哪边写个none就行了

```css
.box1{ 
	border: 10px red solid;
}

```

#### 外边距（margin）

外边距，也叫空白边，位于盒子的最外围，是添加在边框外周围的空间。空白边使盒子之间不会紧凑地连接在一起，是CSS 布局的一个重要手段

**外边距不会影响盒子可见框的大小，但是外边距会影响盒子的位置和占用空间**

margin外边距的简写属性，可以同时指定四个方向的内边距，规则和边框中属性值设置一样

margin会影响到盒子实际占用空间

一共有四个方向的外边距：

- ` margin-top` :上外边距
  - 设置正值，元素自身向下移动
  - 设置负值，元素自身向上移动
-  ` margin-right`:右外边距
  - 设置正值，其右边的元素向右移动
  - 设置负值，其右边的元素向左移动
  - 上述说法并不准确，对于块元素，设置`margin-right`不会产生任何效果

-  `margin-bottom`:下外边距
  - 设置正值，其下边的元素向下移动
  - 设置负值，其下边的元素向上移动
  - 上述说法并不准确，对于块元素，会有垂直方向上的边距重叠问题
- `  margin-left`:左外边距
  - 设置正值，元素自身向右移动
  - 设置负值，元素自身向左移动

元素在页面中是按照自左向右的顺序排列的，所以默认情况下

- 如果我们设置的左和上外边距则会移动元素自身
- 而设置下和右外边距会移动其他元素

```html
.box1 {
    width: 200px;
    height: 200px;
    background-color: #bfa;
    border: 10px orange solid;
    margin-bottom: 100px;

}

.box2 {
    width: 200px;
    height: 200px;
    background-color: #bfa;
    border: 10px red solid;
    margin-top: 100px;
}

```

### 水平方向布局

元素在其父元素中水平方向的位置由以下几个属性共同决定，一个元素在其父元素中，水平布局**必须要满足**以下的等式

```
margin-left + border-left + padding-left + width + padding-right + border-right + margin-right = 其父元素的宽度
```

以上等式必须满足，如果相加结果使等式不成立，则称为**过渡约束**

- 如果这七个值中没有`auto`的情况，则浏览器会自动调整`margin-right`值以使等式满足

  `100 + 0 + 0 + 200 + 0 + 0 + 0 = 800` ==> `100 + 0 + 0 + 200 + 0 + 0 + 500 = 800`

- 如果这七个值中有`auto`的情况，则会自动调整`auto`值以使等式成立
- 这七个值中有三个值可以设置为`auto` ：`width`、`margin-left`、`maring-right`

1/如果某个值为auto，则会自动调整`auto`的那个值以使等式成立

2/如果宽度为`auto`，则宽度会调整到最大，其他`auto`的外边距会自动设置为0

3/如果外边距都为`auto`，则`auto`的外边距会自动均分以使等式成立

【所以我们进程利用这个特点来使一个元素在其都元素中水平居中】

### 垂直方向布局

默认情况下父元素的高度被内容撑开

#### 元素溢出

子元素是在父元素的内容区中排列的，如果子元素的大小超过了父元素，则子元素会从父元素中溢出

使用`overflow`/`overflow-x`/`overflow-y`属性来设置父元素如何处理溢出的子元素

可选值：`visible`/`hidden`/`scroll`/`auto`

`visible` 溢出内容会在父元素外部位置显示，默认值

`hidden` 溢出内容会被裁剪，不会显示

`scroll` 生成两个滚动条，通过滚动条来查看完整的内容

`auto` 根据需要生成滚动条

```html
<style>
    .box1 {
        width: 200px;
        height: 200px;
        background-color: #bfa;
        border: 10px orange solid;
        overflow: visible; /* 默认值 */
    }
</style>
<div class="box1">
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Asperiores aspernatur illo inventore
    deleniti laudantium quaerat excepturi sed quidem tempore? Eaque, cumque porro. Fuga quam error cupiditate quasi
    eveniet in numquam!
</div>

```

#### 边距折叠

垂直外边距的重叠（折叠）：相邻的垂直方向外边距会发生重叠现象

#### 兄弟元素

兄弟元素间的相邻，垂直外边距会取两者之间的较大值（两者都是正值）

特殊情况：

- 如果相邻的外边距一正一负，则取两者的和

- 如果相邻的外边距都是负值，则取两者中绝对值较大的

- ```html
  .box1,.box2{ 
      width:200px; 
      height:200px; 
      font-size:100px;
  }
  
  .boxl{
      background-color: #bfa;
      /*设置一个下外边距*/
      margin-bottom: 100px;
  }
  
  .box2{
      background-color: orange;
      /*设置一个上外边距*/
      margin-top: 100px;
  }
  ```

兄弟元素之间的外边距的重叠，对于开发是有利的，所以我们不需要进行处理
