title: 前端面试题css相关总结
date: 2016-03-19 13:32:55
tags:
- css
- 面试题（知识点）总结
---
### css相关问题

#### 1. 介绍一下CSS的盒子模型？
（1）有两种， IE 盒子模型、标准 W3C 盒子模型；IE的content部分包含了 border 和 pading;
（2）盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border).

#### 2. CSS选择符有哪些？哪些属性可以继承？
1.id选择器（ # myid）
2.类选择器（.myclassname）
3.标签选择器（div, h1, p）
4.相邻选择器（h1 + p）
5.子选择器（ul > li）
6.后代选择器（li a）
7.通配符选择器（ * ）
8.属性选择器（a[rel = "external"]）
9.伪类选择器（a: hover, li: nth - child）

可继承的样式： font-size font-family color, UL LI DL DD DT;
不可继承的样式：border padding margin width height ;

#### 3. CSS优先级算法如何计算？ 
 优先级就近原则，同权重情况下样式定义最近者为准;

 载入样式以最后载入的定位为准;
优先级为:
   !important >  id > class > tag
    important 比 内联优先级高

#### 4. CSS3新增伪类有那些？
CSS3新增伪类举例：
    p:first-of-type 选择属于其父元素的首个 `<p>` 元素的每个 `<p>` 元素。
    p:last-of-type  选择属于其父元素的最后 `<p>` 元素的每个 `<p>` 元素。
    p:only-of-type  选择属于其父元素唯一的 `<p>` 元素的每个 `<p>` 元素。
    p:only-child    选择属于其父元素的唯一子元素的每个 `<p>` 元素。
    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 `<p>` 元素。
    :enabled        :disabled 控制表单控件的禁用状态。
    :checked        单选框或复选框被选中。

#### 5. 如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？
* 给div设置一个宽度，然后添加margin:0 auto属性
		div{
	    width:200px;
	    margin:0 auto;
	 	}

* 居中一个浮动元素
	确定容器的宽高 宽500 高 300 的层
	  设置层的外边距

	 	.div {
	      width:500px ; height:300px;//高度可以不设
	      margin: -150px 0 0 -250px;
	      position:relative;         //相对定位
	      background-color:pink;     //方便看效果
	      left:50%;
	      top:50%;
	 	}

* 让绝对定位的div居中
	  position: absolute;
	  width: 1200px;
	  background: none;
	  margin: 0 auto;
	  top: 0;
	  left: 0;
	  bottom: 0;
	  right: 0;

#### 6. display有哪些值？说明他们的作用。
  block 象块类型元素一样显示。
  none 缺省值。象行内元素类型一样显示。
  inline-block 象行内元素一样显示，但其内容象块类型元素一样显示。
  list-item 象块类型元素一样显示，并添加样式列表标记。
  none 显示为空

#### 7. position的值relative和absolute定位原点是？
  absolute
    生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。

  fixed （老IE不支持）
    生成绝对定位的元素，相对于浏览器窗口进行定位。

  relative
    生成相对定位的元素，相对于其正常位置进行定位。

  static
    默认值。没有定位，元素出现在正常的流中
   （忽略 top, bottom, left, right z-index 声明）。

  inherit
    规定从父元素继承 position 属性的值。  

#### 8. CSS3有哪些新特性？
  CSS3实现圆角（border-radius:8px），
  阴影（box-shadow:10px），
  文字特效（text-shadow、），
  线性渐变（gradient），
  旋转（transform）
  transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);//旋转,缩放,定位,倾斜
  增加了更多的CSS选择器
  多背景 rgba

#### 9. 请解释一下CSS3的Flexbox（弹性盒布局模型）,以及适用场景？

#### 10. 用纯CSS创建一个三角形的原理是什么？
把上、左、右三条边隐藏掉（颜色设为 transparent）
	#demo {
	  width: 0;
	  height: 0;
	  border-width: 20px;
	  border-style: solid;
	  border-color: transparent transparent red transparent;
	}

#### 11. 一个满屏 品 字布局 如何设计?
简单的方式：
    上面的div宽100%，
    下面的两个div分别宽50%，
    然后用float或者inline使其不换行即可

#### 12. 常见兼容性问题？
* png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.

* 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

* IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。

  浮动ie产生的双倍距离 #box{ float:left; width:10px; margin:0 0 0 100px;}

  这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入 ——_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

  渐进识别的方式，从总体中逐渐排除局部。

  首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。
  接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

	  css
	      .bb{
	          background-color:#f1ee18;/*所有识别*/
	          .background-color:#00deff\9; /*IE6、7、8识别*/
	          +background-color:#a200ff;/*IE6、7识别*/
	          _background-color:#1e0bd1;/*IE6识别*/
	      }

