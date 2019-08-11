title: vue相关试题
date: 2019-07-23 21:34:13
tags:
- vue
---

#### 1. vue的生命周期及相关概念（哪个周期在干什么）

###### new vue()
创建vue实例
初始化event和lifecycle

###### beforeCreate
完成实例初始化，初始化非响应式变量
this指向创建的实例；
可以在这加个loading事件；
data computed watch methods上的方法和数据均不能访问

###### created
实例创建完成
完成数据(data props computed)的初始化 导入依赖项。
可访问data computed watch methods上的方法和数据
未挂载DOM,不能访问$el,$ref为空数组
可在这结束loading，还做一些初始化，实现函数自执行,
可以对data数据进行操作，可进行一些请求，请求不易过多，避免白屏时间太长。
若在此阶段进行的 DOM 操作一定要放在 Vue.nextTick() 的回调函数中

###### beforeMount
有了el,编译了template|/outerHTML
能找到对应的template,并编译成render函数

###### mounted
完成创建vm.$el，和双向绑定，
完成挂载DOM 和渲染;可在mounted钩子对挂载的dom进行操作
即有了DOM 且完成了双向绑定 可访问DOM节点,$ref
可在这发起后端请求，拿回数据，配合路由钩子做一些事情；
可对DOM 进行操作

###### beforeUpdate
数据更新之前
可在更新前访问现有的DOM,如手动移除添加的事件监听器；

###### updated
完成虚拟DOM的重新渲染和打补丁；
组件DOM 已完成更新；
可执行依赖的dom 操作
注意：不要在此函数中操作数据，会陷入死循环的。

###### beforeDistory
在执行app.$destroy()之前
可做一些删除提示，如：你确认删除XX吗？ 
可用于销毁定时器，解绑全局时间 销毁插件对象

###### destroyed
当前组件已被删除，销毁监听事件 组件 事件 子实例也被销毁
这时组件已经没有了，你无法操作里面的任何东西了。

##### 在`keep alive`组件中，还有一下两个周期

###### activated
在使用vue-router时有时需要使用<keep-alive></keep-alive>来缓存组件状态，这个时候created钩子就不会被重复调用了，
如果我们的子组件需要在每次加载的时候进行某些操作，可以使用activated钩子触发

###### deactivated
keep-alive 组件被移除时使用

#### 2. vue-model 怎么实现双向数据绑定
Vue数据双向绑定（即数据响应式），是利用了Object.defineProperty()这个方法重新定义了对象获取属性值get和设置属性值set的操作来实现的。
数据的双向绑定，首先要对数据进行劫持监听，所以我们需要设置一个监听器Observer，用来监听所有属性。如果属性发生变化了，就需要告诉订阅者Watcher看是否需要更新。因为订阅者是有很多个，所以需要有一个消息订阅器Dep来专门收集这些订阅者，然后在监听器Observer和订阅者Watcher之间进行统一管理的。还需要有一个指令解析器Compile，对每个节点元素进行扫描和解析，将相关指令对应初始化成一个订阅者Watcher，并替换模板数据或者绑定相应的函数，此时当订阅者Watcher接收到相应属性的变化，就会执行对应的更新函数，从而更新视图。

#### 3. 组件之间的通信(传值)有几种实现方式
1. 父组件向子组件传值props，子组件向父组件传值$emit
2. $emit/$on
3. vuex
4. $attrs/$listeners
5. provide/inject
6. $parent / $children与 ref

#### 4. vue和其他框架相比，有什么优缺点

#### 5. vue3.0（相关）和2.0比较，有什么优缺点
Evan You（尤雨溪）在2018年11月16日早上在 Vue Toronto 的主题演讲中预演了 Vue 3.0的新特性 。利用现代浏览器支持的新功能，Vue 3 将成为我们已经了解和喜爱的 Vue.js 强大的的改进版本。

大概可以分为：
1. 更快
2. 更小
3. 更易于维护
4. 更多的原生支持
5. 更易于开发使用

1、虚拟 DOM 重写，mounting和patching的速度提高100％
2、更多的编译时的提示来减少运行时的开销
3、组件快速路径+单个调用+子类型检测
- 跳过不必要的条件分支
- JS引擎更容易优化
4、优化插槽的生成
- 确保实例正确的跟踪依赖关系
- 避免不必要的父子组件重新渲染
5、静态树提升
- 跳过修补整棵树，从而降低渲染成本
- 即使多次出现也能正常工作
6、静态属性提升
- 跳过不会改变节点的修补过程，但是它的子组件会保持修补过程
7、内联的事件提升
- 避免因为不同的内联函数标识而导致的不必要的重新渲染
8、基于Proxy的观察者机制，全语言覆盖+更好的性能
- 目前vue使用的是Object.defineProperty 的 getter 和 setter
- 组件实例初始化的速度提高100％
- 使用Proxy节省以前一半的内存开销，加快速度，但是存在低浏览器版本的不兼容
- 为了继续支持 IE11，Vue 3 将发布一个支持旧观察者机制和新 Proxy 版本的构建

