title: js中的call和apply
date: 2016-08-11 16:40:45
tags:
- js
- call
- apply
---
call 和 apply 都是为了改变某个函数运行时的 context 即上下文而存在的，换句话说，就是为了改变函数体内部 this 的指向。

`fn.call(thisObj, arg1, arg2, ...);`
`fn.apply(thisObj, [arg1, arg2, ...]);`

两者作用一致，都是把fn(即fn中的this)绑定到thisObj，这时候thisObj具备了obj的属性和方法。或者说thisObj『继承』了obj的属性和方法。

唯一区别是apply接受的是数组参数，call接受的是连续参数。所以当参数固定时可以使用call，当参数不固定时使用apply。

举个栗子：
	// 改变this
	var obj = {
		name: 'linxin'
	}

	function func() {
		console.log(this.name);
	}

	func.call(obj);       // linxin

call 方法的第一个参数是作为函数上下文的对象，这里把 obj 作为参数传给了 func，此时函数里的 this 便指向了 obj 对象。此处 func 函数里其实相当于

	function func() {
		console.log(obj.name);
	}

调用原生对象的方法

	var a = {0:1, 1:"zjz", length: 2}; 
	a.slice(); //TypeError: a.slice is not a function
	Array.prototype.slice.call(a);//[1, "zjz"]

实现继承

	var Parent = function(){
	    this.name = "zjz";
	    this.age = 22;
	}
	var child = {};
	console.log(child);//Object {} ,空对象
	Parent.call(child);
	console.log(child); //Object {name: "zjz", age: 24}

#### bind的使用
`obj.bind(thisObj, arg1, arg2, ...);`

把obj绑定到thisObj，这时候thisObj具备了obj的属性和方法。与call和apply不同的是，bind绑定后不会立即执行。

同样是add()和sub()：

	add.bind(sub, 5, 3); //不再返回8
	add.bind(sub, 5, 3)(); //8

如果bind的第一个参数是null或者undefined，等于将this绑定到全局对象。







