title: 关于nodejs的调试
date: 2016-09-05 10:44:49
tags:
- nodejs
- 调试
---

最近使用了nodejs写程序，但是之前调试都是在程序源码中打印console.log来查看变量或者代替断点，这样在每次修改完之后要重启服务，并且相对来说比较繁琐耗时，因此上网探索了一下nodejs的调试相关内容，把学到的东西整理一下。

因为项目是用express搭的，因此直接说怎么调试express（其实调试单个文件也同理）。

在搭建好node开发环境的前提下，首先要在全局安装node-inspector，
	
	npm install -g node-inspector

然后再安装supervisor（这是一个修改代码保存后自动刷新的插件，免去了每次修改代码后都要重新启动服务的烦恼，如果想了解详情，请自行百度（谷歌）supervisor^_^）

	sudo install supervisor
	//mac上加sudo，否则有时会出错（因为权限问题）

接下来就要正是进行nodejs的调试了

	supervisor --debug ./bin/www
	//在终端中的项目目录下输入这句话回车，监听程序启动，express也跑起来了

打开http://localhost:3000，就可以看到启动的express了。


再打开一个新的终端，cd到文件目录下，执行

	node-inspector &

这时出现一个地址，复制地址到chrome中打开，就可以看到类似chrome开发者工具的东西了，在这里，可以进行设置断点，查看变量等操作，完美调试nodejs程序。

over (^_^)