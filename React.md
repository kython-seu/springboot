# 定义

```javascript
var h1 = <h1>Hello World</h1>;
```

The part that looks like HTML, <h1>Hello world</h1>, is something called JSX.

JSX是一种JavaScript的语法扩展，这是React使用的。为什么说JSX是JavaScript的语法扩展呢，因为Web Browser不能读它，必须经过编译。即需要一个JSX编译器将JSX翻译成常规的JavaScript。需要搭建一个JSX编译器。

<h1>Hello World</h1>就是一个JSX元素。看起来很像HTML，唯一的区别就是你是在JavaScript文件里看到的它而不是HTML文件



JSX element 可以存储在变量里，对象里或者数组里

比如存在变量里：

```javascript
var navBar = <nav>I am a nav bar</nav>;
```

存在对象里

```javascript
var Pistons2004 = {
  center:        <li>Ben Wallace</li>,
  powerForward:  <li>Rasheed Wallace</li>,
  smallForward:  <li>Tayshaun Prince</li>,
  shootingGuard: <li>Richard Hamilton</li>,
  pointGuard:    <li>Chauncey Billups</li>
};
```

JSX element可以具有属性，就像HTML element可以有一样。格式也是用引号括起来。像这样：

my-attribute-name="my-attribute-value"

<a href="http://www.yahoo.com">Welcome to the Yahoo</a>;

var title = <h1 id="title">Introduction to React.js: Part I</h1>;

JSX element可以同时具有很多属性，就像HTML，如

```javascript
var panda = <img src="images/panda.jpg" alt="panda" width="500px" height="500px" />;


var p1 = <p>foo</p>;
var p2 = <p>bar</p>;
p1 = <p id="large">foo</p>;
p2 = <p id="small">bar</p>;
```

我们可以把 JSX element 放置在其他JSX element里面（嵌套），也像HTML一样。如

```html
<a href="https://www.google.net"><h1>Click me I am Google</h1></a>

<a href="https://www.google.net">
  <h1>
    Click me I am Goooogle
  </h1>
</a>
```

如果JSX expression 占了不止一行，那么你应该用（）包裹起来如下：

```html
(
  <a href="https://www.google.net">
    <h1>
      Click me I am Goooooogle
    </h1>
  </a>
)
```

嵌套的JSX expression 可以被保存在变量中，传递给函数等等就像非嵌套的JSX expression那样。

```javascript
var myDiv = (
	<div>
    <h1>Hello world</h1>
  </div>
);
```

*注意：JSX expression必须只有一个最外边的element，具体如下*

```javascript
var paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);
```

这是合法的

```javascript
var paragraphs = (
  <p>I am a paragraph.</p> 
  <p>I, too, am a paragraph.</p>
);
```

这是非法的，（）里面有两个最外边的element，两个<p></p>

If you notice that a JSX expression has multiple outer elements, the solution is usually simple: wrap the JSX expression in a <div></div>万能解决方法啊.



下面我们写个blog.js

```javascript
var blog = (
  <div>
    <img src="pics/192940u73.jpg" />
    <h1>
      Welcome to Dan's Blog!
    </h1>
    <article>
      Wow I had the tastiest sandwich today.  I <strong>literally</strong> almost freaked out.
    </article>
  </div>
);
```

# 渲染JSX expression

写一个js文件，命名为app.js，然后渲染一个h1

```javascript
app.js
var React = require('react');
var ReactDOM = require('react-dom');

// Copy code here:
ReactDOM.render(<h1>Hello world</h1>, document.getElementById('app'));
```

代码分析

ReactDOM是一个JavaScript库，此库封装了专门用于处理DOM相关的方法。如ReactDOM.render。这是最常见的渲染JSX的方法了，根据JSX表达式，创建一相应的DOM 节点树，并将此书add到DOM里，进而让其显示在WEB上。ReactDOM.render的第一个元素应该是一个JSX表达式，就是将这个表达式渲染到web 浏览器里。

```javascript
var React = require('react');
var ReactDOM = require('react-dom');

// Write code here:
ReactDOM.render(<h1>Render me!</h1>,
               document.getElementById("app"));
```

现在来介绍介绍这第二个参数，我们上面已经知道第一个参数是用于显示的内容，那么问题来了，这内容显示在哪儿？

看看我们写的html

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<link rel="stylesheet" href="/styles.css">
	<title>Learn ReactJS</title>
</head>

<body>
  <main id="app"></main>
	<script src="https://s3.amazonaws.com/codecademy-content/courses/React/react-course-bundle.min.js"></script>
  <script src="/app.compiled.js"></script>
</body>

</html>
```

你就可以发现那个id="app"的那个html元素了<main id="app"></main>这个东西就是充当第一个参数的容器，最终id为app的html就变成了这样

```html
<main id="app">
  <h1>Render me!</h1>
</main>
```

使用自定义属性

添加自定义属性需要使用 **data-** 前缀，如下

```javascript
ReactDOM.render(
	<div>
	<h1>菜鸟教程</h1>
	<h2>欢迎学习 React</h2>
    <p data-myattribute = "somevalue">这是一个很不错的 JavaScript 库!</p>
    </div>
	,
	document.getElementById('example')
);
```

# 独立文件

我们可以把react jsx代码写入到一个独立的js文件里，然后通过<script>来引用

```html
<script type="text/babel" src="helloworld_react.js"></script>
```

# JSX使用javascript表达式

JSX 使用javascript表达式很简单，只需要使用{}括起来就可以了。

如下：

```javascript
ReactDOM.render(
<div>
<h1>{1+1}</h1>
</div>,document.getElementById("app"));
```

在JSX不能使用if else语句，但是可以使用conditional（三元运算）

```javascript
<script type="text/babel">
	  var i = 1;
      ReactDOM.render(
      	<div>
      	  <h1>{i == 1 ? 'True!' : 'False'}</h1>
        </div>
      	,
      	document.getElementById('example')
      );
    </script>
```

# 样式

React 推荐使用内联样式，可以使用驼峰命名法。例如:

```javascript
var myStyle = {
  fontSize:100,
  color:'#FF0000'
};
ReactDOM.render(
<h1 style = {myStyle}>hello</h1>,
document.getElementById("app"));
```

# 注释

注释是放在{/*........*/},必须放在花括号里

```javascript
ReactDOM.render(
<div>
<h1>hello </h1>
{/*此处是注释*/}
</div>,
document.getElementById("app")
);
```

# JSX使用数组

```javascript
var arr = [
  <h1>haha</h1>,
  <h2>kkkk<h2>,
];
ReactDOM.render(
<div>{arr}</div>,document.getElementById("app"));
```

# HTML标签VS React组件

React 可以渲染 HTML 标签 (strings) 或 React 组件 (classes)。

要渲染 HTML 标签，只需在 JSX 里使用小写字母的标签名。

```
var myDivElement = <div className="foo" />;
ReactDOM.render(myDivElement, document.getElementById('example'));
```

要渲染 React 组件，只需创建一个大写字母开头的本地变量。

```
var MyComponent = React.createClass({/*...*/});
var myElement = <MyComponent someProperty={true} />;
ReactDOM.render(myElement, document.getElementById('example'));
```

React 的 JSX 使用大、小写的约定来区分本地组件的类和 HTML 标签。

`<u>***注意:***</u>`

`<u>***由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。***</u>`

