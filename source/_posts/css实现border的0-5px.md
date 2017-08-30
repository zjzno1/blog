title: css实现border的0.5px
date: 2017-08-30 15:20:49
tags:
- css
---
用css实现border的0.5px，有以下几种方式：

1.使用png图片，设置元素的background-image和background-size两个属性来实现。
2.使用png图片，设置border-image来实现。
3.在meta元素的viewport标签中，设置scale属性（h5.m.taobao.com使用该方法,要设置成手机模式才可以）。

但是使用这几种方式，各有各的劣势。

1.使用png的图片，不管是设置在background还是设置在border中，都有一个问题就是，这个元素没有办法设置圆角，当如果我需要改变这个边框的颜色时，需要重新设计图片，需求变更时不灵活。
2.在meta中设置scale属性，那么接下来的整个页面的实现，就变的更加困难，因为所有的地方，都要考虑到宽高，大小等，都会被scale属性影响的。

因此，在推荐用一下做法【transform:scale()方法】来实现0.5px：

	<!DOCTYPE html>
	<html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>Document</title>
		<style>
		.custom-border{
			float: left;
			margin-right: 10px;
		    width:200px;
		    height:100px;
		    border:1px solid #333;
		    background-color:#eee;
		    padding:10px;
		}
		.scale-border{
			float: left;
		    height:100px;
		    position:relative;
		    padding:10px;
		    width: 200px;
		}
		.border{
		    -webkit-transform:scale(0.5);
		    transform:scale(0.5);
		    position:absolute;
		    border:1px solid #333;
		    top:-50%;
		    right:-50%;
		    bottom:-50%;
		    left:-50%;
		    border-radius: 10px;
		    background-color:#eee;
		}
		.content{
		    position:relative;
		    z-index:2;
		}
		</style>
	</head>
	<body>
		<div class="custom-border">边框宽度1px</div>
		<div class="scale-border ">
		    <div class="content">边框宽度0.5px</div>
		    <div class="border"></div>
		</div>
	</body>
	</html>

如下图所示：

![](https://github.com/zjzno1/img/blob/master/0.5px.png?raw=true)





