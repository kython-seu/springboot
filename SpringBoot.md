# 起航

# 2 URL

## 2.1@Controller

标注的类表示是一个处理HTTP请求的控制器(即MVC中的C)，该类中所有被`@RequestMapping`标注的方法都会用来处理对应URL的请求。

## 2.2@ResponseBody`

标注表示处理函数直接将函数的返回值传回到浏览器端显示

@RequestMapping标注类

```java
package com.kason.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

/**
 * Created by IBM on 2016/12/18.
 */
@Controller
@RequestMapping("/myblog")
public class AppController {
    @RequestMapping("/create")
    @ResponseBody
    public String create(){
        return "create blog";
    }
}

```

create()绑定的URL是/myblog/create

每一个类中都可以包含一个或多个`@RequestMapping`标注的方法，通常我们会将业务逻辑相近的URL（例如上例中的文章列表、创建文章）放在同一个Controller中进行处理。

## 2.3@RequestMapping的简写形式

在Web应用中常用的HTTP方法有四种：

- PUT方法用来添加的资源
- GET方法用来获取已有的资源
- POST方法用来对资源进行状态转换
- DELETE方法用来删除已有的资源

这四个方法可以对应到CRUD操作（Create(PUT)、Read(GET)、Update(POST)和Delete(DELETE)），比如博客的创建操作，按照REST风格设计URL就应该使用PUT方法，读取博客使用GET方法，更新博客使用POST方法，删除博客使用DELETE方法。

每一个Web请求都是属于其中一种，在Spring MVC中如果不特殊指定的话，默认是GET请求。

比如`@RequestMapping("/")`和`@RequestMapping("/hello")`和对应的Web请求是：

- **GET** `/`
- **GET** `/hello`

实际上`@RequestMapping("/")`是`@RequestMapping("/", method = RequestMethod.GET)`的简写，即可以通过`method`属性，设置请求的HTTP方法。

比如**PUT** `/hello`请求，对应于`@RequestMapping("/hello", method = RequestMethod.PUT)`

Spring MVC最新的版本中提供了一种更加简洁的配置HTTP方法的方式，增加了四个标注：

- `@PutMapping`
- `@GetMapping`
- `@PostMapping`
- `@DeleteMapping`

基于新的标注`@RequestMapping("/hello", method = RequestMethod.PUT)`可以简写为`@PutMapping("/hello")`。`@RequestMapping("/hello")`与`GetMapping("/hello")`等价。

## 2.4HTML Response

上面都是返回的String，下面开始返回HTML页面



在之前所有的Controller方法中，返回值字符串都被直接传送到浏览器端并显示给用户。但是为了能够呈现更加丰富、美观的页面，我们需要将HTML代码返回给浏览器，浏览器再进行页面的渲染、显示。 一种很直观的方法是在处理请求的方法中，直接返回HTML代码：

```java
@GetMapping("/blog")
public String blog() {
    return "<html><head><title>Title</title></head><body><h2>This is a blog</h2><p>This is content of the blog.</p></body></html>";
}
```

显然，这样做的问题在于——一个复杂的页面HTML代码往往也非常复杂，并且嵌入在Java代码中十分不利于维护。

更好的做法是将页面的HTML代码写在模板文件中，然后读取该文件并返回。Spring天然支持这种非常常见的场景，需要先在`pom.xml`引入Thymeleaf依赖（接下来的学习中会重点讲到）：

```java
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

将HTML文本保存在src/main/resources/templates/blog.html下：

```html
<html>
  <head>
    <title>Title</title>
  </head>
  <body>
    <h1>This is title</h1>
    <p> This is Content</h2>
  </body>
</html>
```

`Controller`中可以去掉`@ResponseBody`标注(表示不是直接返回字符串，而是返回渲染的HTML模板)，并将URL处理函数的返回值设为刚刚保存在`templates/`文件夹中的文件名（不需要扩展名）：

```java
@GetMapping("/blogs")
public String blog() {
    return "blog";
}
```

Spring框架在发现返回值是`"blog"`后，就会去`src/main/resources/templates/`目录下读取`blog.html`文件并将它的内容返回给浏览器。

```
在编写HTML代码时，请务必保证每一个标签都是闭合的，容易忽略的标签包括<meta/>, <link/>, <br/>, <hr/>, <img/>, <input/>等等。

但是在HTML5中，有些标签并不要求闭合，Thymeleaf遇到这样的HTML文件会报错。为了支持HTML5，你可以在Spring Boot的配置文件中增加一行配置：

