# 13.2 LESS使用 

### 1.下载安装

#### 服务器(客户端)安装
在服务器上安装Less的最简单方法是通过node.js包管理器npm ，如下所示：
```
$ npm install -g less
```
安装完成后，您可以从命令行调用编译器，如下所示：
```
$ lessc styles.less
```
这将输出编译的CSS stdout。要将CSS结果保存到您选择的文件，请使用：
```
$ lessc styles.less styles.css
```
要对css进行压缩，可以使用CSS [clean-css插件](https://github.com/less/less-plugin-clean-css)。当插件安装完成后，使用如下命令进行压缩：
```
$ lessc --clean-css styles.less styles.min.css
```
要查看所有命令行选项，请运行lessc不带参数或查看[用法](http://lesscss.cn/usage/index.html)

#### 浏览器(Web端)使用
客户端是最简单的入门方式，适合Less开发，但在生产中，当性能和可靠性很重要时，官方建议使用node.js或许多第三方工具之一进行预编译。

首先，将.less样式表与rel设置为“ stylesheet/less” 的属性相关联：
```
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```
接下来，下载[less.js](https://codeload.github.com/less/less.js/zip/master)并将其插入<script></script>：
```
<script src="less.js" type="text/javascript"></script>
```
示例：
```
<style type="text/less">
	.demo{
		position: absolute;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		margin: auto;
	}
	#wrap{
		.demo;
		width: 400px;
		height: 400px;
		border: 1px solid;
		#inner{
			.demo;
			width: 200px;
			height: 200px;
			background: pink;
		}
	}
	
</style>
<script src="less/less.js"></script>
```
也可以引用 CDN 的地址： 
```
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.5.3/less.min.js"></script>
```
### 2.编译工具

**koala**是一个前端预处理器语言图形编译工具，支持Less、Sass、Compass、CoffeeScript，帮助web开发者更高效地使用它们进行开发。跨平台运行，完美兼容windows、linux、mac。在实际工作应用中，koala是我们经常使用的less编译工具，它具有客户端，操作更简单，而且还能够实时编译

官网：http://koala-app.com/index-zh.html

![](https://i.imgur.com/7U9X6HB.png)

**下载安装**

**Windows**：https://github.com/oklai/koala/releases/download/v2.3.0/KoalaSetup.exe
**macOs**：https://github.com/oklai/koala/releases/download/v2.3.0/Koala.dmg


**使用koala**

将less文件所在的目录拖到软件工作窗口，选择需要编译的less文件即可。当改动less文件里的代码，就会自动生成同名的css文件，速度非常快。

![](https://i.imgur.com/p1fFchd.png)

### 3.语言特性

#### 变量(Variables)
在Less中可以定义变量，在对元素进行样式定义时可以引用。

示例：
```
@xbsj:greenyellow; //注意后面一定要加“;”不然使用koala编译会报错
@w:200px;
@h:200px;
#demo{
    width: @w;
    height: @h;
    background-color: @xbsj;
}

```
编译生成css
```
#demo {
  width: 200px;
  height: 200px;
  background-color: #adff2f;
}
```
html结构
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" href="css/index.css" />
	</head>
	<body>
		<div id="demo"></div>
	</body>
</html>
```
#### 嵌套(Nesting)
Less 能够使用嵌套完成子元素的样式定义。可以在一个css里有多个css块，以方便我们更好的组织代码，编写css模板。

我们此时有以下css代码：
```
#list {
  list-style: none;
}
#list li a {
  font-size: 30px;
  text-decoration: none;
}
#list li a:hover {
  font-size: 40px;
  color: pink;
}

```
使用Less我们也可以写成这样：
```
#list{
	list-style: none;
	li{
	    a{
	        font-size: 30px;
	        text-decoration: none;
	        &:hover{
	            font-size: 40px;
	            color: pink;
	        }
	    };
	}
}
```


其中还支持 "**&**" 符号：
```
#header {
  color: black;
  &-navigation {
    font-size: 12px;
  }
  &-logo {
    width: 300px;
  }
  &:hover{
    color:#ccc;
  }
}
```
编译生成css
```
#header {
  color: black;
}
#header-navigation {
  font-size: 12px;
}
#header-logo {
  width: 300px;
}
#header:hover {
  color: #ccc;
}
```

#### 混合（Mixins）
混合是一种将一组属性从一个规则集合放入另一个规则集合使用（“混入”）的方式。简单说就是前面定义的一个样式，后文可以直接引用。

示例：
```
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}

#menu a {
  color: #111;
  .bordered; //引用.bordered
}

.post a {
  color: red;
  .bordered;
}
```
编译生成css
```
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
#menu a {
  color: #111;
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
.post a {
  color: red;
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
```

**带参数的混合**
```
.xbsj(@w:300px,@h:300px){
    width: @w;
    height: @h;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
}



#wrap{
    .xbsj(@h:400px);
    border: 1px solid;
    #inner{
        .xbsj(200px,200px);
        background: pink;
    }
}
```
编译生成css
```
#wrap {
  width: 300px;
  height: 400px;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  border: 1px solid;
}
#wrap #inner {
  width: 200px;
  height: 200px;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  background: pink;
}
```
html结构
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/index.css"/>
	</head>
	<body>
		<div id="wrap" >
			<div id="inner" >
				inner
			</div>
		</div>
	</body>
</html>
```
#### 运算（Operations）
在Less中支持算术运算+，-，*，/，并且任何数字、颜色或者变量都可以参与运算。

