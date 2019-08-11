title: 前端面试题html相关总结
date: 2016-03-17 15:27:09
tags: 
 - html 
 - 面试题（知识点）总结
---
### HTML 相关问题：

#### 1. doctype(文档类型) 的作用是什么？

（1）<!DOCTYPE>声明位于位于HTML文档中的第一行，处于 `<html>` 标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式（怪异模式）呈现。
（2）标准模式的排版和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作。

#### 2. HTML5 为什么只需要写<!DOCTYPE html>？

 HTML5 不基于 SGML，因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）；
 而HTML4.01基于SGML,所以需要对DTD进行引用，才能告知浏览器文档所使用的文档类型。

#### 3. 浏览器标准模式 (standards mode) 和怪异模式 (quirks mode) 之间的区别是什么？
所谓的标准模式是指，浏览器按W3C标准解析执行代码；怪异模式则是使用浏览器自己的方式解析执行代码，因为不同浏览器解析执行的方式不一样，所以我们称之为怪异模式。浏览器解析时到底使用标准模式还是怪异模式，与你网页中的DTD声明直接相关，DTD声明定义了标准文档的类型（标准模式解析）文档类型，会使浏览器使用相应的方式加载网页并显示，忽略DTD声明,将使网页进入怪异模式(quirks mode)。

#### 3. HTML 和 XHTML 有什么区别？
相较HTML，XHTML有着更严格的语法，
XHTML 元素必须被正确地嵌套。
XHTML 元素必须被关闭。
标签名必须用小写字母。
XHTML 文档必须拥有根元素。
因为xml的解析语法过于苛刻，只要网页中出现一处错误，则浏览器停止解析。违背了网页设计的一个基本原理，即“发送时要保守，接收时要开放。”，于是xhtml2.0项目最终流产，被html5所取代。 

#### 4. 如果页面使用 'application/xhtml+xml' 会有什么问题吗？
要求比较严格，必须有head、body标签且每个元素必须是关闭的。
一些老的浏览器不支持，实际上，任何最新的浏览器都将支持application/xhtml+xml媒体类型。大多数浏览器也接受以application/xml发送的XHTML文档。



