title: js函数柯里化
date: 2017-08-29 16:33:57
tags:
- js
- 柯里化
- 原型/原型链
---
柯里化通常也称部分求值，其含义是给函数分步传递参数，每次传递参数后部分应用参数，并返回一个更具体的函数接受剩下的参数，这中间可嵌套多层这样的接受部分参数函数，直至返回最后结果。

柯里化其实本身是固定一个可以预期的参数，并返回一个特定的函数，处理批特定的需求。这增加了函数的适用性，但同时也降低了函数的适用范围。

那么柯里话的好处呢？有以下三个方面：
柯里化有3个常见作用：1. 参数复用；2. 提前返回；3. 延迟计算/运行

通俗的说，就是一个函数接收一个参数，然后在return另一个函数接收另一个参数，如果参数长度任意，则map/reduce或者其他手段循环出来。

例如，一个确定只有两个参数的柯里化

	var add = function(x) {
	  return function(y) {
	    return x + y;
	  };
	};

	var increment = add(1);
	var addTen = add(10);

	increment(2);
	// 3

	addTen(2);
	// 12

这是add()中的形参x表示接收到的第一个参数，也就是`var increment = add(1)` 中的1和 `var addTen = add(10)` 中的10，`increment(2)`与`addTen(2)`中的2分别由y接收到。

那么参数长度不确定呢？

	var currying = function (fn) {
	    var _args = [];
	    return function () {
	        if (arguments.length === 0) {
	            return fn.apply(this, _args);
	        }
	        Array.prototype.push.apply(_args, [].slice.call(arguments));
	        return arguments.callee;
	    }
	};

	var multi=function () {
	    var total = 0;
	    for (var i = 0, c; c = arguments[i++];) {
	        total += c;
	    }
	    return total;
	};

	var sum = currying(multi);  
	  
	sum(100,200)(300);
	sum(400);
	console.log(sum());     // 1000  （空白调用时才真正计算）