**颜色运算**
示例：
```
@nice-blue: #5B83AD;
@light-blue: @nice-blue + #111;

#header {
  color: @light-blue;
}
```
编译生成css
```
#header {
  color: #6c94be;
}
```
*[更多颜色操作](https://less.bootcss.com/functions/#color-operations)*

**数字运算**
纯数字的运算意义并不是很大

示例：
```
@incompatible-units: 2 + 5 - 3;

#xbsj{
    width: (@incompatible-units)px;
}
```
编译生成css
```
#xbsj {
  width: 4 px;
}
```
**单位运算**
在单位运算中，获得运算结果的单位为最左边明确指出单位类型

示例：
```
@incompatible-units: 2 + 5px - 3cm; // result is 4px 获得值单位为“px”
@incompatible-units: 2 + 5cm - 3px; // result is 4cm 获得值单位为“cm”
```

**calc() 特例**
为了与 CSS 保持兼容，Less中calc() 并不对数学表达式进行计算，但是在嵌套函数中会计算变量和数学公式的值。

示例：
```
@var: 50vh/2;

#xbsj{
    width: calc(50% + (@var - 20px)); 
}
```
编译生成css
```
#xbsj {
  width: calc(55%);
}
```
#### 函数（Functions）
Less 内置了多种函数用于转换颜色、处理字符串、算术运算等。这些函数在函数手册中有详细介绍。

函数的用法非常简单。下面这个例子将介绍如何将 0.5 转换为 50%，将颜色饱和度增加 5%，以及颜色亮度降低 25% 并且色相值增加 8 等用法：
```
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```
编译生成css
```
.class {
  width: 50%;
  color: #f6430f;
  background-color: #f8b38d;
}
```
*[更多参见：函数手册](https://less.bootcss.com/functions/)*

#### 命名空间
有时候，我们为了更好组织 CSS 或者单纯是为了更好的封装，将一些变量或者混合模块打包起来，一些属性集之后可以重复使用。

Less 中的命名空间，属于高级语法，在日常项目中应用比较广泛。我们可以用 Less 中的命名空间为自己封装一些日常比较常用的类名，以便以后做项目的时候更有效率。

示例：
```
/*模块*/
#bundle {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white
    }
  }
  .tab { /**/ }
  .citation { /**/ }
}

/*下面复用上面的一部分代码*/
#header a {
  color: orange;
  #bundle > .button;
}
```
编译生成css
```
/*模块*/
#bundle .button {
  display: block;
  border: 1px solid black;
  background-color: grey;
}
#bundle .button:hover {
  background-color: #ffffff;
}
#bundle .tab {
  /**/
}
#bundle .citation {
  /**/
}
/*下面复用上面的一部分代码*/
#header a {
  color: orange;
  display: block;
  border: 1px solid black;
  background-color: grey;
}
#header a:hover {
  background-color: #ffffff;
}
```
#### 作用域（Scope）
Less中的范围与编程语言非常相似。变量和mixin首先在本地查找，如果找不到，编译器将查找父范围，依此类推。简单来说就是，子类里面的优先，找不到才往父类里找。

示例：
```
@var: red;

#page {
  @var: white;
  #header {
    color: @var; // 这里值是white
  }
}
```
也不会因为变量在后面定义而影响作用域：
```
@var: red;

#page {
  #header {
    color: @var; // 这里的值是white
  }
  @var: white;
}
```

#### 注释（Comments）
在css中仅支持块注释，Less中块注释和行注释都可以使用
```
/* 一个块注释
 * style comment! */
@var: red;

// 这一行被注释掉了！
@var: white;
```

#### 导入（Importing）
像css一样，我们也可以导入一个 .less 文件，此文件中的所有变量我们可以全部使用。如果导入的文件是 .less 扩展名，则可以将扩展名省略掉
```
@import "library"; // library.less
@import "typo.css";
```

#### 其他（other）
**避免编译**
避免编译顾名思义就是在编译时保持原有代码，例如我们在使用calc运算时，如果想不想对其进行编译，可以在前面加“~”符号

示例：
```
.box{
    width: ~"calc(800px + 800px)";
}

.box{
    width: "calc(800px + 800px)";
}

```
编译生成css
```
.box {
  width: calc(800px + 800px);
}
.box {
  width: "calc(800px + 800px)";
}

```

**继承**
使用“&:extend”

示例：
```
.xbsj:hover{
    background: yellow;
}
.xbsj{
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
}

#wrap{
    &:extend(.xbsj all);
    width: 400px;
    height: 400px;
    background: pink;
    .inner{
          &:extend(.xbsj);
          width: 200px;
          height: 200px;
          background: gray;
    }
}
```
编译生成css
```
.xbsj:hover,
#wrap:hover {
  background: yellow;
}
.xbsj,
#wrap,
#wrap .inner {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
}
#wrap {
  width: 400px;
  height: 400px;
  background: pink;
}
#wrap .inner {
  width: 200px;
  height: 200px;
  background: gray;
}
```
**循环**
循环生成相应样式

示例：
```
.box(@n) when (@n >= 1){
    .box(@n - 1);
    width: @n * 10px;
}

.test{
    .box(12);
}
```
编译生成css
```
.test {
  width: 10px;
  width: 20px;
  width: 30px;
  width: 40px;
  width: 50px;
  width: 60px;
  width: 70px;
  width: 80px;
  width: 90px;
  width: 100px;
  width: 110px;
  width: 120px;
}
```