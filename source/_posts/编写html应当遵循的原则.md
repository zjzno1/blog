title: 编写html应当遵循的原则
date: 2016-03-12 19:36:14
tags: 
 - 文章
 - html
---
#### 以下是bootsharp给出的h5标准，很有参考意义，可以推荐下
1. 用两个空格符代替tab
2. 嵌套元素应当进行缩进（即两空格）
3. 对于属性的定义，用双引号
4. 不要自闭合
5. 不可省略结束标签
6. 为每个HTML页面第一行添加标准模式<!DOCTYPE html>
7. 语言属性<html lang="zh-cn">
8. IE兼容模式<meta http-equiv="X-UA-Compatible" content="IE=Edge">
9. 字符编码<meta charset="utf-8">
10. 引入css和js文件<link rel="stylesheet" href="code-guide.css">
                  <script src="code-guide.js"></script>
11. 尽量减少标签并保持最小的时间复杂度
12. 属性顺序  
			class
            id , nmae
            data-*
            src , for , type , href
            title , alt
            aria-* , role
13. 布尔boolean属性不用赋值
14. 避免JavaScript生成的标签

##### h5标准实例

![](http://ww1.sinaimg.cn/large/a5152f55gw1ew1s25ouiej20dv076jt8.jpg) 

##### 另外我的一些感悟
- 编写html时应当符合语义化，即对html的编写符合人类和浏览器的阅读习惯
- 编写html时一定要注意文档流，注意清除浮动，不要破坏文档流
- 尽量减少标签的使用

##### 以上