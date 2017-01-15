CSS





# CSS入门基础

## css基础语法

### 基础语法规则

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明。

```
selector {
    declaration1; 
    declaration2;
    ... 
    declarationN;
}

```

选择器通常是您需要改变样式的 HTML 元素。 每条声明由一个属性和一个值组成。每个属性有一个值。属性和值被冒号分开。

```
selector {property: value}

```

例如：

```
h1{
   color:red;
   font-size:14px;
}

```

***<u>属性大于 1 个之后，属性之间用分号隔开</u>***。这行代码的作用是将 h1 元素内的文字颜色定义为红色，同时将字体大小设置为 14 像素。

下面的示意图为您展示了上面这段代码的结构：

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid248time1423292345665)

***注意：如果值大于 1 个单词，则需要加引号,如下：***

```
p{font-family:"sans serif"}
```

# 基础选择器

## 一、派生选择器

**派生选择器** **通过依据元素在其位置的上下文关系来定义样式，可以使标记更加简洁。**

派生选择器允许你根据文档的上下文关系来确定某个标签的样式。通过合理地使用派生选择器，我们可以使 HTML 代码变得更加整洁。 比方说，你希望列表中的 strong 元素变为红色，而不是通常的黑色，可以这样定义一个派生选择器：

```
li strong{
    color: red;
}

```

请注意在 HTML 中标记为

**的代码的上下文关系**

```
<p><strong>我是黑色，因为我不在列表当中，所以这个规则对我不起作用</strong></p>
        <u1>
            <li><strong>我是红色。这是因为 strong 元素位于 li 元素内。</li>
        </u1>

```

**注意：**实验楼环境中没有中文输入法，代码中涉及的中文主要是为了方便大家理解，大家可以英文做相应的替代。

### 完整代码如下：

index.html

```
<!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <link rel="stylesheet" href="mycss.css" type="text/css">
    </head>
    <body>
        <p><strong>我是黑色，因为我不在列表当中，所以这个规则对我不起作用</strong></p>
        <u1>
            <li><strong>我是红色，这是因为 strong 元素位于 li 元素内。</strong></li>
        </u1>
    </body>
</html>
```

mycss.css

```
li strong{
    color: red;
}

```

运行结果：

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid249time1423473784761)

**在 css 中定义的 li strong 的样式，只会影响上面 html 文件中的,而不会影响中的内容**

## 二、id 选择器

**1.id 选择器：** id 选择器可以为标有 id 的 HTML 元素指定特定的样式 id 选择器以“#”来定义

**2.id 选择器和派生选择器：** 目前比较常用的方式是 id 选择器常常用于建立派生选择器

上面两点单从字面意思很难理解，我们通过案例进行讲述。

### 程序举例

index.html 代码 body 中的 p 标签和 div 标签包含了两个 id 属性，值分别为 pid 和 divid，在 css 文件中会以#+属性值引用。注意：id 属性值只能在每个 HTML 文档中出现一次。

```
<!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <link  href="MyCss.css" type="text/css" rel="stylesheet">
    </head>
    <body>
        <p id="pid">hello css<a href="www.shiyanlou.com">shiyanlou</a></p>
        <div id="divid">this is a div</div>

    </body>
</html>
```

MyCss.css `#divid{}`就是一个独立的 id 选择器，而`#pid a{}`就是我们前文提到的 id 选择器用于建立派生选择器,相当于是一个嵌套。

```
#pid a{
    color:#00755f;
}
#divid {
    color: red;

```

运行结果： ![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid249time1423478143796)

**说明**：brackets 可以采用下面的方式调节颜色(在颜色值处右键)

![img](https://dn-anything-about-doc.qbox.me/css/2-3.png)



## 三、类选择器

### (1)在 CSS 中，类选择器以一个点号显示：

```
.divclass {
    color: red;
}

```

在下面的 html 代码中，div 元素含有 divclass 类，意味着它要遵守`.divclass`的规则。

```
<div class="divclass">
hello div
</div>

```

**注意：**类名的第一个字符不能使用数字！它无法在 Mozilla 或 Firefox 中起作用。

### (2)和 id 一样，class 也可被用作派生选择器：

```
.pclass a{
    color: green;

```

上述内容的全部代码如下

### 程序举例

index.html

```
<!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <link  href="MyCss.css" type="text/css" rel="stylesheet">
    </head>
    <body>
    <!--p 标签中嵌套了一个 a 标签，在下面的 css 引用过程中我们可以看到的.pclass a 即为 class 被用作派生选择器-->
        <p class="pclass">这是一个 class 显示效果<a href="hhtp://www.shiyanlou.com">效果</a></p>
        <div class="divclass">hello div</div>
    </body>
</html>

```

MyCss.css

```
.pclass a{
    color: green;
}
.divclass {
    color: red;
}

```

运行结果： ![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid249time1423539361459)



## 四、属性选择器

**对带有指定属性的 HTML 元素设置样式。**

### (1)下面的例子为带有 title 属性的所有元素设置样式：

```
[title]
{
color:red;
}

```

### (2)属性和值选择器

下面的例子为 title="te" 的所有元素设置样式：

```
[title=te]{
                color: red;
            }

```

### 程序代码举例

index.html

```
<!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style type="text/css">
            [title]{
                color: #00ff14;
            }
            [title=te]{
                color: red;
            }
              </style>    
    </head>
    <body>
       <p title=>属性选择器</p>
        <p title="te">属性和值选择器</p>
    </body>
</html>
```

# CSS 基本样式二超链接

针对一个超链接

<a href="http://www.shiyanlou.com">shiyanlou</a>



下面是 CSS 文件内容：

```
a:link {color:#FF0000;}    /* 未被访问的链接 */
a:visited {color:#00FF00;} /* 已被访问的链接 */
a:hover {color:#FF00FF;}   /* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}  /* 正在被点击的链接 */

```

我们先来看看效果： 这是未被访问的颜色：

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid251time1425361405882)