*  IE下,可以使用获取常规属性的方法来获取自定义属性,
   也可以使用getAttribute()获取自定义属性;
   Firefox下,只能使用getAttribute()获取自定义属性。
   解决方法:统一通过getAttribute()获取自定义属性。

*  IE下,even对象有x,y属性,但是没有pageX,pageY属性;
   Firefox下,event对象有pageX,pageY属性,但是没有x,y属性。

*  解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。

*  Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,
   可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。

超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序:
L-V-H-A :  a:link {} a:visited {} a:hover {} a:active {}

#### 12. li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

#### 13. 为什么要初始化CSS样式。
- 因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。

- 当然，初始化样式会对SEO有一定的影响，但鱼和熊掌不可兼得，但力求影响最小的情况下初始化。

最简单的初始化方法： * {padding: 0; margin: 0;} （强烈不建议）

淘宝的样式初始化代码：

	body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; }
	body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; }
	h1, h2, h3, h4, h5, h6{ font-size:100%; }
	address, cite, dfn, em, var { font-style:normal; }
	code, kbd, pre, samp { font-family:couriernew, courier, monospace; }
	small{ font-size:12px; }
	ul, ol { list-style:none; }
	a { text-decoration:none; }
	a:hover { text-decoration:underline; }
	sup { vertical-align:text-top; }
	sub{ vertical-align:text-bottom; }
	legend { color:#000; }
	fieldset, img { border:0; }
	button, input, select, textarea { font-size:100%; }
	table { border-collapse:collapse; border-spacing:0; }

#### 14. absolute的containing block(容器块)计算方式跟正常流有什么不同？
无论属于哪种，都要先找到其祖先元素中最近的 position 值不为 static 的元素，然后再判断：
1、若此元素为 inline 元素，则 containing block 为能够包含这个元素生成的第一个和最后一个 inline box 的 padding box (除 margin, border 外的区域) 的最小矩形；
2、否则,则由这个祖先元素的 padding box 构成。
如果都找不到，则为 initial containing block。

补充：
1. static(默认的)/relative：简单说就是它的父元素的内容框（即去掉padding的部分）
2. absolute: 向上找最近的定位为absolute/relative的元素
3. fixed: 它的containing block一律为根元素(html/body)，根元素也是initial containing block

#### 15. CSS里的visibility属性有个collapse属性值是干嘛用的？在不同浏览器下以后什么区别？

#### 16. position跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样？

#### 17. 对BFC规范(块级格式化上下文：block formatting context)的理解？
W3C CSS 2.1 规范中的一个概念,它是一个独立容器，决定了元素如何对其内容进行定位,以及与其他元素的关系和相互作用。）
 一个页面是由很多个 Box 组成的,元素的类型和 display 属性,决定了这个 Box 的类型。
 不同类型的 Box,会参与不同的 Formatting Context（决定如何渲染文档的容器）,因此Box内的元素会以不同的方式渲染,也就是说BFC内部的元素和外部的元素不会互相影响。

#### 18. css定义的权重
以下是权重的规则：标签的权重为1，class的权重为10，id的权重为100，以下例子是演示各种定义的权重值：

	/*权重为1*/
	div{
	}
	/*权重为10*/
	.class1{
	}
	/*权重为100*/
	#id1{
	}
	/*权重为100+1=101*/
	#id1 div{
	}
	/*权重为10+1=11*/
	.class1 div{
	}
	/*权重为10+10+1=21*/
	.class1 .class2 div{
	}

如果权重相同，则最后定义的样式会起作用，但是应该避免这种情况出现

#### 19. 请解释一下为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式

#### 20. 移动端的布局用过媒体查询吗？

#### 21. 使用 CSS 预处理器吗？喜欢那个？
SASS (SASS、LESS没有本质区别，只因为团队前端都是用的SASS)

#### 22. CSS优化、提高性能的方法有哪些？

#### 23. 浏览器是怎样解析CSS选择器的？

#### 24. 在网页中的应该使用奇数还是偶数的字体？为什么呢？

#### 25. margin和padding分别适合什么场景使用？

#### 26. 抽离样式模块怎么写，说出思路，有无实践经验？[阿里航旅的面试题]

#### 27. 元素竖向的百分比设定是相对于容器的高度吗？

#### 28. 全屏滚动的原理是什么？用到了CSS的那些属性？

#### 29. 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？

#### 30. 视差滚动效果，如何给每页做不同的动画？（回到顶部，向下滑动要再次出现，和只出现一次分别怎么做？）

#### 31. ::before 和 :after中双冒号和单冒号 有什么区别？解释一下这2个伪元素的作用。

#### 32. 如何修改chrome记住密码后自动填充表单的黄色背景 ？

#### 33. 你对line-height是如何理解的？