spring.thymeleaf.mode=LEGACYHTML5
Spring Boot的配置文件通常在/resources根目录下，以application.properties命名，没有这个这个文件则创建一个。
```

另外为了保证Thymeleaf能够正确的识别HTML5，还需要添加Maven依赖：

```java
<dependency>
  <groupId>net.sourceforge.nekohtml</groupId>
  <artifactId>nekohtml</artifactId>
  <version>1.9.22</version>
</dependency>
```

## 2.5静态资源CSS JS IMAGE处理

### 2.5.1外部资源文件

在编写HTML代码的过程中，我们会遇到几类外部静态资源：

- CSS文件：``
- JavaScript文件：``
- 图像：``

这些外部资源都是通过HTTP协议访问得到——也就是说，当我们用浏览器打开我们编写的HTML页面（无论是通过本地文件直接打开，还是访问Spring Boot服务器），在获取页面内容本身之外，还需要向外部服务器（例如`maxcdn.bootstrapcdn.com`）发起HTTP请求以获取我们需要的CSS/JavaScript资源。

但是在我们开发过程中，如果某个时刻不能访问Internet，那我们的页面也就无法正确的展现出它应有的样式。另一方面，除了使用第三方库，我们自己还会编写大量的CSS/JavaScript文件，这就要求我们必须有一种很快的方式能够在修改之后立马在本地看到结果。

### 2.5.2本地资源文件组织

首先我们抛开本地HTTP服务器，简单来看在本地编写一个HTML文件以及使用CSS资源，那么我们可以这样组织项目结构：

```javascript
.
├── index.html
├── css
    └── style.css
└── js
    └── main.js
```

在`index.html`文件中可以这样引用它们：

```html
<link rel="stylesheet" href="css/style.css"/>
<script src="js/main.js"></script>
```

`css/style.css`和`js/main.js`都是使用相对路径描述，当我们在浏览器中打开`index.html`，URL应该类似`file:///Users/tianmaying/app/index.html`，此时当浏览器解释到上述引用外部资源的代码，会以当前访问的URL为基准，根据相对路径计算出完整的HTTP请求地址：

```html
Base: file:///Users/tianmaying/app/index.html
CSS: file:///Users/tianmaying/app/css/style.css
JavaScript: file:///Users/tianmaying/app/js/main.js
```

### 2.5.3服务器中的静态资源文件

如果我们需要讲`index.html`放在服务器中呢？`index.html`位于`templates`目录下，通过`http://localhost:8080/`可以访问首页内容，但是CSS和JavaScript外部资源呢？因为我们的HTTP服务器根本没有处理它们，所以不可能通过类似`http://localhost:8080/css/style.css`这样的方式来访问它们使得我们的页面正确显示。

默认情况下，Spring Boot会将类路径上的`/static/`目录的内容Serve起来，意思就是对静态资源的请求，都会返回`/static/`目录中对应路径的文件内容，于是我们可以这样组织文件目录结构来处理静态资源（以下是`src/main/resources`目录结构，这个目录经过编译后会被添加到类路径上）：

```
.
├── static
    ├── css
        └── style.css
    └── js
        └── main.js
└── templates
    └── index.html
```

这样，当我们经过以上布局，重启应用后，就可以通过访问`http://localhost:8080/css/style.css`和`http://localhost:8080/js/main.js`来获取CSS和JavaScript资源了。

### 2.5.4在HTML中引入资源

最后我们将静态资源引入到HTML页面中，我们往往需要一种介于相对路径(如`css/style.css`)和绝对路径(如`http://assets0.tianmaying.com/img/appicon/ios.png`)之间的资源访问方式——*<u>**Context**路径</u>*：

```html
<link rel="stylesheet" href="/css/style.css"/>
<script src="/js/main.js"></script>
```

***<u>这里只是简单的在相对路径URL的最前面加上了`/`（`/css/style.css`），但是意义和相对路径就完全不同了，此时服务器会将其视为访问当前host中的“绝对路径”——也就是自动在这个路径之前添加上协议、主机名和端口（都是当前服务器的相同信息），那么无论我们访问的是当前网站下的任何路径，它都会给出统一的结果，从而正确引用到外部资源，即`http://localhost:8080/css/style.css`。***

***</u>***

为了能够正确解析html5文件：需要加入一下依赖

```java
<dependency>
  <groupId>net.sourceforge.nekohtml</groupId>
  <artifactId>nekohtml</artifactId>
  <version>1.9.22</version>
</dependency>
```

## 2.6本章总结