这是鼠标移动到链接上面的颜色：

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425361668570)

这是正在被点击的颜色：

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid251time1425361938929)

这是被点击之后的颜色：

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid251time1425361965736)

### 1.2CSS 设置链接背景颜色

这个一样的简单，修改对应的属性 background-color 就好。 我们动手实验的话，就将刚才的 CSS 文件替换或者添加：

```
a:link {background-color:#B2FF99;}
a:visited {background-color:#FFFF85;}
a:hover {background-color:#FF704D;}
a:active {background-color:#FF704D;}
```

### 1.3 修改链接下划线

不是所有的时候我们都需要链接下面的下划线，有时很影响美观。所以这里我们要在 link 属性中加入 text-decoration 属性，将传指改为空就行，修改过后就是下面的结果：

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid251time1425362974020)

# CSS盒子

## 1.CSS 盒子模型概述

我们先来看看盒子的组成包括： ***<u>margin(外边距);border(边框);padding(内边距);content(内容) 正文框的最内部分是实际的内容</u>***，直接包围内容的是内边距。内边距呈现了元素的背景。内边距的边缘是边框。边框以外是外边距，外边距默认是透明的，因此不会遮挡其后的任何元素。

下面我们就用一张图来描述下他们的结构：

![此处输入图片的描述](https://dn-anything-about-doc.qbox.me/document-uid13labid252timestamp1469495679179.png/wm)

内边距、边框和外边距都是可选的，默认值是零。但是，许多元素将由用户单独设置也可以使用通用选择器对所有元素进行设置，就相当与是一个初始化：

```
* {
  margin: 0;
  padding: 0;
}

```

从上面的图中可以看出，宽度（width） 和 高度（height） 指的是内容区域的宽度和高度。增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸。

可以如下设置这几个属性：

```
box {
  width: 70px;
  margin: 10px;
  padding: 5px;
}

```

> 外边距可以是负值，而且在很多情况下都要使用负值的外边距。

## 2.CSS 盒子模型内边距

内边据是什么：

***内边据在正文（content）外，边框（border）内***。控制该区域最简单的属性是 ***<u>padding 属性</u>***。padding 属性定义元素边框与元素内容之间的空白区域。

CSS padding 属性定义元素的内边距。padding 属性接受长度值或百分比值，但不允许使用负值。

你可以进行统一的内边距设置，也可以进行单边的内边距设置： 例如，如果您希望所有 h1 元素的各边都有 10 像素的内边距，只需要这样：

```
h1 {padding: 10px;}

```

您还可以按照***上、右、下、左的顺序***分别设置各边的内边距，各边均可以使用不同的单位或百分比值：

```
h1 {padding: 10px 0.25em 2ex 20%;}

```

如果只想设置某一边的那边据，我们也只可以办到的,只需通过以下四个属性：

- padding-top
- padding-right
- padding-bottom
- padding-left

顾名思义，这个是很好理解的。

在数值的设置中,我们前面讲到过,可以使用多种单位,常用的就是像素(px)和厘米(cm),这个比较简单,就简单的测试一下就好:

在 html 文件中写入一个表格,加上边框属性:

```
<table border="1">
    <tr>
        <td>
            <h1>正文<h1>
        </td>
    </tr>
</table>
```

这是未设置之前的页面:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425460265381)

css 文件



body{

    background-color: green;
}
h1{
    /**
    设置内外边距
     */
    padding-left: 5cm;
    padding-right: 5cm;
    padding-top: 30px;
    padding-bottom: 30px;
}

下面就是效果截图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425460546578)

## 3.CSS 盒子模型边框

***<u>元素的边框 (border) 是围绕元素内容和内边距的一条或多条线。 设置 border 属性可以规定元素边框的样式、宽度和颜色。</u>***

学习过 HTML 的同学都知道,在 HTML 中,我们常使用表格来创建周围的边框,但是通过使用 CSS 边框属性,我们可以创建出效果出色的边框,并且可以应用于任何元素.

