title: 浏览器和node中的Eventloop
date: 2019-07-13 14:50:39
tags:
---
#### 浏览器中的Eventloop
JS 在执行的过程中会产生执行环境，这些执行环境会被顺序的加入到执行栈中。如果遇到异步的代码，会被挂起并加入到 Task（有多种 task） 队列中。一旦执行栈为空，Event Loop 就会从 Task 队列中拿出需要执行的代码并放入执行栈中执行，所以本质上来说 JS 中的异步还是同步行为。

setTimeout的第二个参数不得小于 4 毫秒，不足会自动增加

不同的任务源会被分配到不同的 Task 队列中，任务源可以分为 微任务（microtask） 和 宏任务（macrotask）。在 ES6 规范中，microtask 称为 jobs，macrotask 称为 task。

微任务包括 `process.nextTick ，promise ，Object.observe ，MutationObserver`
宏任务包括 `script ， setTimeout ，setInterval ，setImmediate ，I/O ，UI rendering`

很多人有个误区，认为微任务快于宏任务，其实是错误的。因为宏任务中包括了 script ，浏览器会先执行一个宏任务，接下来有异步代码的话就先执行微任务。

所以正确的一次 Event loop 顺序是这样的

执行同步代码，这属于宏任务
执行栈为空，查询是否有微任务需要执行
执行所有微任务
必要的话渲染 UI
然后开始下一轮 Event loop，执行宏任务中的异步代码

#### node中的Eventloop

Node 中的 Event loop 和浏览器中的不相同。

Node 的 Event loop 分为6个阶段，它们会按照顺序反复运行

   ┌───────────────────────┐
┌─>│        timers         │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     I/O callbacks     │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │     idle, prepare     │
│  └──────────┬────────────┘      ┌───────────────┐
│  ┌──────────┴────────────┐      │   incoming:   │
│  │         poll          │<──connections───     │
│  └──────────┬────────────┘      │   data, etc.  │
│  ┌──────────┴────────────┐      └───────────────┘
│  │        check          │
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
└──┤    close callbacks    │
   └───────────────────────┘

timer
timers 阶段会执行 setTimeout 和 setInterval
一个 timer 指定的时间并不是准确时间，而是在达到这个时间后尽快执行回调，可能会因为系统正在执行别的事务而延迟。
下限的时间有一个范围：[1, 2147483647] ，如果设定的时间不在这个范围，将被设置为1。
**I/O **
I/O 阶段会执行除了 close 事件，定时器和 setImmediate 的回调
idle, prepare
idle, prepare 阶段内部实现
poll
poll 阶段很重要，这一阶段中，系统会做两件事情

执行到点的定时器
执行 poll 队列中的事件

并且当 poll 中没有定时器的情况下，会发现以下两件事情

如果 poll 队列不为空，会遍历回调队列并同步执行，直到队列为空或者系统限制
如果 poll 队列为空，会有两件事发生

如果有 setImmediate 需要执行，poll 阶段会停止并且进入到 check 阶段执行 setImmediate
如果没有 setImmediate 需要执行，会等待回调被加入到队列中并立即执行回调



如果有别的定时器需要被执行，会回到 timer 阶段执行回调。
check
check 阶段执行 setImmediate
close callbacks
close callbacks 阶段执行 close 事件
并且在 Node 中，有些情况下的定时器执行顺序是随机的
setTimeout(() => {
    console.log('setTimeout');
}, 0);
setImmediate(() => {
    console.log('setImmediate');
})
// 这里可能会输出 setTimeout，setImmediate
// 可能也会相反的输出，这取决于性能
// 因为可能进入 event loop 用了不到 1 毫秒，这时候会执行 setImmediate
// 否则会执行 setTimeout
复制代码当然在这种情况下，执行顺序是相同的
var fs = require('fs')

fs.readFile(__filename, () => {
    setTimeout(() => {
        console.log('timeout');
    }, 0);
    setImmediate(() => {
        console.log('immediate');
    });
});
// 因为 readFile 的回调在 poll 中执行
// 发现有 setImmediate ，所以会立即跳到 check 阶段执行回调
// 再去 timer 阶段执行 setTimeout
// 所以以上输出一定是 setImmediate，setTimeout
复制代码上面介绍的都是 macrotask 的执行情况，microtask 会在以上每个阶段完成后立即执行。
setTimeout(()=>{
    console.log('timer1')

    Promise.resolve().then(function() {
        console.log('promise1')
    })
}, 0)

setTimeout(()=>{
    console.log('timer2')

    Promise.resolve().then(function() {
        console.log('promise2')
    })
}, 0)

// 以上代码在浏览器和 node 中打印情况是不同的
// 浏览器中一定打印 timer1, promise1, timer2, promise2
// node 中可能打印 timer1, timer2, promise1, promise2
// 也可能打印 timer1, promise1, timer2, promise2
复制代码Node 中的 process.nextTick 会先于其他 microtask 执行。
setTimeout(() => {
  console.log("timer1");

  Promise.resolve().then(function() {
    console.log("promise1");
  });
}, 0);

process.nextTick(() => {
  console.log("nextTick");
});
// nextTick, timer1, promise1
