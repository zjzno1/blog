title: node相关试题
date: 2019-07-23 22:03:27
tags:
- node相关试题
---

#### 1. node什么时候内存溢出（泄露），怎么避免（解决）
原因：
在 Node 中，V8引擎有默认限制内存大小，通过 JavaScript 使用内存时只能使用部分内存（64位系统下约为1.4 GB，32位系统下约为0.7 GB），如果项目过于庞大，就会造成内存溢出。
解决方法：
（1）可以在Node启动的时候，传递--max-old-space-size或--max-new-space-size来调整内存大小的使用限制。

    node --max-old-space-size=1700 test.js // 单位为MB
    // 或者
    node --max-new-space-size=1024 test.js // 单位为KB

上述参数在V8初始化时生效，一旦生效就不能再动态改变。如果遇到 Node 无法分配足够内存给 JavaScript 的情况，可以用这个办法来放宽V8默认的内存限制

#### 2. node中间件（中间件是什么（定义），中间件原理是什么），为什么引入中间件，有没有写过或者使用过中间件，它解决了什么问题

##### 中间件定义（是什么）：
中间件就是请求req和响应res之间的一个应用，本质就是一个函数

详细描述：
请求浏览器向服务器发送一个请求后，服务器直接通过request定位属性的方式得到通过request携带过去的数据，就是用户输入的数据和浏览器本身的数据信息，这中间就一定有一个函数将这些数据分类做了处理，最后让`request（是不是response存疑）`对象调用使用，这个处理函数就是我们所所得中间插件

##### 中间件原理（app.use的原理）：
作用就是把我们用app.use注册的所有中间件和路由方法交给Router类来处理。

##### 中间件分类
应用级中间件 ()
路由级中间件 (router.use, router.get, router.post等)
错误处理中间件 ()
内置中间件 （app.static）
第三方中间件 

##### 写过（或者使用过）什么中间件，解决了什么问题
写过也用过一些中间件，例如最常用的路由级中间件，首先根据页面url的不同，走到了不同的路由中间件中；在单页面应用中，还解决了单页面应用刷新时使用history下的rewrites进行重定向的问题。
再比如其他中间件，还用到过解析cookie，记录日志等中间件
自己也写过设置缓存的中间件等

    res.setHeader("Expires", nowTime.toUTCString());
    res.setHeader("Cache-Control", "max-age=" + maxAge);

#### 3. node的event-loop（）

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


#### 4. express和koa的对比，各自的优缺点
1. 体积不同
Express较大而全，主要基于Connect中间件框架，功能丰富，随取随用，并且框架自身封装了大量便利的功能，比如路由、视图处理等等
koa体积更小，主要基于co中间件框架，框架自身并没集成太多功能，大部分功能需要用户自行require中间件去解决。

2. 中间件不同
（1） 调用方式不同
express是使用了callback进行回调，koa使用了ES6 generator特性，co框架会把所有generator的返回封装成为Promise对象
koa的中间件模式与express的是不一样的，koa是洋葱型，express是直线型`存疑`

#### 5. 洋葱模型

    const Koa = require('koa');
    const app = new Koa();

    // logger

    app.use(async (ctx, next) => {
        console.log(1);
        await next();
        console.log(2);
        const rt = ctx.response.get('X-Response-Time');
        console.log(`${ctx.method} ${ctx.url} - ${rt}`);
    });

    // x-response-time

    app.use(async (ctx, next) => {
        console.log(3);
        const start = Date.now();
        await next();
        console.log(4);
        const ms = Date.now() - start;
        ctx.set('X-Response-Time', `${ms}ms`);
    });

    // response

    app.use(async ctx => {
        console.log(5);
        ctx.body = 'Hello World';
    });

    app.listen(3000);  // 访问localhost:3000 得到 1 3 5 4 2

koa的洋葱模型，在遇到next的时候会把当前中间件压栈，执行下一个中间件，一直到没有next或者next为空，然后在一个个按照先进后出的原则出栈

#### 6. v8引擎相关原理与知识

#### 7. 有过哪些node的原生api，是怎么和php以及java系统交互的
fs、path、http(我们内部封装了h-request的npm包，在请求不同系统时，附带不同的参数)
#### 8. node的守护进程，（node集群是怎么管理的，怎么收集日志的）
node的守护进程
pm2 
node集群管理
上线代码会分别在线上node机器上全部上去，然后根据nginx做负载均衡，如果其中一台机器一直重启，在重启到一定次数后会终止重启，然后发邮件以及短信通知。
日志收集
从三个纬度收集日志
1. 首先用leo收集打到nginx的url，用来收集一些例如url，cookie，referrer等信息，已复现用户的操作路径
2. 在编写代码时，使用try chach或者if代码块，如果走入异常情况，发送sentry记录日志
3. node代码中，在异常情况下，同时可以记录更为详细的log在node工程的同级目录下
#### 9. node怎么上线（上线流程），怎么监控

