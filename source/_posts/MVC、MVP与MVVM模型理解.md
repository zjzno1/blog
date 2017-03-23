title: MVC、MVP与MVVM模型理解
date: 2016-07-15 16:24:11
tags: 
- MVC
- MVP
- MVVM
- 模型
---
 早就听说过MVC,MCP,MVVM模型，但一直只知其一，不知其二。这几天终于找机会实力查了一波资料，好好的了解了一下，下面就聊一聊这三种模型，如有不对，欢迎大家指正。

 首先来说一下MVC框架，就是经典的Model，view，controller，最早提出于上世纪80年代。一般来说，Model提供数据，view是向用户展示的界面，而controller，以及用Model中的数据是Model和View之间联系的桥梁。一个简单的例子就是一般建设一个网站，数据库扮演的就是Model的角色，而后台扮演的就是controller的角色，前端扮演的是View角色。但是在前端中，MVC又该如何理解呢？

 下面来举一个例子：
 
	/**本实例来源于维基百科 */	
	/** 模型 Model, View, Controller */
	var M = {}, V = {}, C = {};

	/** Model 负责存放资料 */
	M.data = "hello world";

	/** View 负责将资料打印到屏幕上 */
	V.render = function (M) { alert(M.data); }

	/** Controller 作为一个M和V的桥梁 */
	C.handleOnload = function () { V.render(M); }

	/** 在网页读取的时候呼叫 Controller */
	window.onload = C.handleOnload;

 这就是一个前端的MVC实例

 那么MVP呢？即 Model View Presenter

 1. Model 定义使用者界面所需要被显示的资料模型，一个模型包含着相关的业务逻辑。
 2. View 视图为呈现使用者界面的终端，用以表现来自 Model 的资料，和使用者命令路由再经过 Presenter 对事件处理后的资料。
 3. Presenter 包含着元件的事件处理，负责检索 Model 取得资料，和将取得的资料经过格式转换与 View 进行沟通。
 
 那MVC与MVP之前又有什么不同呢？

在经典MVC中，一对controller-view捆绑起来表示一个ui组件，controller直接接受用户输入，并将输入转为相应命令来调用model的接口，对model的状态进行修改，最后通过观察者模式对view进行重新渲染。而MVP是修改controller-view的捆绑关系，为了解决controller-view的捆绑关系，将进行改造，使view不仅拥有UI组件的结构，还拥有处理用户事件的能力，这样就能将controller独立出来。为了对用户事件进行统一管理，view只负责将用户产生的事件传递给controller，由controller来统一处理，这样的好处是多个view可共用同一个controller。总结而言，即提升了controller的作用，把他从ui组件中提取出来，进而成为一个可以通用的逻辑处理程序。

MVVM —— Model-View-ViewModel

这个让我们来看一下下图：
![](https://raw.githubusercontent.com/zjzno1/img/master/mvvm.jpeg)

view和model是不知道彼此存在的，同MVP一样，将view和model清晰地分离开来。 其次，view是对viewmodel的外在显示，与viewmodel保持同步，viewmodel对象可以看作是view的上下文。view绑定到viewmodel的属性上，如果viewmodel中的属性值变化了，这些新值通过数据绑定会自动传递给view。反过来viewmodel会暴露model中的数据和特定状态给view。 所以，view不知道model的存在，viewmodel和model也觉察不到view。事实上，model也完全忽略viewmodel和view的存在。这是一个非常松散耦合的设计。













