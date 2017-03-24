title: js中的call和apply
date: 2016-08-11 16:40:45
tags:
- js
- call
- apply
---
call 和 apply 都是为了改变某个函数运行时的 context 即上下文而存在的，换句话说，就是为了改变函数体内部 this 的指向。

obj.call(thisObj, arg1, arg2, ...);
obj.apply(thisObj, [arg1, arg2, ...]);

两者作用一致，都是把obj(即this)绑定到thisObj，这时候thisObj具备了obj的属性和方法。或者说thisObj『继承』了obj的属性和方法。

唯一区别是apply接受的是数组参数，call接受的是连续参数。所以当参数固定时可以使用call，当参数不固定时使用apply。

举个栗子：