每个 border 属性我们可以设置宽度,样式,以及颜色.下面我们就看看如何通过 border 属性来设置边框宽度,以及颜色:

> CSS 没有定义 3 个关键字的具体宽度，所以一个用户代理可能把 thin 、medium 和 thick 分别设置为等于 5px、3px 和 2px，而另一个用户代理则分别设置为 3px、2px 和 1px。

可以通过如下的内容

```
td {border-style: solid; border-width: 15px 5px 15px 5px;}

```

同样,这里我们也可以设置单边边框的宽度,

```
border-top-width
border-right-width
border-bottom-width
border-left-width
```

下面我们在 CSS 文件中加入

```
border-style: dashed;
  border-top-width: 15px;
  border-right-width: 5px;
  border-bottom-width: 15px;
  border-left-width: 5px;

```

下面是效果截图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425462801761)

说完宽度,我们再来看看颜色,设置边框颜色非常简单。CSS 使用一个简单的 border-color 属性，它一次可以接受最多 4 个颜色值,分别是边框的四边(具体顺序自己可以试试)。可以使用任何类型的颜色值，例如可以是命名颜色，也可以是十六进制和 RGB 值：

在 CSS 文档中添加以下内容:

```
  border-color: blue rgb(25%,35%,45%) #909090 red;

```

下面就是效果截图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425463413926)

同样可以使用属性控制各个边框的颜色,以达到相同的效果: border-top-color border-right-color border-bottom-color border-left-color

## 4.CSS 盒子模型外边距

外边距就是围绕在内容框的区域,可以参考上面的结构图.默认为透明的区域.同样,外边距也接受任何长度的单位,百分数.与内边据很相似 我们可以使用下列任何一个属性来只设置相应上的外边距，而不会直接影响所有其他外边距： margin-top margin-right margin-bottom margin-left 是不是很眼熟,这些属性都是这么相通,大家可以发散的联系

margin 的默认值是 0，所以如果没有为 margin 声明一个值，就不会出现外边距。但是，在实际中，浏览器对许多元素已经提供了预定的样式，外边距也不例外。例如，在支持 CSS 的浏览器中，外边距会在每个段落元素的上面和下面生成“空行”。因此，如果没有为 p 元素声明外边距，浏览器可能会自己应用一个外边距。当然，只要你特别作了声明，就会覆盖默认样式。

这里讲一讲的具体赋值:

值复制 还记得吗？我们曾经在前两节中提到过值复制。下面我们为您讲解如何使用值复制。 有时，我们会输入一些重复的值：

```
p {margin: 0.5em 1em 0.5em 1em;}

```

通过值复制，您可以不必重复地键入这对数字。上面的规则与下面的规则是等价的：

```
p {margin: 0.5em 1em;}

```

这两个值可以取代前面 4 个值。这是如何做到的呢？CSS 定义了一些规则，允许为外边距指定少于 4 个值。规则如下：

如果缺少左外边距的值，则使用右外边距的值。

如果缺少下外边距的值，则使用上外边距的值。

如果缺少右外边距的值，则使用上外边距的值。

反正就是对称复制

下面我们来举例说明:

```
h1 {margin: 0.25em 1em 0.5em;}  
/* 等价于 0.25em 1em 0.5em 1em */
h2 {margin: 0.5em 1em;} 
/* 等价于 0.5em 1em 0.5em 1em */
p {margin: 1px;}        
/* 等价于 1px 1px 1px 1px */

```

这里来一个简单的示例: html 文件内容如下:

```
<div class="wb">
    <div class="bk">
        <div class="nj">
            <div class="zw">
                shiyanlou
            </div>
        </div>
    </div>
</div>
```

CSS 文件内容如下:

```
.wb{
    margin: 100px;
}
.bk{
    border-style: groove;

}
.nj{
    padding: 10px;

}
.zw{
    background-color: cornflowerblue;

}

```

效果图如下:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425521842418)

这里还有个知识点,就是这是外边距的合并,外边框合并就是一个叠加的概念,下面我们用一张图来说明合并之前与合并之后的差别:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425520581681)

当我们将 HTML 文件中的 div 复制一遍之后我们会发现,效果是这样的:

![img](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425526121626)

***<u>按理这两个模块时间的间距是 200px,但是这里却是 100px,这就说明,默认的状态是合并的状态.</u>***

## 5.CSS 盒子模型应用

接下来我们就来练习下盒子模型,绘制一定的样式,实现下图的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425526087756)

我们先来分析下整体结构:最上面是有两部分组成,最上面的是 top,外边距内边距都为 0,上面还有个 topcenter,上下边距为 0,左右是居中状态:

实现 html 内容为:

```
<div class="top">
    <div class="topcenter"><h1>topcenter</h1></div>
</div>
```

CSS 内容为:

```
.top{
    background-color: steelblue;
    width: 100%;
    height: 70px;
    text-align: left;

}
.topcenter{
    margin: 0px auto;/*左右自适应,上下为 0*/
    width: 75%;
    height: 70px;/*与 top 一样*/
    background-color: cadetblue;
    text-align: center;

}
```

这样就能实现最上面的两个模块:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425531639714)

接下来就是中间部分,我们可以将其分成三部分,第一部分就是 middle,我们可以看出 middle 与上下都有外边距的存在,接下来就是 middle1 包含在 middle 中,宽度完全填充,高度自定义,middle2 宽度完全填充,上外边距有规定.

HTML 内容如下:

```
<div class="middle">
    <div class="middle1"><br/><h2>middle1</h2></div>
    <br/>
    <div class="middle2"><br/><h2>middle2</h2></div>
</div>

```

CSS 内容如下:

.middle{
​    width: 75%;
​    height: 700px;
​    margin: 8px auto;
​    background-color: gray;
}
.middle1{
​    width: 100%;
​    height: 30%;
​    background-color: cadetblue;
​    margin: 0px;
​    text-align: center;
}
.middle2{
​    width: 100%;
​    height: 10%;
​    margin: 10px 0px;
​    background-color: darkgreen;
​    text-align: center;
}

就可以完成如下的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425533360861)

最后我们再加上个底边: HTML:

```
<div class="bottom"></div>

```

CSS:

```
.bottom{
    margin: 0px auto;
    height: 50px;
    background-color: darkslategrey;
    width: 75%;
}

```

这样我们就完成了整个盒子模型的设计:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid252time1425533800510)



# CSS 高级

## 1.CSS 定位

定位的基本思想很简单，它允许你定义元素框相对于其正常位置应该出现的位置，或者相对于父元素、另一个元素甚至浏览器窗口本身的位置。

CSS 有三种基本的定位机制：

普通流:

元素按照其在 HTML 中的位置顺序决定排布的过程

浮动:

浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。

绝对定位:

绝对定位使元素的位置与文档流无关，因此不占据空间。这一点与相对定位不同，相对定位实际上被看作普通流定位模型的一部分，因为元素的位置相对于它在普通流中的位置。

定位属性:

position,将元素放在一个静态的,相对的,绝对的,或固定的位置

通过对 top,left,right,bottom 这四个属性的赋值让元素向对应的方向偏移

overflow 设置元素溢出其区域发生的事情

clip 设置元素的显示形状,多用于图片

vertical-align 设置元素的垂直对其方式

z-index 设置元素的堆叠顺序

接下来就着重来看看 position 属性: 为了形象,我们先建立一个 html 文件和 CSS 文件

html:

```
<div class="position1"></div>
<p>this is shiyanlou</p>
<p>this is shiyanlou</p>
<p>this is shiyanlou</p>
<p>this is shiyanlou</p>

```

CSS:

```
.position1{
    width: 100px;
    height: 100px;
    background-color: cornflowerblue;

}

```

接下来我们就可以看到普通流的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425540329640)

当我们在 CSS 中加入 position 赋值为相对的,向左偏移 60px

```
 position: relative;
 left: 60px;

```

接下来我们会看见:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425540720945)

下面我们再将 position 设置为绝对的:

```
position: absolute;

```

效果就变成了这样:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425540853272)

通过比较我么就能理解 position 这两个值的区别,还有两个属性就是 fixed,和 static,fixed 是将元素固定下来,就算滚动屏幕,它也会在同一个地方不会动;而 static 设置以后,偏移量什么的就没用了.

下面我们接着来看其他的属性

当我们再加一个块在前面 div 后面的时候: HTML

```
<div class="position1"></div>
<div class="position2"></div>

```

CSS 添加:

```
.position2{
    width: 100px;
    height: 100px;
    background-color: aquamarine;
    position: relative;
    left:10px;
    top: 10px;
}

```

就会出现下面的情况:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425542153214) 接下来我们就可以通过 z-index 来控制哪一块在最前面:

接下来我们就修改下 CSS 文件来交换他们的前后顺序: position1 中加入

```
z-index: 2;

```

position2 中加入:

```
z-index: 1;

```

就可以达到交换的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425542449027)

## 2.CSS 浮动

这里涉及到的属性就是 float,其值可以赋值为:

left:元素向左浮动 right:元素向右浮动 none:不浮动 inherit:从父级继承浮动的属性

还有一个就 clear 属性: 主要用于去掉向各方向的浮动属性(包括继承来的属性)

下面我们就先创建一个最基础 html 和 CSS 文件,下面是基础内容:

html:

```
    <div class="qd"></div>
    <div class="wd"></div>
    <div class="ed"></div>

```

CSS

```
.qd{
    width: 100px;
    height: 100px;
    background-color: lightskyblue;

}
.wd{
    width: 100px;
    height: 100px;
    background-color: lightseagreen;

}
.ed{
    width: 100px;
    height: 100px;
    background-color: lightsalmon;

}

```