##### 更小
更友好的tree-shaking
新的core runtime 压缩后大概 10kb

##### 更加可维护
Flow -> TypeScript
包的解耦
编译器重写
    - 可插拔的架构
    - 提供更强大的IDE支持来作为基础设施

##### 提供更方便的原生支持
运行时内核也将与平台无关，使得 Vue 可以更容易地与任何平台（例如Web，iOS或Android）一起使用

##### 更方便的开发
暴露响应式的api

#### 6. vue里this的指向
在根组件中
this 指向  vue实例
this.$el 指向绑定的根元素

在子组件中
this  指向 Vue 子组件的实例
this.$el  指向 当前组件的DOM元素

#### 7. v-for的时候为什么要使用key，优缺点什么
vue和react都是采用diff算法来对比新旧虚拟节点，从而更新节点。在vue的diff函数中（建议先了解一下diff算法过程）。
在交叉对比中，当新节点跟旧节点头尾交叉对比没有结果时，会根据新节点的key去对比旧节点数组中的key，从而找到相应旧节点（这里对应的是一个key => index 的map映射）。如果没找到就认为是一个新增节点。而如果没有key，那么就会采用遍历查找的方式去找到对应的旧节点。一种一个map映射，另一种是遍历查找。相比而言。map映射的速度更快。

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性。理想的 key 值是每项都有唯一 id

key只在查找复用节点的时候起到了查找作用

key 的特殊属性主要用在 Vue 的虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes。如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试修复/再利用相同类型元素的算法。使用 key，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。


#### 8. vue的diff算法

#### 9. vue怎么更新的视图，视图怎么更新vue

#### 10. vue中的on可以监听多个事件嘛
可以。
vm.$on( event, callback )
用法：
监听当前实例上的自定义事件。事件可以由vm.$emit触发。回调函数会接收所有传入事件触发函数的额外参数。（$emit和$on必须在一个公共实例上才能触发）
#### 11. vuex相关，（action和mutations有什么区别）
mutations 同步更新store里的state
action 异步更新store里的state

#### 12. vue-router相关（vue-router的生命周期，动态加载，传值，实现原理，全局守卫 https://router.vuejs.org/zh/  https://blog.csdn.net/yelin042/article/details/79932606）

#### 13. keep-alive相关

#### 14. vue的渲染过程，vue组件的渲染过程

#### 15. vue中的data可以是个对象吗，为什么

#### 16. vue里的$this.nextTick();
nextTick 可以让我们在下次 DOM 更新循环结束之后执行延迟回调，用于获得更新后的 DOM。
在 Vue 2.4 之前都是使用的 microtasks，但是 microtasks 的优先级过高，在某些情况下可能会出现比事件冒泡更快的情况，但如果都使用 macrotasks 又可能会出现渲染的性能问题。所以在新版本中，会默认使用 microtasks，但在特殊情况下会使用 macrotasks，比如 v-on。
对于实现 macrotasks ，会先判断是否能使用 setImmediate ，不能的话降级为 MessageChannel ，以上都不行的话就使用 setTimeout

    if (typeof setImmediate !== 'undefined' && isNative(setImmediate)) {
        macroTimerFunc = () => {
            setImmediate(flushCallbacks)
        }
        } else if (
        typeof MessageChannel !== 'undefined' &&
        (isNative(MessageChannel) ||
            // PhantomJS
            MessageChannel.toString() === '[object MessageChannelConstructor]')
        ) {
        const channel = new MessageChannel()
        const port = channel.port2
        channel.port1.onmessage = flushCallbacks
        macroTimerFunc = () => {
            port.postMessage(1)
        }
        } else {
        /* istanbul ignore next */
        macroTimerFunc = () => {
            setTimeout(flushCallbacks, 0)
        }
    }

nextTick 同时也支持 Promise 的使用，会判断是否实现了 Promise

    export function nextTick(cb?: Function, ctx?: Object) {
        let _resolve
        // 将回调函数整合进一个数组中
        callbacks.push(() => {
            if (cb) {
            try {
                cb.call(ctx)
            } catch (e) {
                handleError(e, ctx, 'nextTick')
            }
            } else if (_resolve) {
            _resolve(ctx)
            }
        })
        if (!pending) {
            pending = true
            if (useMacroTask) {
            macroTimerFunc()
            } else {
            microTimerFunc()
            }
        }
        // 判断是否可以使用 Promise 
        // 可以的话给 _resolve 赋值
        // 这样回调函数就能以 promise 的方式调用
        if (!cb && typeof Promise !== 'undefined') {
            return new Promise(resolve => {
            _resolve = resolve
            })
        }
    }

[13道可以举一反三的Vue面试题](https://juejin.im/post/5d41eec26fb9a06ae439d29f?utm_source=gold_browser_extension#heading-16)