#### 34. 设置元素浮动后，该元素的display值是多少？（自动变成display:block）

#### 35. 怎么让Chrome支持小于12px 的文字？

#### 36. 让页面里的字体变清晰，变细用CSS怎么做？
（-webkit-font-smoothing: antialiased;）

#### 37. font-style属性可以让它赋值为“oblique” oblique是什么意思？

#### 38. position:fixed;在android下无效怎么处理？

#### 39. 如果需要手动写动画，你认为最小时间间隔是多久，为什么？（阿里）
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms

#### 40. display:inline-block 什么时候会显示间隙？(携程)
移除空格、使用margin负值、使用font-size:0、letter-spacing、word-spacing

#### 41. overflow: scroll时不能平滑滚动的问题怎么处理？
在ios上
	-webkit-overflow-scrolling: touch;

#### 42. 有一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度。

#### 43. png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过webp？

1. gif图形交换格式，索引颜色格式，颜色少的情况下，产生的文件极小，支持背景透明，动画，图形渐进，无损压缩（适合线条，图标等），缺点只有256种颜色
2. jpg支持上百万种颜色，有损压缩，压缩比可达180：1，而且质量受损不明显，不支持图形渐进与背景透明，不支持动画
3. png为替代gif产生的，位图文件，支持透明，半透明，不透明。不支持动画，无损图像格式。Png8简单说是静态gif，也只有256色，png24不透明，但不止256色。
4. webp谷歌开发的旨在加快图片加载速度的图片格式，图片压缩体积是jpeg的2/3，有损压缩。高版本的W3C浏览器才支持，google39+，safari7+

CSS 中类 (classes) 和 ID 的区别。
请问 "resetting" 和 "normalizing" CSS 之间的区别？你会如何选择，为什么？
请解释浮动 (Floats) 及其工作原理。
描述z-index和叠加上下文是如何形成的。
请描述 BFC(Block Formatting Context) 及其如何工作。
列举不同的清除浮动的技巧，并指出它们各自适用的使用场景。
请解释 CSS sprites，以及你要如何在页面或网站中实现它。
你最喜欢的图片替换方法是什么，你如何选择使用。
你会如何解决特定浏览器的样式问题？
如何为有功能限制的浏览器提供网页？
你会使用哪些技术和处理方法？
有哪些的隐藏内容的方法 (如果同时还要保证屏幕阅读器可用呢)？
你用过栅格系统 (grid system) 吗？如果使用过，你最喜欢哪种？
你用过媒体查询，或针对移动端的布局/CSS 吗？
你熟悉 SVG 样式的书写吗？
如何优化网页的打印样式？
在书写高效 CSS 时会有哪些问题需要考虑？
使用 CSS 预处理器的优缺点有哪些？
请描述你曾经使用过的 CSS 预处理器的优缺点。
如果设计中使用了非标准的字体，你该如何去实现？
请解释浏览器是如何判断元素是否匹配某个 CSS 选择器？
请描述伪元素 (pseudo-elements) 及其用途。
请解释你对盒模型的理解，以及如何在 CSS 中告诉浏览器使用不同的盒模型来渲染你的布局。
请解释 * { box-sizing: border-box; } 的作用, 并且说明使用它有什么好处？
请罗列出你所知道的 display 属性的全部值
请解释 inline 和 inline-block 的区别？
请解释 relative、fixed、absolute 和 static 元素的区别
CSS 中字母 'C' 的意思是叠层 (Cascading)。请问在确定样式的过程中优先级是如何决定的 (请举例)？如何有效使用此系统？
你在开发或生产环境中使用过哪些 CSS 框架？你觉得应该如何改善他们？
请问你有尝试过 CSS Flexbox 或者 Grid 标准规格吗？
为什么响应式设计 (responsive design) 和自适应设计 (adaptive design) 不同？
你有兼容 retina 屏幕的经历吗？如果有，在什么地方使用了何种技术？
请问为何要使用 translate() 而非 absolute positioning，或反之的理由？为什么？
#### 实现一个footer固定在底部，当内容不够一屏时固定在页面底部，当超出一屏时在页面最下方。

#### 怎么引入一个新的字体

	@font-face {

		/* font-properties */

		font-family: 用户自定义的字体名称;

		src:url('加载外部字体文件的文件地址'),  

		url('加载外部字体文件的文件地址'),

		url('加载外部字体文件的文件地址'); /* IE9 */

	}

#### iconfront使用过吗，怎么引入

#### flex实现垂直居中布局，实现左固定，右充填的布局或者上固定，下充填的布局

#### grid栅格布局

#### z-index在什么情况下生效，又在什么情况下失效

#### 请解释一下bfc

#### 浮动的产生和怎么清楚浮动



















