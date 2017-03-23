title: css实现水平垂直居中
date: 2016-03-22 10:58:28
tags:
- css
- 水平竖直居中
---
##### 废话不多说，直接上代码

##### 父级元素position属性设置为 relative
	
	body {
		height:100%;
		width:100%;
	}
	div-one {
		position:relative;
		height:100px;
		width:100px;
	}

##### 子元素css
	div-one-content {
		position: absolute;
		height:100px;
		width:100px;
		background-color: #cbcb04;
		top: 50%;
		left: 50%;
		margin-left: -50px;
		margin-top: -50px;
	}

##### 这样子元素就在父元素中居中