- `@Controller`、`@RequestMapping`及其简写方式(`@PUTMapping`、`@GETTMapping`、`@blogMapping`和`@DELETEMapping`)的用法
- 如何通过模板文件返回HTML
- 理解相对路径、绝对路径和Context Relative路径以及它们的使用时机，参考[Spring Boot处理静态资源](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-spring-mvc-static-content)



# 3@PathVariable

## 3.1 URL变量

在上一课中我们学习了如何在`@Controller`中创建`@RequestMapping`（或者相应的简写）来处理不同的URL请求。但是在Web应用中URL通常不是一成不变的，例如微博两个不同用户的个人主页对应两个不同的URL: `http://weibo.com/user1`，`http://weibo.com/user2`。我们不可能对于每一个用户都编写一个被`@RequestMapping`注解的方法来处理其请求，也就是说，对于相同模式的URL（例如不同的用户的主页，它们仅仅是URL中的某一部分不同，为它们各自的用户名，我们说它们具有相同的模式）。

## 3.2 定义URL变量规则

我们可以在`@RequestMapping`注解里用`{}`来表明它的变量部分，例如:

```java
@GetMapping("/users/{username}")
```

***<u>这里`{username}`就是我们定义的变量规则，`username`是变量的名字</u>***。那么这个URL路由可以匹配下列任意URL并进行处理：

- `/users/tianmaying`
- `/users/ricky`
- `/users/tmy1234`

> 需要注意的是，在默认情况下，变量中不可以包含URL的分隔符`/`（Slash），例如上述路由不能匹配`/users/tianmaying/ricky`，即使你认为`tianmaying/ricky`是一个存在的用户名

## 3.3 获取URL变量值

在路由中定义变量规则后，通常我们需要在处理方法（也就是`@RequestMapping`注解的方法）中获取这个URL变量的具体值，并根据这个值（例如用户名）做相应的操作，Spring MVC提供的`@PathVariable`可以帮助我们：

```java
@GetMapping("/users/{username}")
public String userProfile(@PathVariable String username) {
    return String.format("user %s", username);
}
```



在上述例子中，当`@Controller`处理HTTP请求时，`userProfile`的参数`username`会被自动设置为URL中的对应变量`username`***<u>~~（同名赋值）~~</u>***的值***~~(注意一定要同一个名字，如果不是同一个名字需要使用下面的方法@PathVariable{"username"} String xxx)~~***，例如当HTTP请求为：`/users/tianmaying`，URL变量`username`的值`tianmaying`会被赋给函数参数`username`，函数的返回值自然也就是：`String.format("user %s", username);`，即`user tianmaying`。

在默认情况下，Spring会对`@PathVariable`注解的变量进行自动赋值，当然你也可以指定`@PathVariable`使用哪一个URL中的变量：

```java
@GetMapping("/users/{username}")
public String userProfile(@PathVariable("username") String user) {
    return String.format("user %s", user);
}
```

这时，由于注解`String user`的`@PathVariable`的参数值为`username`，所以仍然会将URL变量`username`的值赋给变量`user`

## 3.4 定义多个URL变量

可以定义URL路由，其中包含多个URL变量：

```java
@GetMapping("/users/{username}/blogs/{blogId}")
public String getUserBlog(@PathVariable String username, @PathVariable int blogId) {
    //具体实现，略
}
```

这种情况下，Spring能够根据名字自动赋值对应的函数参数值，当然也可以在`@PathVariable`中显式地表明具体的URL变量值。

在默认情况下，`@PathVariable`注解的参数可以是一些基本的简单类型：`int`，`long`，`Date`，`String`等，Spring能够根据URL变量的具体值以及函数参数的类型来进行转换，例如`/users/tianmaying/blogs/12`，会将`tianmaying`赋值给String变量`username`，而`12`赋值给`int`变量`blogId`

## 3.5 总结

- 在`@RequestMapping`注解中定义URL变量规则
- 在`@RequestMapping`注解的方法中获取URL变量——`@PathVariable`
- `@PathVariable`指定URL变量名
- 定义多个URL变量
- 用正则表达式精确定义URL变量

# 4 @RequestParam

## 4.1 Request参数

我们在访问各种各样的网站时，经常会发现网站的URL的最后一部分形如：`?xxxx=yyyy&zzzz=wwww`。这就是HTTP协议中的Request参数，它有什么用呢？我们先来看一个例子：

- 在知乎中搜索`web`
- 浏览器跳转到新页面后，URL变为`https://www.zhihu.com/search?type=content&q=web`