下面是显示效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425544947196)

在这个基础上我们他们全加上 float 属性,前两个往左,后一个向右,看看会有什么效果:

```
float: left;
float: right;

```

效果图

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425545256313)

就像几个小东西在一个房间里面跑,你可以规定它跑的方向,他们会跑到边框为止,为了测试,我们不妨来限定一个空间给它们(将这三个 div 全放到一个 div 中).就像这样:

```
<div class="container">
    <div class="qd"></div>
    <div class="wd"></div>
    <div class="ed"></div>
</div>

```

接下来你就会看见:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425545488300)

但是有时我们不需要浮动,就像下面这样,我们想在上面效果下面加上一句话,然后我们就直接加入了一个

```
<div class="text">hello shiyanlou</div>

```

在 container 中.然后我们会看见

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425546630117)

这说明,这个 div 也继承了浮动的属性,要想让字体到下面去,我么就必须取消字体 div 浮动.那么我们就在 CSS 中添加如下如下内容:

```
.text{
    clear: both;
}

```

效果图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425546811461)

## 3.CSS 尺寸

尺寸属性允许你控制元素的高度和宽度。同样，它允许你增加行间距。 涉及到的属性有

height-- 设置元素的高度。 line-height --设置行高。 max-height-- 设置元素的最大高度。 max-width --设置元素的最大宽度。 min-height --设置元素的最小高度。 min-width --设置元素的最小宽度。 width --设置元素的宽度。

下面我们就写个 html 和 CSS 文件来具体比较下

```
.p1{
    line-height: normal;
    width: 400px;

}

.p2{
    line-height: 50%;
    width: 400px;

}

.p3{
    line-height: 200%;
   width: 400px;

}

```

效果图如下:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1425548602580)

## 4.CSS 导航栏

不管是什么网页,都会有导航栏来表述本网页所包含的内容,一般导航栏分为:水平导航栏,垂直导航栏.下面我们就来定制下自己的导航栏.

垂直导航栏:

首先我们以列表的形式作为最基础的承载,然后我们再其中加入本地或外部的链接,就像下面这样:

```
<ul>
    <li><a href="http://www.shiyanlou.com">shiyanlou1 link</a></li>
    <li><a href="http://www.shiyanlou.com">shiyanlou2 link</a></li>
    <li><a href="http://www.shiyanlou.com">shiyanlou3 link</a></li>
    <li><a href="http://www.shiyanlou.com">shiyanlou4 link</a></li>

</ul>

```

然后我们就会得到这样的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1426038092682)

我们一般看见的导航栏都没有下划线,和前面的带点,并且当我们的鼠标移到链接上面时链接的颜色会发生相应的变化,这就是我们现在要让 CSS 实现的效果.

首先,我们要去掉前面的点

```
ul{
    list-style: none;
}

```

接下来我们就去掉下划线(不管是未被点击的状态还是已被点击的状态都去掉),然后加上个背景颜色,再将其显示作为块来显示:

```
a:link,a:visited{
   text-decoration: none;
   background-color: lightgray;
    display: block;
}

```

最后我们再给导航栏加个鼠标移动到上面时,改变背景颜色:

```
a:active,a:hover{
    background-color: cadetblue;

}

```

下面就是效果图

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1426039329121)

垂直的效果图讲完之后,我们再来讲讲水平的导航栏,我们就只需要修改 CSS 文件就可以了.

首先我们要将前面的显示效果删除,就是这句:

```
 display: block;

```

然我们只需要在 li 标签中改变显示方式就可以:

```
li{
    display: inline;
}

```

这样就可以实现水平导航栏

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1426039831432)

我们可以根据自己的喜好,设置边距,字体,颜色等等.这里我么不就不再一一的讲述.

## 5.CSS 图片

首先我们先引入一张图片,加上一句描述语,使用 div 承载.

```
    <div class="image">
    <a href="./1348306907524.jpg" target="_self">
        <img src="1348306907524.jpg" width="150px" height="150px">
    </a>
    </div>
    <div>beautiful </div>

```

就是下面的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1426041769926)

接下来我们就开始定制图片的显示:

图片加边框,修改描述字体中对其,修改字体大小,将整个 div 向左浮动,使边框与图片进行贴合:

```
.image{
    border: 2px solid darkgrey;
    width: auto;
    height: auto;
    float: left;
    text-align: center;
    padding: 5px;

}
img{
    padding: 5px;
}
.text{
    font-size: 20px;
    margin-bottom: 5px;

}

```

这就是处理过后的的效果

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1426042557280)

之后我么再设计图片的透明度: 这个比较简单,就只需要在图片 CSS 设置中加入:

```
opacity: 0.5;

```

这个属性的值范围为 0-1 设置透明度,0 为完全透明,1 代表完全不透明.

下面就是半透明的效果图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid253time1426043303004)

## 小结

