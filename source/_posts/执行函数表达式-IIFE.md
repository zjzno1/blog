title: js立即执行函数表达式(IIFE)
date: 2017-08-31 10:34:10
tags:
- js
- IIFE
---

有时需要在定义函数之后，立即调用该函数。这种函数就叫做立即执行函数，全称为立即调用的函数表达式IIFE(Imdiately Invoked Function Expression)。

　[注意]javascript引擎规定，如果function关键字出现在行首，一律解释成函数声明语句。
	
	//声明语句（必须有函数名）
	function foo(){}

所以，解决方法就是不要让function出现在行首，让引擎将其理解成一个表达式

最常用的两种写法：

	(function(){ /* code */ }()); 
	(function(){ /* code */ })(); 

其他写法：

	!function(){ /* code */ }();
	~function(){ /* code */ }();
	-function(){ /* code */ }();
	+function(){ /* code */ }();

	var i = function(){ return 10; }();
	true && function(){ /* code */ }();
	0, function(){ /* code */ }();
