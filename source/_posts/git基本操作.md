title: git基本操作
date: 2016-03-24 12:20:18
tags:
- git 
---
接触git也有一段时间了，现在总结下git的使用知识点。如想详细学习git，请百度———— ［廖雪峰 git］ 第一个就是。
### git知识点：

#### 1. 如何上传一个项目

#### (再此之前我默认你已经配置好ssh密匙等)

1. 首先在git中新建一个仓库（名字不可以为中文）；
2. 在本地建立与之对应的一个仓库用于存储这个仓库的代码；
3. cd到本仓库的目录下；
4. git init （此步操作完成后，会生成一个隐藏的.git后缀文件） 
5. git add . (.是指添加整个工程，如需添加单个文件则只需要 git add test.js)
6. git commit －m"注释内容"
7. git remote add origin git@github.com:zjzno1/Demo.git (zjzno1是你的git名字，Demo是你新建的仓库的名字)
8. git push -u origin master (将项目推向git)

#### 2. 删除git一个项目（仓库）<font style="color: red">慎用！！！！！<font>
1. 在主页点击进入想要删除的仓库
2. 在仓库的上方点击settings
3. 将页面拖到最下面，点击Delete this repository
4. 在弹出框输入本仓库的名字，确认删除。

#### 3. git上clone一个项目到本地
1. git clone [ssh]

#### 4. 更新远程代码到本地
1. git remote -v 查看远程仓库
   git fetch origin master 从远程的origin仓库的master分支下载代码到本地的origin master
   git log -p master.. origin/master 比较本地的仓库和远程参考的区别

