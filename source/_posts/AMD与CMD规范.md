title: AMD与CMD规范
date: 2016-12-13 09:45:41
tags:
- 规范
---

AMD 是 RequireJS 在推广过程中对模块定义的规范化产出。
CMD 是 SeaJS 在推广过程中对模块定义的规范化产出。

AMD规范其实只有一个主要接口 define(id,dependencies,factory)，它要在声明模块的时候指定所有的依赖dependencies，并且还要当做形参传到factory中，对于依赖的模块提前执行，依赖前置

第一个参数 id 为字符串类型，表示了模块标识，为可选参数。若不存在则模块标识应该默认定义为在加载器中被请求脚本的标识。如果存在，那么模块标识必须为顶层的或者一个绝对的标识。
第二个参数，dependencies ，是一个当前模块依赖的，已被模块定义的模块标识的数组字面量。
第三个参数，factory，是一个需要进行实例化的函数或者一个对象。

	define("module", ["dep1", "dep2"], function(d1, d2) {
	  return someExportedValue;
	});
	require(["module", "../file"], function(module, file) { /* ... */ });

优点：
适合在浏览器环境异步加载
并行加载多个模块
缺点：
提高开发成本，代码阅读和书写比较困难
不符合通用的模块思维方式，是一种妥协的实现

在CMD中，一个模块就是一个文件，格式为：
    define( factory );
    全局函数define，用来定义模块。
    参数 factory  可以是一个函数，也可以为对象或者字符串。
    当 factory 为对象、字符串时，表示模块的接口就是该对象、字符串。

	define(function(require, exports, module) {
	  var $ = require('jquery');
	  var Spinning = require('./spinning');
	  exports.doSomething = ...
	  module.exports = ...
	})

优点：

依赖就近，延迟执行
很容易在node中运行
缺点：
依赖SPM打包，模块的加载逻辑偏重
实现： SeaJS