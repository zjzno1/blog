title: 前端面试题js相关总结
date: 2016-03-19 18:04:19
tags:
- js
- 面试题（知识点）总结
---
### js相关问题

#### 1. 介绍js的基本数据类型。
` Undefined、Null、Boolean、Number、String`

#### 2. 介绍js有哪些内置对象？
Object 是 JavaScript 中所有对象的父对象

数据封装类对象：Object、Array、Boolean、Number 和 String
其他对象：Function、Arguments、Math、Date、RegExp、Error

#### 3. 说几条写JavaScript的基本规范？
1.不要在同一行声明多个变量。
2.请使用 ===/!==来比较true/false或者数值
3.使用对象字面量替代new Array这种形式
4.不要使用全局函数。
5.Switch语句必须带有default分支
6.函数不应该有时候有返回值，有时候没有返回值。
7.For循环必须使用大括号
8.If语句必须使用大括号
9.for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污染。

#### 4. JavaScript原型，原型链 ? 有什么特点？<font style="color:red">(有疑问，函数对象有prototype，而普通对象没有。。写完查一下再来补充)</font>
每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，
如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，
于是就这样一直找下去，也就是我们平时所说的原型链的概念。
关系：`instance.constructor.prototype = instance._proto_`

特点：
JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。


 当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话，
 就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。

    function Func(){}
    Func.prototype.name = "Sean";
    Func.prototype.getInfo = function() {
      return this.name;
    }
    var person = new Func();//现在可以参考var person = Object.create(oldObject);
    console.log(person.getInfo());//它拥有了Func的属性和方法
    //"Sean"
    console.log(Func.prototype);
    // Func { name="Sean", getInfo=function()}

#### 5. JavaScript有几种类型的值？，你能画一下他们的内存图吗？
栈：原始数据类型（Undefined，Null，Boolean，Number、String） 
堆：引用数据类型（对象、数组和函数）

两种类型的区别是：存储位置不同；
原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其
在栈中的地址，取得地址后从堆中获得实体

<img src="http://ww3.sinaimg.cn/mw690/a5152f55gw1f235pmmhmmj20lm0nqwfe.jpg" style="width:430px;" />

#### 6. Javascript如何实现继承？
1、构造继承
2、原型继承
3、实例继承
4、拷贝继承

原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。

	 function Parent(){
	        this.name = 'wang';
	    }

	    function Child(){
	        this.age = 28;
	    }
	    Child.prototype = new Parent();//继承了Parent，通过原型

	    var demo = new Child();
	    alert(demo.age);
	    alert(demo.name);//得到被继承的属性
	  }

#### 7. javascript创建对象的几种方式？
javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用。


1、对象字面量的方式   

    person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};

2、用function来模拟无参的构造函数

    function Person(){}
    var person=new Person();//定义一个function，如果使用new"实例化",该function可以看作是一个Class
    person.name="Mark";
    person.age="25";
    person.work=function(){
    alert(person.name+" hello...");
    }
    person.work();

3、用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）

    function Pet(name,age,hobby){
       this.name=name;//this作用域：当前对象
       this.age=age;
       this.hobby=hobby;
       this.eat=function(){
          alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
       }
    }
    var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
    maidou.eat();//调用eat方法


4、用工厂方式来创建（内置对象）

     var wcDog =new Object();
     wcDog.name="旺财";
     wcDog.age=3;
     wcDog.work=function(){
       alert("我是"+wcDog.name+",汪汪汪......");
     }
     wcDog.work();


5、用原型方式来创建

    function Dog(){

     }
     Dog.prototype.name="旺财";
     Dog.prototype.eat=function(){
     alert(this.name+"是个吃货");
     }
     var wangcai =new Dog();
     wangcai.eat();


5、用混合方式来创建

    function Car(name,price){
      this.name=name;
      this.price=price; 
    }
     Car.prototype.sell=function(){
       alert("我是"+this.name+"，我现在卖"+this.price+"万元");
      }
    var camry =new Car("凯美瑞",27);
    camry.sell(); 

#### 8. Javascript作用链域?
全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。
当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，
直至全局函数，这种组织形式就是作用域链。

#### 9. 谈谈This对象的理解。
那就是this指的是，调用函数的那个对象。 

#### 10. eval是做什么的？
它的功能是把对应的字符串解析成JS代码并运行；
应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。

#### 11. 什么是window对象? 什么是document对象?
Window -- 代表浏览器中一个打开的窗口
document对象 -- 代表整个HTML 文档,可用来访问页面中的所有元素

#### 12. null，undefined 的区别？
null        表示一个对象被定义了，值为“空值”；
undefined   表示不存在这个值。


typeof undefined
    //"undefined"
    undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined； 
    例如变量被声明了，但没有赋值时，就等于undefined

