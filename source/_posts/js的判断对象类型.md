title: js的判断对象类型
date: 2019-07-11 21:04:07
tags:
---
可以通过 Object.prototype.toString.call(xx)。这样我们就可以获得类似 [object Type] 的字符串。
instanceof 可以正确的判断对象的类型，因为内部机制是通过判断对象的原型链中是不是能找到类型的 prototype。

实现instanceof

    function instanceof(left, right) {
    // 获得类型的原型
    let prototype = right.prototype
    // 获得对象的原型
    left = left.__proto__
    // 判断对象的类型是否等于类型的原型
    while (true) {
    	if (left === null)
    		return false
    	if (prototype === left)
    		return true
    	left = left.__proto__
    }
}


