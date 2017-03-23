title: node中n的使用——版本控制
date: 2016-07-26 14:30:41
tags:
- node
- 版本控制
---
在node开发中，有时候会遇到这样一些情况：

一些工程要求低版本的node，而一些工程要求高版本的node，因此出来这样一个需求，那就是node的版本控制，要求在想要的时候可以切换到相应的node版本，且各个版本之间互不干扰。

基于这一需求，网上给出两种答案，一是用nvm进行node的版本控制管理，二是用n进行node的版本控制管理，在权衡完nvm与n的利弊之后，笔者选择了n作为node的版本控制工具。原因如下：

相比nvm，n更轻量，且n的操作更简单。但n也有弊端，那就是n是依赖于npm下的包，在想装n之前，要先装一个node环境。

安装n

	npm install -g n
安装指定的node版本

	n install <version>
选择指定的node版本

	n //这时出现了安装过的node的版本号，按上下键选择相应的版本，回车
	node -v //查看当前node版本号
删除指定的node版本

	n rm <version>

在n安装过程中遇到的一些问题：

安装n后选择node版本号失效。呃。。。对于这个问题。。笔者的解决方法是删除所有node环境重新安装，然后成功。初步估计是路径问题。

碰到 dyld:bad external relocation length Trace/BPT trap: 5

这个问题也困扰了我比较长的时间，最后看到overstackflow上有个兄弟给出了一个解决的方案，在终端中输入

	n latest 

将版本更新到最新，然后node -v就是最新的版本，然后把出问题的版本删除，成功解决。