typeof null
    //"object"
    null : 是一个对象(空对象, 没有任何属性和方法)；
    例如作为函数的参数，表示该函数的参数不是对象；

注意：
    在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined


再来一个例子：

    null
    Q：有张三这个人么？
    A：有！
    Q：张三有房子么？
    A：没有！

    undefined
    Q：有张三这个人么？
    A：没有！

#### 13. 写一个通用的事件侦听器函数。

    // event(事件)工具集，来源：github.com/markyun
    markyun.Event = {
        // 页面加载完成后
        readyEvent : function(fn) {
            if (fn==null) {
                fn=document;
            }
            var oldonload = window.onload;
            if (typeof window.onload != 'function') {
                window.onload = fn;
            } else {
                window.onload = function() {
                    oldonload();
                    fn();
                };
            }
        },
        // 视能力分别使用dom0||dom2||IE方式 来绑定事件
        // 参数： 操作的元素,事件名称 ,事件处理程序
        addEvent : function(element, type, handler) {
            if (element.addEventListener) {
                //事件类型、需要执行的函数、是否捕捉
                element.addEventListener(type, handler, false);
            } else if (element.attachEvent) {
                element.attachEvent('on' + type, function() {
                    handler.call(element);
                });
            } else {
                element['on' + type] = handler;
            }
        },
        // 移除事件
        removeEvent : function(element, type, handler) {
            if (element.removeEventListener) {
                element.removeEventListener(type, handler, false);
            } else if (element.datachEvent) {
                element.detachEvent('on' + type, handler);
            } else {
                element['on' + type] = null;
            }
        },
        // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
        stopPropagation : function(ev) {
            if (ev.stopPropagation) {
                ev.stopPropagation();
            } else {
                ev.cancelBubble = true;
            }
        },
        // 取消事件的默认行为
        preventDefault : function(event) {
            if (event.preventDefault) {
                event.preventDefault();
            } else {
                event.returnValue = false;
            }
        },
        // 获取事件目标
        getTarget : function(event) {
            return event.target || event.srcElement;
        },
        // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
        getEvent : function(e) {
            var ev = e || window.event;
            if (!ev) {
                var c = this.getEvent.caller;
                while (c) {
                    ev = c.arguments[0];
                    if (ev && Event == ev.constructor) {
                        break;
                    }
                    c = c.caller;
                }
            }
            return ev;
        }
    };

#### 14. [“1”, “2”, “3”].map(parseInt) 答案是多少？
[1, NaN, NaN] 因为 parseInt 需要两个参数 (val, radix)，
 其中 radix 表示解析时用的基数。
 map 传了 3 个 (element, index, array)，对应的 radix 不合法导致解析失败。

#### 15. 事件是？IE与火狐的事件机制有什么区别？ 如何阻止冒泡？
 1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。
 2. 事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件；
 3. ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;）

#### 15. 什么是闭包（closure），为什么要用它？
闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。

闭包的特性：

1.函数内再嵌套函数
2.内部函数可以引用外层的参数和变量
3.参数和变量不会被垃圾回收机制回收

//li节点的onclick事件都能正确的弹出当前被点击的li索引
	
	 <ul id="testUL">
	    <li> index = 0</li>
	    <li> index = 1</li>
	    <li> index = 2</li>
	    <li> index = 3</li>
	</ul>
	<script type="text/javascript">
	    var nodes = document.getElementsByTagName("li");
	    for(i = 0;i<nodes.length;i+= 1){
	        nodes[i].onclick = function(){
	            console.log(i+1);//不用闭包的话，值每次都是4
	        }(i);
	    }
	</script>



执行say667()后,say667()闭包内部变量会存在,而闭包内部函数的内部变量不会存在
使得Javascript的垃圾回收机制GC不会收回say667()所占用的资源
因为say667()的内部函数的执行需要依赖say667()中的变量
这是对闭包作用的非常直白的描述

	  function say667() {
	    // Local variable that ends up within closure
	    var num = 666;
	    var sayAlert = function() {
	        alert(num);
	    }
	    num++;
	    return sayAlert;
	}

	 var sayAlert = say667();
	 sayAlert()//执行结果应该弹出的667

#### 16. javascript 代码中的”use strict”;是什么意思 ? 使用它区别是什么？
use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行,

使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。
默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;

提高编译器效率，增加运行速度；
为未来新版本的Javascript标准化做铺垫。

#### 16. 如何判断一个对象是否属于某个类？
使用instanceof （待完善）
   if(a instanceof Person){
       alert('yes');
   }
#### 17. new操作符具体干了什么呢?
     1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
     2、属性和方法被加入到 this 引用的对象中。
     3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。

var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);

#### 18. 用原生JavaScript的实现过什么功能吗？
开放性问答，略。

#### 19. Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？
hasOwnProperty