这一章中我们学习了 CSS 基本的高级设置,包括:定位,浮动,尺寸,导航,图片.这些都是 在平时用的很多的设置.

## 练习

根据教程练习上面讲到的高级设置及属性,熟练掌握这些讲到的设置.

![img](https://static.shiyanlou.com/img/vip-icon.png) 升级实验楼会员

精品课程+环境保存+会员客户端

[[获取会员特权\]](https://www.shiyanlou.com/vip)

[** 停止实验](https://www.shiyanlou.com/courses/running#stop-lab-modal) [** 下一个实验](https://www.shiyanlou.com/courses/running#next-lab-modal)

** 纠错

隐藏工具栏

59:05 [延时](https://www.shiyanlou.com/courses/running#increase-time-modal)

[** 切换界面](undefined)[** 图形界面](undefined) [** 字符界面](undefined)[**](undefined)



## css选择器

# CSS选择器

前面几个章节我们简单介绍过选择器,大家应该会对选择期有一些基础的了解,下面我们就来具体的讲述下面几个选择器.

## 1.元素选择器

1.最常见的选择器就是元素选择器,文档的元素就是最基本的选择器.

就像这些: h1{}. a{}等

css 文件可以这样实现:

```
h1{
  color: cadetblue;  
}

```

这样的实例很多,这里就不一一举例了. 很简单吧.这就叫元素选择器,下面我们来讲讲选择器的分组.

## 2.选择器分组

在原来的基础上我们想将下面 html 文件中的文件都设置成一样的颜色,我们可以这么干: html:

```
<h1>shiyanlou</h1>
<h2>shiyanlou</h2>
<h3>shiyanlou</h3>
<h4>shiyanlou</h4>

```

css:

```
h1{
  color: cadetblue;

}
h2{
    color: cadetblue;

}
h3{
    color: cadetblue;

}
h4{
    color: cadetblue;

}

```

这样就是下面的效果图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426054624332)

但是我们一般会这样写 css:

```
h1,h2,h3,h4{
  color: cadetblue;
}

```

效果是一样的,完全没有变化:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426054671586)

这样是不是减少了不少代码,这就叫做选择器的分组. 下面我们要补充的知识就是通配符*. 要想达到与前面相同的效果,还有一种方式就是,用通配符.

```
*{
  color: cadetblue;
}

```

这样一来的话,如果没有特定元素的设置,都会发生颜色的转换.下面有同学就要提问了,要是我们不想全一样,其中有几个采用别的设置呢.

解决这个问题我们就只需要进行覆盖就好.如果我们想让最后一个标题变成黑灰色,那么在后面加上下面这句就好:

```
h4{
    color: darkslategray;
}

```

这样的话,我们就能看见下面的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426055601418)

但是一般我们使用通配符的时候就是设置整个页面的内边距和外边距.就像这样

```
*{
    padding: 0px;
    margin: 0px;
}

```

下面我们再来讲讲类选择器

## 3.类选择器

类选择器允许以一种独立与文档元素的方式来制定样式

例如: .class{}(注意是点开头的哦,这是类选择器的标志,点后面是属性名,大括号里面就是具体的设置)

下面我们就来简单举例:

html 文件:

```
<div class="div">
    shiyanlou is my home
</div>

```

css 文件:

```
.div{
color: cadetblue;

}

```

这样就可以实现定制效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426057904950)

前面我们还接触过,将类选择器结合元素选择器来使用.下面再添加一个:

```
<h1 class="div">shiyanlou is my home</h1>

```

下面我们将 css 文件如下修改:

```
h1.div{
color: cadetblue;
}

```

这样在类选择器前面加了元素描述以后,这个.div 就只会对 h1 起作用.

下面我们来看看具体的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426058289794)

下面我们要讲的就是多类选择器:.class.class{} 这个在先前我们没有接触过.下面我们就来边写边感受: html 文件列出几个 p 字段,到时好比较:

```
<p class="p1">shiyanlou is my home</p>
<p class="p2">shiyanlou is my home</p>
<p class="p3">shiyanlou is my home</p>

```

css 文件没一个选择器修改一处设置,地一个颜色蓝黑,第二个字体大小 20px,第三个字体样式斜体:

```
.p1{
    color: cadetblue;
}
.p2{
    font-size: 20px;
}
.p3{
    font-style: italic;
}

```

下面就是效果截图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426059117787)

下面我们就来使用多类选择器:

这里就只需要将 css 文件中 p3 改为 .p1.p2 就好,另外在 html 引用时将第三个 p 标签 class 进行修改: css:

```
.p1.p2{
    font-style: italic;
}

```

html:

```
<p class="p1 p2">shiyanlou is my home</p>

```

下面就是结果图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426059366447)

这里我们看出,第三个段即有 p1 颜色的修改,也有 p2 字体大小的修改,还有自己斜体的修改.这就是多类选择器的应用.

## 4.id 选择器