#### 10. npm install后是怎么执行的
首先根据package.json的dependencies和devDependencies去下载引用的包放在package.json的同级目录node_modules下。如果你没有设置npm的源，那默认到npm的官方网址下载，如果有设置其他源，例如淘宝源或者公司内部源，那就会去设置的源去下载。
npm install -g 下载到全局
npm install --save 保存到dependencies
npm install --save-dev 保存到devDependencies

#### 11. node有哪些定时功能
setTimeout/clearTimeout, setInterval/clearInterval, setImmediate/clearImmediate, process.nextTick

#### 12.  fs.watch和fs.watchFile有什么区别，怎么应用?
二者主要用来监听文件变动．fs.watch利用操作系统原生机制来监听，可能不适用网络文件系统; fs.watchFile则是定期检查文件状态变更，适用于网络文件系统，但是相比fs.watch有些慢，因为不是实时机制．

#### 13. 实现一个简单的http服务器

    var http = require('http'); // 加载http模块
    http.createServer(function(req, res) {
        res.writeHead(200, {'Content-Type': 'text/html'}); // 200代表状态成功, 文档类型是给浏览器识别用的
        res.write('<meta charset="UTF-8"> <h1>我是标题啊！</h1> <font color="red">这么原生，初级的服务器，下辈子能用着吗?!</font>'); // 返回给客户端的html数据
        res.end(); // 结束输出流
    }).listen(3000); // 绑定3ooo, 查看效果请访问 http://localhost:3000

#### 14. child-process相关
1.  为什么需要child-process?
参考答案: node是异步非阻塞的，这对高并发非常有效．可是我们还有其它一些常用需求，比如和操作系统shell命令交互，调用可执行文件，创建子进程进行阻塞式访问或高CPU计算等，child-process就是为满足这些需求而生的．child-process顾名思义，就是把node阻塞的工作交给子进程去做．
2.  exec,execFile,spawn和fork都是做什么用的?
参考答案: exec可以用操作系统原生的方式执行各种命令，如管道 cat ab.txt | grep hello; execFile是执行一个文件; spawn是流式和操作系统进行交互; fork是两个node程序(javascript)之间时行交互.
3.  实现一个简单的命令行交互程序?
参考答案: 那就用spawn吧.

#### 15. 怎样充分利用多个CPU?
每个进程各使用一个CPU，，以此实现多核CPU的利用。Node提供了child_process模块，并且也提供了fork()方法来实现进程的复制(Node复制进程需要不小于10M的内存和不小于30ms的时间)。
解决方案就是Master-Worker模式（又称为主从模式），通过IPC通道实现主从进程间的通信，通信的目的是为了让不同的进程能够互相访问资源并进行协调工作


#### 16. 程序总是崩溃，怎样找出问题在哪里?
参考答案: 1) node --prof 查看哪些函数调用次数多 2) memwatch和heapdump获得内存快照进行对比，查找内存溢出

#### 17. 有哪些常用方法可以防止程序崩溃?
1) try-catch-finally 
2) EventEmitter/Stream error事件处理 
3) domain统一控制 
4) jshint静态检查 
5) jasmine/mocha进行单元测试

#### 18. 怎样调试node程序
node --debug app.js 和node-inspector

#### 19. typeScript的优点（具体举例）
两大特性：
1. 给JavaScript加上可选的类型系统，很多事情是只有静态类型才能做的，给JavaScript加上静态类型后，就能将调试从运行期提前到编码期，诸如类型检查、越界检查这样的功能才能真正发挥作用。TypeScript的开发体验远远超过以往纯JavaScript的开发体验，无需运行程序即可修复潜在bug。
2. 另一个特性是支持未来的ES 6甚至ES 7，最近的更新都与此有关。在TypeScript中，你可以直接使用ES 6的最新特性，在编译时它会自动编译到ES 3或ES 5。

优点细节浏览：
1. TS是一个应用程序级的JavaScript开发语言。
2. TS是JavaScript的超集，可以编译成纯JavaScript。
3. TS跨浏览器、跨操作系统、跨主机，开源。
4. TS始于JS，终于JS。遵循JavaScript的语法和语义，方便了无数的JavaScript开发者。
5. TS可以重用现有的JavaScript代码，调用流行的JavaScript库。
6. TS可以编译成简洁、简单的JavaScript代码，在任意浏览器、Node.js或任何兼容ES3的环境上运行。
7. TypeScript比JavaScript更具开发效率，包括：静态类型检查、基于符号的导航、语句自动完成、代码重构等。
8. TS提供了类、模块和接口，更易于构建组件。


#### 20. 介绍一下对nodejs的异步IO原理，以及内部线程池相关内容

#### 21. nodejs的进程维护有了解过么

#### 22. nodejs的0秒重载

#### 23. express运行流程与原理

#### 24. 模版引擎是怎么渲染到页面上的

#### 25. express中的路由规则

#### 26. node性能优化

#### 27. 说一下node里对Buffer数据类型的认识，对于初始化的Buffer，可以实现增加长度吗