javaScript中hasOwnProperty函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性；该属性必须是对象本身的一个成员。
使用方法：
object.hasOwnProperty(proName)
其中参数object是必选项。一个对象的实例。
proName是必选项。一个属性名称的字符串值。

如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。

#### 20. JSON 的了解？
JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。
它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小
如：{"age":"12", "name":"back"}

#### 21. [].forEach.call($$("*"),function(a){a.style.outline="1px solid #"+(~~(Math.random()*(1<<24))).toString(16)}) 能解释一下这段代码的意思吗？

#### 22. js延迟加载的方式有哪些？
defer和async、动态创建DOM方式（用得最多）、按需异步载入js

#### 23. Ajax 是什么? 如何创建一个Ajax？
ajax的全称：Asynchronous Javascript And XML。
异步传输+js+xml。
所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。

(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象
(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
(3)设置响应HTTP请求状态变化的函数
(4)发送HTTP请求
(5)获取异步调用返回的数据
(6)使用JavaScript和DOM实现局部刷新

#### 24. 同步和异步的区别?
同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,j进行下一步操作。
异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容。

#### 25. 如何解决跨域问题?
jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面(详见本博客跨域及解决办法)

#### 26. 页面编码和被请求的资源编码如果不一致如何处理？

#### 27. 模块化开发怎么做？
sea.js cmd amd 规范

#### 28. AMD（Modules/Asynchronous-Definition）、CMD（Common Module Definition）规范区别？
AMD 规范在这里：https://github.com/amdjs/amdjs-api/wiki/AMD
CMD 规范在这里：https://github.com/seajs/seajs/issues/242

	Asynchronous Module Definition，异步模块定义，所有的模块将被异步加载，模块加载不影响后面语句运行。所有依赖某些模块的语句均放置在回调函数中。

	 区别：

	    1. 对于依赖的模块，AMD 是提前执行，CMD 是延迟执行。不过 RequireJS 从 2.0 开始，也改成可以延迟执行（根据写法不同，处理方式不同）。CMD 推崇 as lazy as possible.
	    2. CMD 推崇依赖就近，AMD 推崇依赖前置。看代码：

	// CMD
	define(function(require, exports, module) {
	    var a = require('./a')
	    a.doSomething()
	    // 此处略去 100 行
	    var b = require('./b') // 依赖可以就近书写
	    b.doSomething()
	    // ...
	})

	// AMD 默认推荐
	define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好
	    a.doSomething()
	    // 此处略去 100 行
	    b.doSomething()
	    // ...
	})


#### 29. requireJS的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何缓存的？）

#### 30. 谈一谈你对ECMAScript6的了解？

#### 31. ECMAScript6 怎么写class么，为什么会出现class这种东西?

#### 32. 异步加载JS的方式有哪些？
 (1) defer，只支持IE
 (2) async：
 (3) 创建script，插入到DOM中，加载完毕后callBack

#### 33. documen.write和 innerHTML的区别
document.write只能重绘整个页面
innerHTML可以重绘页面的一部分

#### 34. DOM操作——怎样添加、移除、移动、复制、创建和查找节点?
（1）创建新节点
  createDocumentFragment()    //创建一个DOM片段
  createElement()   //创建一个具体的元素
  createTextNode()   //创建一个文本节点
（2）添加、移除、替换、插入
  appendChild()
  removeChild()
  replaceChild()
  insertBefore() //在已有的子节点前插入一个新的子节点
（3）查找
  getElementsByTagName()    //通过标签名称
  getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
  getElementById()    //通过元素Id，唯一性

#### 35. .call() 和 .apply() 的区别？
  例子中用 add 来替换 sub，add.call(sub,3,1) == add(3,1) ，所以运行结果为：alert(4);

  注意：js 中的函数其实是对象，函数名是对 Function 对象的引用。

    function add(a,b)
    {
        alert(a+b);
    }

    function sub(a,b)
    {
        alert(a-b);
    }

    add.call(sub,3,1);

#### 36. 数组和对象有哪些原生方法，列举一下？
pop push sort join concat reverse shift isNaN split toLowerCase toUpperCase getDate getMonth等等。

#### 37. 数组和对象有哪些原生方法，列举一下？
重复，同上。

#### 38. JS 怎么实现一个类。怎么实例化这个类

#### 39. JavaScript中的作用域与变量声明提升？

#### 40. 如何编写高性能的Javascript？

#### 41. 那些操作会造成内存泄漏？

#### 42. JQuery的源码看过吗？能不能简单概况一下它的实现原理？

#### 43. jQuery.fn的init方法返回的this指的是什么对象？为什么要返回this？

#### 44. jquery中如何将数组转化为json字符串，然后再转化回来？

#### 45. jQuery 的属性拷贝(extend)的实现原理是什么，如何实现深拷贝？

