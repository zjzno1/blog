title: js事件绑定与事件委托
date: 2016-03-22 10:50:36
tags:
- js
- 事件绑定
- 事件委托
---
早就准备总结这篇文章，但一直没动笔，今天抽个空总结一下。

事件绑定，顾名思义，就是把js绑定到一个html的元素上，比如：

html文件：

	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <title>Document</title>
	</head>
	<body>
	  <ul id="list">
	    <li>1</li>
	    <li>2</li>
	    <li>3</li>
	    <li>4</li>
	    <li>5</li>
	  </ul>
	</body>
	</html>

js文件：
	$('#list li').on('click', function() {
	    alert(($(this).html()));
	});
这就是事件绑定，其实现原理是分别给list下的`<li>绑定click事件，这样做的弊端在于加大了内存的压力，因为$('#list li')要存放n个li对象，同时会降低代码的性能，因为$('#list li')会搜索#list下的所有li元素。

=======================================分割线==========================================

那么针对这种情况，有没有什么比较好的解决方案？

当然有，那就是js的时间委托。

	$('#data-list').on('click', 'li', function() {
	    alert(($(this).html()));
	});
这么做的原理是js具有事件冒泡机制，内层元素的事件被触发，时间会一层一层的冒到更外层的元素，并且当外层事件被触发时，会判断事件的来源即event.target是否是目标元素li，如果是就执行回调。

	以上代码等同于：

	function showText(text) {
	    alert((text));
	}

	$('#data-list').on('click', function(event) {
	    var $target = $(event.target);
	    if ($target.is('li')) {
	        showText($target.html());
	    }
	});

这样做的好处不仅仅提高了内存的利用率，还在页面动态变化之后，不需要重新检查元素与添加绑定事件，也方便ajax操作dom。