id 选择器类似于类选择器,当然还是有很多不同的地方

id 选择器的引入是用"#",就和类选择器的"."是一样的效果.示例:#div{} 下面我们就来具体实验一把: html:

```
<p id="div">shiyanlou is my home</p>

```

css:

```
div{
    color: cadetblue;
}

```

效果图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426059850989)

因为 id 和类选择器很相似,这里我们就主要讲解他俩的区别:

id 顾名思义只能在文档中使用一次,而类可以使用多次 id 选择器不能像刚才类选择器一样结合使用 后面大家会了解到,关于网页渲染也有区别,这里不赘述.

## 5.属性选择器

简单的属性选择器: 例如:[title]{}

下面我们先来看看最简单的属性选择器的是怎样实现的: html: 在 head 中添加

```
  [title]{

        color: cadetblue;
    }

    </style>

```

在后面加入一个 p 标签:

```
<p title="li">shiyanlou is my home</p>

```

这样以后我们就得到这样的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426061219412)

属性选择器还可以根据具体属性值选择,为了确定设置范围,仅让有特定属性的元素进行设置:

下面我们来看看示例:

我们在 head 中添加 a 属性选择器,使其变色,在 body 中设立两个 a 标签来对比,一个 href 是和上面的属性选择器相等,后面一个与属性选择器不相等:

```
a[href="http://www.shiyanlou.com"]{
        color: cornflowerblue;

        }

```

```
<a href="http://www.shiyanlou.com">shiyanlou right</a>
<a href="http://www.baidu.com">baidu</a>

```

让我们来看看效果图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426061998762)

也就像前面类选择器前家一个元素进行定位,筛选一样.

## 6.后代选择器

后代选择其可以选择作为某元素后代的元素 首先我么在 body 中加入一个 p 标签,并且在里面嵌套一个 strong 子标签:

```
<p>shiyanlou is <strong>my</strong> home</p>

```

然后我们希望将 my 这个单词设置颜色.其余的不动,这样我们就要在 css 中使用后代选择器来设置: css:

```
p strong{
    color: cadetblue;
}

```

下面就是我们的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426063168966)

这就是我们后代选择器的使用,一般我们会用来着重某一句话或者某个字.下面我们就来看看子元素选择器.

## 7.子元素选择器

与后代选择器相比,子元素选择器只能选择作为某子元素的元素 范例就是后面这样:h1>strong{};我们这就来试试.

html:

```
<h1>shiyanlou is my <strong>home</strong></h1>

```

css:

```
h1 > strong{
    color: cadetblue;
    font-size: 60px;
}

```

下面就是我们的效果图:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426063783553)

## 8.相邻兄弟选择器

相邻兄弟选择器可以选择紧接在另一个元素后的元素,且二者有相同的父级元素,势力:h1+p{};

兄弟选择器多用于列表,具有相同的父级元素 ul,下面我们就来写一个实例: html:

```
<ul>
    <li>shiyanlou</li>
    <li>shiyanlou</li>
    <li>shiyanlou</li>
</ul>

```

css:

```
li+li{
    color: cadetblue;
    font-size: 40px;
}

```

这就是最后的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid254time1426064937838)

## 小结:

上面我们讲到了这么多选择器,其实在一般的开发中我们就只会用到一些常用的选择器,比如类选择器,id 选择器,元素选择器,其余的作为了解就好.

## 练习:

根据讲解,自己动手实验各种选择器.

