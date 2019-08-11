title: AMD，CMD，commonJS，UMD和es6 module的概念与区别
date: 2016-12-13 09:45:41
tags:
- 规范
---

#### Javascript模块化

模块化是指在解决某一个复杂问题或者一系列的杂糅问题时，依照一种分类的思维把问题进行系统性的分解以之处理。模块化是一种处理复杂系统分解为代码结构更合理，可维护性更高的可管理的模块的方式。可以想象一个巨大的系统代码，被整合优化分割成逻辑性很强的模块时，对于软件是一种何等意义的存在。对于软件行业来说：解耦软件系统的复杂性，使得不管多么大的系统，也可以将管理，开发，维护变得“有理可循”。

首先，既然是模块化设计，那么作为一个模块化系统所必须的能力：
1. 定义封装的模块。
2. 定义新模块对其他模块的依赖。
3. 可对其他模块的引入支持。

#### 1.CommonJS和Node

CommonJS是服务器端模块的规范，Node.js采用了这个规范
##### CommonJS规范特点：
1. CommonJS 加载模块是同步的，所以只有加载完成才能执行后面的操作，模块加载的顺序按照其在代码中出现的顺序加载。由于Node.js主要用于服务器编程，模块文件一般都已经存在于本地硬盘，所以加载起来比较快，不用考虑非同步加载的方式，所以CommonJS规范比较适用。
2. 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。（输入的是被输出值的拷贝。也就是说，一旦输出一个值，模块内部的变化就影响不到这个值了）
3. 一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在一个文件定义的变量（还包括函数和类），都是私有的，对其他文件是不可见的。
使用方式：

根据CommonJS规范，一个单独的文件就是一个模块。加载模块使用require方法，该方法读取一个文件并执行，最后返回文件内部的exports对象。commonjs规定，每个模块内部，module变量代表当前模块，这个变量是一个对象，它的exports 属性（即module.exports）是对外的接口，加载某个模块，其实是加载该模块的module.exports属性

	// example.js
	let x = 5;
	let addX = function(value){
		return value + x;
	};
	
	module.exports.x = x;
	module.exports.addX = addX;

在上面代码通过  module.exports输出 变量x 和 函数 addX.