#### 46. jquery.extend 与 jquery.fn.extend的区别？

#### 47. jQuery 的队列是如何实现的？队列可以用在哪些地方？

#### 48. 谈一下Jquery中的bind(),live(),delegate(),on()的区别？

#### 49. JQuery一个对象可以同时绑定多个事件，这是如何实现的？

#### 50. 是否知道自定义事件。jQuery里的fire函数是什么意思，什么时候用？

#### 51. jQuery 是通过哪个方法和 Sizzle 选择器结合的？（jQuery.fn.find()进入Sizzle）

#### 52. 针对 jQuery性能的优化方法？

#### 53. Jquery与jQuery UI 有啥区别？
*jQuery是一个js库，主要提供的功能是选择器，属性修改和事件绑定等等。

*jQuery UI则是在jQuery的基础上，利用jQuery的扩展性，设计的插件。
 提供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等

#### 54. JQuery的源码看过吗？能不能简单说一下它的实现原理？

#### 55. jquery 中如何将数组转化为json字符串，然后再转化回来？
jQuery中没有提供这个功能，所以你需要先编写两个jQuery的扩展：

    $.fn.stringifyArray = function(array) {
        return JSON.stringify(array)
    }

    $.fn.parseArray = function(array) {
        return JSON.parse(array)
    }

    然后调用：
    $("").stringifyArray(array)

#### 56. jQuery和Zepto的区别？各自的使用场景？

#### 57. 针对 jQuery 的优化方法？
*基于Class的选择性的性能相对于Id选择器开销很大，因为需遍历所有DOM元素。

*频繁操作的DOM，先缓存起来再操作。用Jquery的链式调用更好。
 比如：var str=$("a").attr("href");

*for (var i = size; i < arr.length; i++) {}
 for 循环每一次循环都查找了数组 (arr) 的.length 属性，在开始循环的时候设置一个变量来存储这个数字，可以让循环跑得更快：
 for (var i = size, length = arr.length; i < length; i++) {}

#### 58. Zepto的点透问题如何解决？

#### 59. jQueryUI如何自定义组件?

#### 60. 需求：实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后退时正确响应。给出你的技术实现方案？

#### 61. 如何判断当前脚本运行在浏览器还是node环境中？（阿里）

#### 62. 通过判断Global对象是否为window，如果不为window，当前脚本没有运行在浏览器中

#### 63. 移动端最小触控区域是多大？

#### 64. jQuery 的 slideUp动画 ，如果目标元素是被外部事件驱动, 当鼠标快速地连续触发外部元素事件, 动画会滞后的反复执行，该如何处理呢?

#### 65. 把 Script 标签 放在页面的最底部的body封闭之前 和封闭之后有什么区别？浏览器会如何解析它们？

#### 66. 移动端的点击事件的有延迟，时间是多久，为什么会有？ 怎么解决这个延时？
click 有 300ms 延迟,为了实现safari的双击事件的设计，浏览器要知道你是不是要双击操作。

#### 67. 知道各种JS框架(Angular, Backbone, Ember, React, Meteor, Knockout…)么? 能讲出他们各自的优点和缺点么?

#### 68. Underscore 对哪些 JS 原生对象进行了扩展以及提供了哪些好用的函数方法？

#### 69. 解释JavaScript中的作用域与变量声明提升？
详解本博客js变量声明提前

#### 70. 那些操作会造成内存泄漏？
内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

#### 71. JQuery一个对象可以同时绑定多个事件，这是如何实现的？

#### 72. Node.js的适用场景？

#### 73. (如果会用node)知道route, middleware, cluster, nodemon, pm2, server-side rendering么?

#### 74. 解释一下 Backbone 的 MVC 实现方式？

#### 75. 什么是“前端路由”?什么时候适合使用“前端路由”? “前端路由”有哪些优点和缺点?

#### 76. 知道什么是webkit么? 知道怎么用浏览器的各种工具来调试和debug代码么?

#### 77. 如何测试前端代码么? 知道BDD, TDD, Unit Test么? 知道怎么测试你的前端工程么(mocha, sinon, jasmin, qUnit..)?

#### 78. 前端templating(Mustache, underscore, handlebars)是干嘛的, 怎么用?

#### 79. 简述一下 Handlebars 的基本用法？

#### 80. 简述一下 Handlerbars 的对模板的基本处理流程， 如何编译的？如何缓存的？

#### 81. 用js实现千位分隔符?(来源：前端农民工，提示：正则+replace)

	function commafy(num) {
	     num = num + '';
	     var reg = /(-?d+)(d{3})/;

	    if(reg.test(num)){
	     num = num.replace(reg, '$1,$2');
	    }
	    return num;
	}
	
#### 82. 检测浏览器版本版本有哪些方式？
功能检测、userAgent特征检测

比如：navigator.userAgent
//"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"









































