title: es6编程风格规范
date: 2019-02-12 09:21:35
tags:
- es6
- js
---

### (1) 使用let，const 取代 var
	在let和const之间，建议优先使用const，尤其是在全局环境，不应该设置变量，只应设置常量。

		// bad
		var a = 1, b = 2, c = 3;

		// good
		const a = 1;
		const b = 2;
		const c = 3;

		// best
		const [a, b, c] = [1, 2, 3];


### (2) 静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号。

	// good
	const a = 'foobar';
	const b = `foo${a}bar`;

### (3) 使用数组成员对变量赋值时，优先使用解构赋值。
	
	const arr = [1, 2, 3, 4];
	// good
	const [first, second] = arr;

函数的参数如果是对象的成员，优先使用解构赋值。
	
	// bad
	function getFullName(user) {
	  const firstName = user.firstName;
	  const lastName = user.lastName;
	}

	// good
	function getFullName(obj) {
	  const { firstName, lastName } = obj;
	}

	// best
	function getFullName({ firstName, lastName }) {
	}

如果函数返回多个值，优先使用对象的解构赋值，而不是数组的解构赋值。这样便于以后添加返回值，以及更改返回值的顺序。

	// bad
	function processInput(input) {
	  return [left, right, top, bottom];
	}

	// good
	function processInput(input) {
	  return { left, right, top, bottom };
	}

	const { left, right } = processInput(input);

### (4) 单行定义的对象，最后一个成员不以逗号结尾。多行定义的对象，最后一个成员以逗号结尾。
	
	// good
	const a = { k1: v1, k2: v2 };
	const b = {
	  k1: v1,
	  k2: v2,
	};

对象尽量静态化，一旦定义，就不得随意添加新的属性。如果添加属性不可避免，要使用Object.assign方法。
	
	// if reshape unavoidable
	const a = {};
	Object.assign(a, { x: 3 });

	// good
	const a = { x: null };
	a.x = 3;

如果对象的属性名是动态的，可以在创造对象的时候，使用属性表达式定义。
	
	// bad
	const obj = {
	  id: 5,
	  name: 'San Francisco',
	};
	obj[getKey('enabled')] = true;

	// good
	const obj = {
	  id: 5,
	  name: 'San Francisco',
	  [getKey('enabled')]: true,
	};

另外，对象的属性和方法，尽量采用简洁表达法，这样易于描述和书写。

	var ref = 'some value';

	// bad
	const atom = {
	  ref: ref,

	  value: 1,

	  addValue: function (value) {
	    return atom.value + value;
	  },
	};

	// good
	const atom = {
	  ref,

	  value: 1,

	  addValue(value) {
	    return atom.value + value;
	  },
	};

### (5) 使用扩展运算符（...）拷贝数组。

	// good
	items = [1,2,3]
	const itemsCopy = [...items];

使用 Array.from 方法，将类似数组的对象转为数组。

	const foo = document.querySelectorAll('.foo');
	const nodes = Array.from(foo);

那些需要使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了 this。

	// good
	[1, 2, 3].map((x) => {
	  return x * x;
	});

	// best
	[1, 2, 3].map(x => x * x);

箭头函数取代Function.prototype.bind，不应再用 self/_this/that 绑定 this。

	// bad
	const self = this;
	const boundMethod = function(...params) {
	  return method.apply(self, params);
	}

	// acceptable
	const boundMethod = method.bind(this);

	// best
	const boundMethod = (...params) => method.apply(this, params);

所有配置项都应该集中在一个对象，放在最后一个参数，布尔值不可以直接作为参数。

	// bad
	function divide(a, b, option = false ) {
	}

	// good
	function divide(a, b, { option = false } = {}) {
	}

不要在函数体内使用 arguments 变量，使用 rest 运算符（...）代替。

	// bad
	function concatenateAll() {
	  const args = Array.prototype.slice.call(arguments);
	  return args.join('');
	}

	// good
	function concatenateAll(...args) {
	  return args.join('');
	}

使用默认值语法设置函数参数的默认值。

	// bad
	function handleThings(opts) {
	  opts = opts || {};
	}

	// good
	function handleThings(opts = {}) {
	  // ...
	}

### (7) Map 结构 
	注意区分 Object 和 Map，只有模拟现实世界的实体对象时，才使用 Object。如果只是需要key: value的数据结构，使用 Map 结构。因为 Map 有内建的遍历机制。

	let map = new Map(arr);

	for (let key of map.keys()) {
	  console.log(key);
	}

	for (let value of map.values()) {
	  console.log(value);
	}

	for (let item of map.entries()) {
	  console.log(item[0], item[1]);
	}

### (8) Class
	总是用 Class，取代需要 prototype 的操作。因为 Class 的写法更简洁，更易于理解。

	// bad
	function Queue(contents = []) {
	  this._queue = [...contents];
	}
	Queue.prototype.pop = function() {
	  const value = this._queue[0];
	  this._queue.splice(0, 1);
	  return value;
	}

	// good
	class Queue {
	  constructor(contents = []) {
	    this._queue = [...contents];
	  }
	  pop() {
	    const value = this._queue[0];
	    this._queue.splice(0, 1);
	    return value;
	  }
	}

使用 `extends` 实现继承，因为这样更简单，不会有破坏 `instanceof` 运算的危险。

	// bad
	const inherits = require('inherits');
	function PeekableQueue(contents) {
	  Queue.apply(this, contents);
	}
	inherits(PeekableQueue, Queue);
	PeekableQueue.prototype.peek = function() {
	  return this._queue[0];
	}

	// good
	class PeekableQueue extends Queue {
	  peek() {
	    return this._queue[0];
	  }
	}

### (9) 模块 
	首先，Module 语法是 JavaScript 模块的标准写法，坚持使用这种写法。使用 `import` 取代 `require`。

	// bad
	const moduleA = require('moduleA');
	const func1 = moduleA.func1;
	const func2 = moduleA.func2;

	// good
	import { func1, func2 } from 'moduleA';

	使用 `export` 取代 `module.exports`。

		// commonJS的写法
	var React = require('react');

	var Breadcrumbs = React.createClass({
	  render() {
	    return <nav />;
	  }
	});

	module.exports = Breadcrumbs;

	// ES6的写法
	import React from 'react';

	class Breadcrumbs extends React.Component {
	  render() {
	    return <nav />;
	  }
	};

	export default Breadcrumbs;

如果模块只有一个输出值，就使用export default，如果模块有多个输出值，就不使用export default，export default与普通的export不要同时使用。

不要在模块输入中使用通配符。因为这样可以确保你的模块之中，有一个默认输出（export default）。

	// bad
	import * as myObject from './importModule';

	// good
	import myObject from './importModule';

如果模块默认输出一个函数，函数名的首字母应该小写。

	function makeStyleGuide() {
	}

	export default makeStyleGuide;

如果模块默认输出一个对象，对象名的首字母应该大写。

	const StyleGuide = {
	  es6: {
	  }
	};

	export default StyleGuide;









