# JavaScript 的诞生

## 始于对浏览器功能的革新

1993年美国 **国家超级电脑应用中心**（NCSA）发表了NCSA
Mosaic，这是最早流行的图形接口网页浏览器，它在万维网的普及上发挥了重要作用。随后1994年，Mosaic的主要开发人员创立了网景（Netescape）公司，并开发了Netscape Navigator浏览器。Netscape
Navigator一经推出，在四个月内抢占了四分之三的浏览器市场，成为90年代互联网的主要浏览器。但在当时，Navigator浏览器只能用来浏览网页，并不具备用户也网页的互动能力。网景公司也预见到了网络需要变得更加动态，所以公司急需一种胶水语言、一种网页脚本语言，来让浏览器可以和网页互动。

## 创造者——布兰登·艾克

布兰登·艾克（Brendan Eich），1995年4月被网景公司招募，最初目标是把Scheme语言嵌入到Netscape Navigator浏览器当中作为网页脚本语言。  
但在这之前，一个名为昇阳的公司推出了一门语言Java。昇阳大肆宣传，许诺这种语言可以“ 一次编写，到处运行”（Write Once, Run
Anywhere）。网景被宣传打动，和昇阳公司组成了开发联盟，决定在Navigator浏览中支持Java。所以为了蹭上Java的“热度”，最初的目标被改变了，网景决定未来的网页脚本语言必须“看上去与Java足够相似”
，但是比Java简单，使得非专业的网页作者也能很快上手。  
布兰登进入公司是为了研究如何将Scheme语言作为网页脚本语言的可能性，现在脚本语言必须重新设计，并且与Java相似，对Java一点兴趣也没有的他在1995年5月仅仅花了10天就把JavaScript设计出来了。

### 命名的由来

瓜哇岛（Java Island）是印度尼西亚的岛屿，它的**瓜哇咖啡**（Java coffee）非常有名，Java语言的名字便是从此汲取了灵感。JavaScript的语言最初命名也是咖啡，名为**摩卡（Mocha）**
，1995年9月在Netscape Navigator 2.0的Beta版中改名为 **LiveScript**，同年12月，Netscape Navigator 2.0 Beta 3中部署时被重命名为**JavaScript**。  
当时网景公司与昇阳电脑公司组成的开发联盟为了让这门语言搭上Java这个编程语言“热词”，因此将其临时改名为JavaScript，日后这成为大众对这门语言有诸多误解的原因之一。

# JavaScript 的发展

## 微软的IE

微软（Microsoft）在1995年首次推出了 Internet Explorer（IE浏览器），开始了与Netscape的浏览器大战。微软通过对Netscape Navigator的解释器进行逆向工程，创建了**JScript**
（JScript也是一种JavaScript实现）。除此之外，微软也在网页技术上加入了不少专属对象，使不少网页使用非微软平台及浏览器无法正常显示，这使得浏览器大战期间用户经常只能在特定浏览器上浏览目标网页。

## 标准化

为了反制微软，1996年11月，网景正式向ECMA（欧洲计算机制造商协会）提交语言标准。

- 1997年6月，ECMA以JavaScript语言为基础制定了ECMAScript标准规范ECMA-262。
- **1999年12月，ECMAScript 3.0版发布，成为JavaScript的通行标准，得到了广泛支持。**
- **2015年6月，ECMAScript 2015（ES2015），第 6 版，最早被称作是 ECMAScript 6（ES6）。**

### ECMAScript与JavaScript的关系

ECMAScript实际上是一种脚本在语法和语义上的标准。而JavaScript是ECMAScript的一种实现。

- JavaScript的标准只有一种，就是ECMAScript。
- ECMAScript实现可以有很多种，比如chromeV8引擎也是ECMAScript的一种实现。

## JavaScript的设计缺陷

当时布兰登设计JavaScript的思路：

1. 借鉴C语言的基本语法；
2. 借鉴Java语言的数据类型和内存管理；
3. 借鉴Scheme语言，将函数提升到"第一等公民"（first class）的地位；
4. 借鉴Self语言，使用基于原型（prototype）的继承机制。

所以，JavaScript语言实际上是两种语言风格的混合产物——（简化的）函数式编程 + （简化的）面向对象编程。

### 纵观全局，有三个客观原因导致JavaScript设计不够完善：

**1. 设计阶段过于仓促**  
Javascript的设计，只用了十天，并且当时只是为了解决一些简单的网页互动，并没有考虑复杂应用的需要。

**2. 没有先例**  
Javascript同时结合了函数式编程和面向对象编程的特点，而且直到今天为止，Javascript仍然是世界上唯一使用Prototype继承模型的主要语言。这使得它没有设计先例可以参考。

**3.过早的标准化**  
Javascript才推出一年半之后，为了反制微软就被早早标准化，设计缺陷没有得到足够长时间的暴露。相比之下，C语言问世将近20年之后，国际标准才颁布。

### [Javascript的10个设计缺陷](http://www.ruanyifeng.com/blog/2011/06/10_design_defects_in_javascript.html)