require 方法用于加载模块

	var example = require('./example.js')';
	console.log(example.x);
	console.log(example.addX(1);

为了方便，Node为每个模块提供一个exports变量，指向module.exports。这等同在每个模块头部，有一行这样的命令。 

var exports = module.exports;
于是我们可以直接在 exports 对象上添加方法，表示对外输出的接口，如同在module.exports上添加一样。注意，不能直接将exports变量指向一个值，因为这样等于切断了exports与module.exports的联系。
提出问题

但如果是浏览器环境，要从服务器加载模块，这是就必须采用异步模式。所以就有了 AMD  CMD 等解决方案。 那为什么在浏览器环境，就必须采用异步模式加载模块?

#### 2.AMD规范和RequireJs

AMD 全称是 Asynchronous Module Definition ，即异步模块加载机制
 

RequireJS 是一个前端的模块化管理的工具库，遵循AMD规范，它的作者就是AMD规范的创始人 James Burke。
RequireJS 的基本思想为：通过一个函数来将所有所需要的或者说所依赖的模块实现装载进来，然后返回一个新的函数（模块），我们所有的关于新模块的业务代码都在这个函数内部操作，其内部也可无限制的使用已经加载进来的模块。
RequireJs特点：

1. AMD规范是预加载，也就是说会将所有模块全加载，也可以实现动态加载(requirejs2.0 版本也支持)。
2. 管理模块之间的依赖性，便于代码的编写和维护，可以让代码松耦合

RequireJs的用法

	<script src="scripts/require.js"></script>
	<script src="scripts/main.js"></script>
 
那么scripts下的main.js则是指定的主代码脚本文件，所有的依赖模块代码文件都将从该文件开始异步加载进入执行。

define用于定义模块，RequireJS要求每个模块均放在独立的文件之中。按照是否有依赖其他模块的情况分为独立模块和非独立模块。

独立模块，不依赖其他模块。直接定义：

	define({
		method1: function(){},
		method2: function(){}
	});
	// 也等价于
	define(function(){
		return {
			method1: function(){},
			method2: function(){}
		}
	});

非独立模块，对其他模块有依赖。

	define([ 'module1', 'module2' ], function(m1, m2) {
		...
	});
	// 或者是
	define(function(require) {
		var m1 = require('module1'),
			m2 = require('module2');
		...
	});

require方法调用模块
在require进行调用模块时，其参数与define类似。

	require(['foo', 'bar'], function(foo, bar) {
		foo.func();
		bar.func();
	} );
 
define 和 require 这两个定义模块，调用模块的方法合称为AMD模式，定义模块清晰，不会污染全局变量，清楚的显示依赖关系。AMD模式可以用于浏览器环境并且允许非同步加载模块，也可以按需动态加载模块。

#### 3.CMD和SeaJS

CMD是SeaJS 在推广过程中对模块定义的规范化产出
Common Module Definition表示通用模块定义，该规范是国内发展出来的，由阿里的玉伯提出。

SeaJS特点：

1. CMD规范是懒加载，按需加载，也就是在require的时候相应的模块才会被加载进来。
2. 对于依赖的模块CMD是延迟执行。
3. AMD的API默认是一个当多个用，CMD严格的区分推崇职责单一。例如：AMD里require分全局的和局部的。CMD里面没有全局的 require，提供 seajs.use()来实现模块系统的加载启动。CMD里每个API都简单纯粹

	//AMD
	define(['./a','./b'], function (a, b) {
	
		//依赖一开始就写好
		a.test();
		b.test();
	});
	
	//CMD
	define(function (requie, exports, module) {
		
		//依赖可以就近书写
		var a = require('./a');
		a.test();
		
		...
		//软依赖, 动态加载
		if (status) {
		
			var b = requie('./b');
			b.test();
		}
	});

seajs 使用demo https://www.cnblogs.com/imwtr/p/4666150.html
https://www.jd.com/   js main.min.js 文件用的就是seaJs

#### 4.UMD

UMD是AMD和CommonJS的糅合

AMD模块以浏览器第一的原则发展，异步加载模块。

CommonJS模块以服务器第一原则发展，选择同步加载，它的模块无需包装。
这迫使人们又想出另一个更通用的模式UMD （Universal Module Definition）。希望解决跨平台的解决方案。
UMD先判断是否支持Node.js的模块（exports）是否存在，存在则使用Node.js模块模式。
在判断是否支持AMD（define是否存在），存在则使用AMD方式加载模块。

	(function (window, factory) {
		if (typeof exports === 'object') {
		
			module.exports = factory();
		} else if (typeof define === 'function' && define.amd) {
		
			define(factory);
		} else {
		
			window.eventUtil = factory();
		}
	})(this, function () {
		// module ...
	});

node 包 moment.js就是可以跨平台使用的，内部采用的就是这种写法

#### 5.ES6  Module模块化

ES6 的模块自动采用严格模式，不管你有没有在模块头部加上"use strict";。
 

模块功能主要由两个命令构成：export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。
 

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。下面是一个 JS 文件，里面使用export命令输出变量。

##### Module特点：

1. ES6模块中的值属于【动态只读引用】。
2. 对于只读来说，即不允许修改引入变量的值，import的变量是只读的，不论是基本数据类型还是复杂数据类型。当模块遇到import命令时，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。
3. 对于动态来说，原始值发生变化，import加载的值也会发生变化。不论是基本数据类型还是复杂数据类型。
4. 循环加载时，ES6模块是动态引用。只要两个模块之间存在某个引用，代码就能够执行。
5. 代码是在模块作用域之中运行，而不是在全局作用域运行。模块内部的顶层变量，外部不可见。
6. 模块脚本自动采用严格模式，不管有没有声明use strict。
7. 模块之中，可以使用import命令加载其他模块（.js后缀不可省略，需要提供绝对 URL 或相对 URL），也可以使用export命令输出对外接口。
8. 模块之中，顶层的this关键字返回undefined，而不是指向window。也就是说，在模块顶层使用this关键字，是无意义的。
9. 同一个模块如果加载多次，将只执行一次。

	export var firstName = 'Michael';
	export var lastName = 'Jackson';
	export var year = 1958;

export语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值。

export default命令用于指定模块的默认输出。显然，一个模块只能有一个默认输出，因此export default命令只能使用一次。所以，import命令后面才不用加大括号，因为只可能唯一对应export default命令。

使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。

	// main.js
	import {firstName, lastName, year} from './profile.js';
	
	function setName(element) {
	element.textContent = firstName + ' ' + lastName;
	}


