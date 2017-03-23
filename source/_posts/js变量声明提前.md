title: js变量声明提前
date: 2016-03-18 14:20:01
tags:
- js
---
##### 在一些代码如c中都有块级作用域的概念，即在一个花括号内定义的变量只是局部变量，每个变量都有他自己的作用域（一般来说是变量定义之后花括号结束之前），而js不一样，js的执行区间（即作用域）十分有意思，因为在执行区间之内js定义的局部变量声明会提前，所以如果不太了解这个机制的话有可能写代码的时候会出现一些你意想不到的结果。下面我们就来聊聊这个机制。
	
	var a = "hello"
	function f(){
		console.log(a);
		var a = "world"
		console.log(a);
	}
	f();
	输出结果为 undefind world 

##### 为什么会出现这样的结果呢？为什么不实 hello world 或者 world world ？这就涉及到了js的变量声明提前。
##### 以上代码等同于

	var a = "hello"
	function f(){
	    var a;  //变量声明提前
		console.log(a);
		a = "world"
		console.log(a);
	}
	f();
##### 也就是相当于在函数开始的时候定义了变量，但是没有赋值，所以第一个console.log(a)输出为 undefind。
##### 那么下面这种情况呢？

	var a = "hello"
	function f(){
		console.log(a);
		a = "world"
		console.log(a);
	}
	f();

##### 输出是什么？

##### 没错，就是 hello world。那为什么呢？

##### 那是因为在js中，如果变量声明没有加 var 关键字时，即定义的是全局变量。所以第一个console.log(a)输出hello，然后把world赋值给全局变量a，第二个console.log(a)输出为world。

##### so，这就是js的变量声明提前，简单吧Y(^_^)Y

以上。












