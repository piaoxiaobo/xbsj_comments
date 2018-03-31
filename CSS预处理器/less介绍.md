# 13.1 LESS介绍 

### LESS是什么？
**中文译文**
```
less
英 [les]  美 [lɛs]

adv. 较少地；较小地；更小地
adj. 较少的；较小的
prep. 减去
n. 较少；较小
```

**预处理器**

**Less** 是一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展。

Less 可以运行在 Node 或浏览器端。

示例：
```
@base: #f938ab;

.box-shadow(@style, @c) when (iscolor(@c)) {
  -webkit-box-shadow: @style @c;
  box-shadow:         @style @c;
}
.box-shadow(@style, @alpha: 50%) when (isnumber(@alpha)) {
  .box-shadow(@style, rgba(0, 0, 0, @alpha));
}
.box {
  color: saturate(@base, 5%);
  border-color: lighten(@base, 30%);
  div { .box-shadow(0 0 5px, 30%) }
}
```
输出：
```
.box {
  color: #fe33ac;
  border-color: #fdcdea;
}
.box div {
  -webkit-box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
}
```

### LESS相关网站
[Less中文网](http://lesscss.cn/)
[Less官网](http://lesscss.org/)
[快速入门丨less.js](https://less.bootcss.com/)
[Less百度百科](https://baike.baidu.com/item/less/17570158?fr=aladdin)

### LESS历史
LESS由Alexis Sellier于2009年设计。LESS是一个开源。LESS的第一个版本是用Ruby编写的，在后来的版本中，它被JavaScript代替

### LESS和CSS

**CSS（层叠样式表）**是一门历史悠久的标记性语言，同 HTML 一道，被广泛应用于**万维网（World Wide Web）**中。HTML 主要负责文档结构的定义，CSS 则负责文档表现形式或样式的定义。

作为一门标记性语言，CSS 的语法相对简单，对使用者的要求较低，但同时也带来一些问题：CSS 需要书写大量看似没有逻辑的代码，不方便维护及扩展，不利于复用，尤其对于非前端开发工程师来讲，往往会因为缺少 CSS 编写经验而很难写出**<font color='red'>组织良好且易于维护</font>**的 CSS 代码，造成这些困难的很大原因源于 CSS 是一门非程序式语言，没有变量、函数、SCOPE（作用域）等概念。

**LESS** 为 Web 开发者带来了福音，它在 CSS 的语法基础之上，引入了变量，Mixin（混入），运算以及函数等功能，大大简化了 CSS 的编写，并且降低了 CSS 的维护成本，就像它的名称所说的那样，LESS 可以让我们**<font color='red'>用更少的代码做更多的事情。</font>**

### 使用LESS和CSS的争论

**FQA:知乎网友**

建议还是用less这种来写，层叠嵌套的问题是你编写的习惯造成的，你完全可以把页面内容以板块方式切割，每个板块作为最外层嵌套，板块内部的子元素全部不要嵌套就可以了，只要你谨慎使用全局样式的话，也不会发生样式彼此冲突的问题。另外，JS修改样式 无非两种手段，一个是写行内样式，当然这个效率差一点，另一个是调用预写的样式，像这种JS调用的特定样式 你可以写在一个独立的样式表中，然后嵌套一个ID选择器提升优先级【JS操作DOM多会为元素提供一个ID】，这样既方便管理 也不会有其他什么问题了。

作者：小八戒
链接：https://www.zhihu.com/question/40010008/answer/84332773
来源：知乎

**FQA:掘金网友**

作者：泊浮目
Less写好编译一下就成了Css。
如果你自己写过css就会发现css冗余度是比较高的。
less就可以比较方便的解决这些问题。


作者：熊猫桑
原生css和Less都有各自适用的领域，不是简单的一个“好”或者“不好”就能下定论的。不然PHP不就成了世界上最好的语言么……

写一些小东西，比如单个的Demo页面、或者说有速度要求根本没时间做二次的转换，那么直接手写css无疑是明智的；但在大一些的项目里，试试Less和其他这些类似的预处理器（包括后处理器），我觉得也不妨一试，用上以后样式可以有更复杂的表现（比如用上函数）或者体现继承关系，比手打几百行css可能要更加直观可视化，也可以部分降低在编写复杂样式时的出错概率（当然只是部分）。