#### 5. 如果网页内容需要支持多语言，你会怎么做？
采用统一编码UTF-8方式编码
navigator.language 可以返回用户设置的用户首选语言，然后根据用户首选语言执行js操作
[Google提供的网站翻译器](https://translate.google.com/manager/website/)
或
一个可以用域名跳转，不同的语言版本跳转到不同的域名
另一个可以通过浏览器发送带 accept-language 头部信息的请求请求不同版本的页面文档

#### 6. 在设计和开发多语言网站时，有哪些问题你必须要考虑？
  （1） 应用字符集的选择 
       对提供了多语言版本的网站来说，Unicode字符集应该是最理想的选择。
  （2） 语言书写习惯&导航结构
  （3） 数据库驱动型网站
  （4） 搜索引擎&市场推广

#### 7. data-属性的作用是什么？
data- 属性使 HTML 有了存储数据的能力，它让 HTML 更加灵活，JavaScript 可以通过 dataset 方法访问到 data- 的自定义属性，CSS 中也可以通过 attr 方法来引用 data- 属性的值。

	<div data-author="david" data-time="2011-06-20" data-comment-num="10">...</div>
	var post = document.getElementsByTagName('div')[0];
	post.dataset; // DOMStringMap
	post.dataset.commentNum; // 10

#### 8. 如果把 HTML5 看作做一个开放平台，那它的构建模块有哪些？
`<nav>, <header>,<section>, <footer>` 

#### 9. 请描述 cookies、sessionStorage 和 localStorage 的区别。
cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。
cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递。
sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

存储大小：
    cookie数据大小不能超过4k。
    sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

有期时间：
    localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
    sessionStorage  数据在当前浏览器窗口关闭后自动删除。
    cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭


#### 10. 请解释`<script>、<script async>` 和 `<script defer>` 的区别。
普通脚本加载方式在加载和执行时会阻塞页面的渲染，async 和 defer 方式是用异步的方式加载脚本，不会阻塞页面渲染，它们之间的不同在于何时执行，async 方式是加载后马上执行，defer 方式是加载后等所有 DOM 都渲染好触发 DOMContentLoaded 事件之前执行，所以 async 方式里面的脚本都是乱序执行，defer 方式加载的代码都是按序执行的，按序执行对有依赖的代码非常重要。
若两个属性同在，会忽略defer而遵从async

#### 11. 为什么通常推荐将 CSS `<link>` 放置在 `<head></head>` 之间，而将 JS `<script>` 放置在 `</body>` 之前？你知道相关解释吗？
浏览器从上到下依次解析html文档。将 css 文件放到头部， css 文件可以先加载。避免先加载 body 内容，导致页面一开始样式错乱，然后闪烁。将 javascript 文件放到底部是因为：若将 javascript 文件放到 head 里面，就意味着必须等到所有的 javascript 代码都被 下载、解析和执行完成 之后才开始呈现页面内容。这样就会造成呈现页面时出现明显的延迟，窗口一片空白。为避免这样的问题一般将全部 javascript 文件放到 body 元素中页面内容的后面。

#### 12. 什么是渐进式渲染 (progressive rendering)？
渐进式渲染是指浏览器不用等待所有页面资源都渲染好之后再呈现给用户看，而是边下载边渲染，所以用户打开一个网页的时候往往不能第一时间看到所有的内容，但是能够看到一个大概的样子，后续的内容浏览器会慢慢补上形成一个完整的页面。这个有点像 bigpipe。

#### 13. 你用过哪些不同的 HTML 模板引擎？
这个有很多，各大前端框架组件基本都可以叫模版引擎，自己用过什么说说什么。
比喻jQuery，Backbone，Anguar, React，bootstarp等等。

#### 14. 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？
首先：CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”，则为“块级”元素；span默认display属性值为“inline”，是“行内”元素。
（1）行内元素有：a b span img input select strong（强调的语气）
（2）块级元素有：div ul ol li dl dt dd h1 h2 h3 h4…p
（3）常见的空元素：
    `<br> <hr> <img> <input> <link> <meta>`
    鲜为人知的是：
    `<area> <base> <col> <command> <embed> <keygen> <param> <source> <track> <wbr>`
#### 15. 页面导入样式时，使用link和@import有什么区别？

 (1)link属于XHTML标签，除了加载CSS外，还能用于定义RSS, 定义rel连接属性等作用；而@import是CSS提供的，只能用于加载CSS;
（2）页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;
（3）import是CSS2.1 提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题;

#### 16. 介绍一下你对浏览器内核的理解？
主要分成两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎。
渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。
JS引擎则：解析和执行javascript来实现网页的动态效果。
最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。

#### 17. 常见的浏览器内核有哪些？
Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。[又称MSHTML]
Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
Presto内核：Opera7及以上。      [Opera内核原为：Presto，现为：Blink;]
Webkit内核：Safari,Chrome等。   [ Chrome的：Blink（WebKit的分支）]

#### 18. html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？
* HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
  绘画 canvas;
  用于媒介回放的 video 和 audio 元素;
  本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
  sessionStorage 的数据在浏览器关闭后自动删除;
  语意化更好的内容元素，比如 article、footer、header、nav、section;
  表单控件，calendar、date、time、email、url、search;
  新的技术webworker, websockt, Geolocation;
  移除的元素：
  纯表现的元素：basefont，big，center，font, s，strike，tt，u;
  对可用性产生负面影响的元素：frame，frameset，noframes；
* 支持HTML5新标签：
     IE8/IE7/IE6支持通过document.createElement方法产生的标签，
     可以利用这一特性让这些浏览器支持HTML5新标签，
     浏览器支持新标签后，还需要添加标签默认的样式。

     当然最好的方式是直接使用成熟的框架、比如html5shim;
	     <!--[if lt IE 9]>
	        <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
	     <![endif]-->

* 如何区分HTML5： DOCTYPE声明\新增的结构元素\功能元素

#### 19. 简述一下你对HTML语义化的理解？
用正确的标签做正确的事情。
html语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析;
及时在没有样式CCS情况下也以一种文档格式显示，并且是容易阅读的;
搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO;
使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

#### 20. HTML5的离线储存怎么使用，工作原理能不能解释一下？
在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓存文件。
原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。

如何使用：
1、页面头部像下面一样加入一个manifest的属性；
2、在cache.manifest文件的编写离线存储的资源；

	CACHE MANIFEST
	#v0.11
	CACHE:
	js/app.js
	css/style.css
	NETWORK:
	resourse/logo.png
	FALLBACK:
	/ /offline.html
3、在离线状态时，操作window.applicationCache进行需求实现。

#### 21. 浏览器是怎么对HTML5的离线储存资源进行管理和加载的呢？
在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
离线的情况下，浏览器就直接使用离线存储的资源。

#### 22. iframe有那些缺点？
*iframe会阻塞主页面的Onload事件；
*搜索引擎的检索程序无法解读这种页面，不利于SEO;
*iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
使用iframe之前需要考虑这两个缺点。如果需要使用iframe，最好是通过javascript
动态给iframe添加src属性值，这样可以绕开以上两个问题。

#### 23. Label的作用是什么？是怎么用的？
label标签来定义表单控制间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

	<label for="Name">Number:</label>
	<input type=“text“name="Name" id="Name"/>

	<label>Date:<input type="text" name="B"/></label>

#### 24. HTML5的form如何关闭自动完成功能？
给不想要提示的 form 或下某个input 设置为 autocomplete=off。

#### 25. 如何实现浏览器内多个标签页之间的通信? (阿里)
调用localstorge、cookies等本地存储方式

#### 26. webSocket如何兼容低浏览器？(阿里)
Adobe Flash Socket 、
ActiveX HTMLFile (IE) 、
基于 multipart 编码发送 XHR 、
基于长轮询的 XHR

#### 27. 页面可见性（Page Visibility）API 可以有哪些用途？
在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放；

#### 28. 如何在页面上实现一个圆形的可点击区域？
1、map+area或者svg
2、border-radius
3、纯js实现 需要求一个点在不在圆上简单算法、获取鼠标坐标等等

#### 29. 实现不使用 border 画出1px高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果。

	<div style="height:1px;overflow:hidden;background:#ccc"></div>

#### 30. 网页验证码是干嘛的，是为了解决什么安全问题。
区分用户是计算机还是人的公共全自动程序。可以防止：恶意破解密码、刷票、论坛灌水；
有效防止黑客对某一个特定注册用户用特定程序暴力破解方式进行不断的登陆尝试；

#### 31. mate标签都有哪些属性，作用是什么

#### 32. 模板引擎的实现原理是什么

https://www.jianshu.com/p/9091e8a343e4
https://blog.csdn.net/qq_41047322/article/details/82935877








