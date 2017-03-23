title: js回调函数
date: 2016-08-11 16:26:06
tags:
- js
- 回调函数
---
什么是js的回调函数，简而言之，就是把一个函数当做参数传入另一个函数中。

	funtion a(a,callback) {
		callback()
	}
	funtion b() {
		alert(a)
	}
	a(b)
其中，函数b就是函数a的回调函数。

那么回调函数如何传参？

	function a(callback){
		var m = 1;
		var n = 2;
		alert(callback(m,n));
	}
	function b(m,n){
		return m+n;
	}
	a(b);
	//alert得出3