![img](https://static.shiyanlou.com/img/vip-icon.png) 升级实验楼会员

精品课程+环境保存+会员客户端

[[获取会员特权\]](https://www.shiyanlou.com/vip)

[** 停止实验](https://www.shiyanlou.com/courses/running#stop-lab-modal) [** 下一个实验](https://www.shiyanlou.com/courses/running#next-lab-modal)

** 纠错

隐藏工具栏

59:40 [延时](https://www.shiyanlou.com/courses/running#increase-time-modal)

[** 切换界面](undefined)[** 图形界面](undefined) [** 字符界面](undefined)

## HTML与css简单页面效果实例

# HTMl 与 CSS 简单页面效果实例

## 1.总体实验概述(结构)

前面我们讲述了 css 的基础知识,这里我们来做一个整体的练习,回顾下我们前面学到的知识.首先我们来看一下我们需要实现的页面样式

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid255time1426145353709)

这是小编提前做好的,下面我们就具体的来分下要怎样实现.

我们最先要做的,就是分析整个网页的结构,我们可以发现,我们大致可以将整个页面分为三个部分. 第一部分是头部,上面有标题,导航,还有表单,最后一个小插图. 第二部分是主体,其中有文字描述,有下划线,有图片的排布(细节过下再说). 第三部分就是最简单的脚部,这里就不多说

下面我们用一张结构图来描述下这个页面的结构,进一步加深同学的理解:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid255time1426145754828)

从图上我们就可以看出,没一个模块用一个 div 块来描述就很简单了,只是运用前面学到的知识对细节进行优化就好.下面我们就开始具体的讲述每一个部分的实现.

## 2.head 部分

从结构图上我们可以看出,这个部分要实现的功能比较多,首先我们要定义一个 div 来承载这样一个标题(这个超简单), html:

```
<div class="headtitle"><h2>Colorful Life</h2></div>

```

后面我们要做的就是加上导航,导航利用列表引入,我们知道列表默认的列表会垂直排布,这里我们需要将其设置成为水平排布,为了美观,我们还需要适当加上内边据和外边距

html:

```
<div class="headlead">
               <ul>
                  <li><a href="./cabin.png">Working</a></li>
                   <li><a href="./cake.png">Eating</a></li>
                   <li><a href="./game.png">Playing</a></li>
                   <li><a href="./circus.png">Sleeping</a></li>
               </ul>
           </div>

```

css:

```
li{
    padding: 2px;
    display: inline;

}

```

既然是导航,列表元素必定是链接,涉及到链接,我们就要设置,是否去掉下划线,鼠标移动到上面有什么变化,单击之前是什么颜色,点击之后是什么颜色(这里简单设置):

css:

```
a:link,a{
    color: snow;
    text-align: center;
    padding: 2px;
    text-decoration: none;

}
a:hover{
    color: black;
}

```

在右边我们需要插入一个图片,让它浮动在最右边.

html:

```
<div class="headimage">
               <img src="profile.png">
           </div>

```

css:

```
.headimage{

    float: right;
    margin-top: 30px;
    margin-right: 5px;



}
.headimage img{
    height: 60px;
    width: 60px;
}

```

这些都是比较简单的设置,前面我们都讲到过的,下面就还剩一个输入文字的表单,小编的审美及只能这样了,我们只需设置表单设置边框为圆弧,背景颜色,还有输入类型就好.下面显而易见的设置,至于自己想怎样发挥,就随大家了.

html:

```
 <div class="headform">
               <form>
                   <input type="text">
               </form>
           </div>

```

css

```
.headform form{
    float: right;
    height: 26px;
    margin-right: 50px;
}

form input{
    height: 20px;
    background-color: cadetblue ;
    width: 100px;
    margin-top: 50px;
    border-radius: 30px;

}

```

当写完这些效果以后我们来具体的展示:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid255time1426149016796)

在这里我们可以看出上面我们写的导航的效果.

## 3.body 部分

从结构图中我们可以看出,这部分无非就是两大模块,一段的文描述加上下面的图片排列.记得在上一章中我们详细讲述了 css 中的图片样式,图片的排版方式,相信大家映像都还很深吧下面我们就来具体的写写.

首先我们在把文字描述写出来:

html:

```
 <div class="bdytitle">
               <h3>enjoy everyday of us</h3>
               <p>let's study with us ,improve with us,we need you</p>
           </div>

```

在 css 中我们设定字体颜色模块边距等:

```
.bdytitle{
    color: snow;

}
.bdytitle p{
    margin: 20px;

}

```

下面这部分就是上一节中的图片排版,这里主要涉及到图片的边框,大小,设置浮动,我就举一个例子:

html:

```
<div class="img1">
               <img src="cabin.png">
               <p>Working</p>
           </div>

```

css:

```
.img1{
    border: 2px solid lightgray;
    float: left;
    text-align: center;
    margin: 10px 10px;



}
.img1 img{
    width: 250px;
    height: 220px;

}
.img1 p{
    color: snow;
    font-size: 20px;

}

```

我们就会得到下面的效果:

![图片描述信息](https://dn-anything-about-doc.qbox.me/userid20407labid255time1426150555246)

下面我们来看看最简单的 foot 部分

## 4.foot 部分

在网页的最后我们加上了一个底框:

html:

```
 <div class="foot">
        shiyanlou

       </div>

```

css:

```
.foot{
    text-align: center;
    background-color: lightgray;
    height: 50px;
    padding: 20px;
    font-size: 30px;
    color: darkslategrey;

}

```

我们就简单的设置下字体对齐方式,背景颜色,等基础配置就好

## 小结

在这一章中我们将 html 与 css 结合做了一个小实验,希望大家回顾起以前所学到的知识.

## 练习

根据实验讲解,动手做一个属于自己的小网页

补充:整个实验的工程可以用以下方式下载

```
git clone http://git.shiyanlou.com/shiyanlou/cssfinaltest

```

![img](https://static.shiyanlou.com/img/vip-icon.png) 升级实验楼会员

精品课程+环境保存+会员客户端

[[获取会员特权\]](https://www.shiyanlou.com/vip)

[** 停止实验](https://www.shiyanlou.com/courses/running#stop-lab-modal)

** 纠错

隐藏工具栏

59:51 [延时](https://www.shiyanlou.com/courses/running#increase-time-modal)

[** 切换界面](undefined)[** 图形界面](undefined) [** 字符界面](undefined)