这里`type=content&q=web`就是搜索请求的参数，不同的参数之间用`&`分隔，每个参数形如`name=value`形式，分别表示参数名字和参数值。在这个例子中，我们输入不同的搜索关键词，在搜索结果页面的URL的`q`参数是不同的，也就是说，***<u>HTTP参数实际上可以认为是一种用户的输入，根据不同的用户输入，服务器经过处理后返回不同的输出</u>***（例如我搜索`奥运会`和搜索`世界杯`，显示的结果是不一样的）。

## 4.2 Spring MVC中的Request参数

在Spring MVC框架中，现在我们已经可以通过定义@RequestMapping来处理URL请求了，和@PathVariable一样，我们也需要在处理URL的函数中获取URL中的参数——也就是?key1=value1&key2=value2这样的参数列表。通过注解@RequestParam可以轻松的将URL中的参数绑定到处理函数方法的变量中：

```java
@GetMapping("/myblogs")
    @ResponseBody
    public String blog(@RequestParam("id") int blogid){
        return String.format("blog id = %d",blogid);
    }
```

这样当我们访问`/blogs?id=1`时，Spring MVC帮助我们将Request参数`id`的值绑定到了处理函数的参数`blogId`上。这样我们就能够轻松获取用户输入，并且根据它的值进行计算并返回了。

## 4.3 @RequestParam VS @PathVariable

@RequestParamv.s @PathVariable

相信大家可能注意到了，`@RequestParam`和`@PathVariable`都能够完成类似的功能——因为本质上，他们都是用户的输入，只不过输入的部分不同，一个在URL路径部分，另一个在参数部分。我们要访问一篇博客文章，这两种URL设计都是可以的：

- 通过`@PathVariable`，例如`/blogs/1`
- 通过`@RequestParam`，例如`blogs?blogId=1`

那么究竟应该如何选择呢？我们建议：

1. 当URL指向的是某一具体业务资源（或者资源列表），例如博客、用户时，使用`@PathVariable`
2. 当URL需要对资源或者资源列表进行过滤、筛选时，用`@RequestParam`

例如我们会这样设计URL：

- `/blogs/{blogId}`
- `/blogs?state=publish`而不是`/blogs/state/publish`来表示处于发布状态的博客文章

更多用法



一旦我们在方法中定义了`@RequestParam`变量，如果访问的URL中不带有相应参数，就会抛出异常——这是显然的，Spring尝试帮我们进行绑定，然而没有成功。但是有的时候，参数确实不一定永远都存在，这时我们可以通过定义`required`属性：

```java
@RequestParam(name="id", required=false)//在默认情况下，required=true
```

当然，在参数不存在的情况下，我们可能希望变量有一个默认值：

```java
@RequestParam(name="id", required=false, defaultValue="0")
```

## 4.4 分页

随着时间的流逝，我们的博客文章可能越来越多，博客列表页面如果一下显示几百甚至数千篇文章，首先是不方便查找，其次返回的文章过多也影响网页的加载效率。所以，对文章列表进行分页是非常有必要的，假设现在我们每页显示10篇文章，如果一共1000篇文章，那么就可以被分成100页。

访问`/blogs`时，我们需要通过告知服务器，我们需要第几页的文章，这里正是`@RequestParam`发挥用武之地的地方：

```
http://localhost:8080/blogs?page=1
```

相比于`/blogs/pages/1`，明显上面这个URl更加优雅、易懂。这时我们的处理函数可以这样定义：

```java
private static final int PAGE_SIZE = 10;

@GetMapping("/blogs")
//如果URL没有带page参数，我们默认显示第一页
public List<Blog> blogs(@RequestParam(name="page", required=false, defaultValue="1") int page) {
    int start = (page - 1) * PAGE_SIZE;//找到起始点
    List<blog> blogs = blogService.findBlogs().subList(start, start + PAGE_SIZE);
  
    return blogs;
}
```

当然我们完全也可以把每一页的大小`size`也作为参数放在URL中。

## 4.5 回顾

- URL中的参数格式
- 使用`@RequestParam`绑定URL参数
- `@RequestParam`和`@PathVariable`的选择
- `@RequestParam`的其他属性——是否必须，默认参数值



# 5 新篇章

http://www.jianshu.com/p/b72242828ec1

https://github.com/zsl131/thymeleaf-study

https://github.com/zsl131/school-blog

## 5.1 配置数据库

maven 配置：

pom.xml配置依赖

引入jdbc支持

<dependency>

    <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

配置生产数据库mysql

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.21</version>
</dependency

```

然后在application.properties中配置数据库连接信息。

```
spring.datasource.url=jdbc:mysql://localhost:3306/blog
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

使用JdbcTemplate操作数据库

Spring的JdbcTemplate是自动配置的，你可以直接使用`@Autowired`来注入到你自己的bean(比如User bean)中来使用。

