title: js的引用、深拷贝与浅拷贝
date: 2017-08-29 16:34:37
tags:
- js
- 深拷贝/浅拷贝
---

这篇文章主要总结下什么是js的引用、深拷贝与浅拷贝。

要先理解什么是深拷贝和浅拷贝，就要先回顾一下js的基础知识。

### js的基本数据类型与引用类型（栈与堆）

#### 什么是栈与堆

栈（stack）是自动分配的内存空间，由系统自动释放；堆（heap）则是动态分配内存，大小不定也不会自动释放。

#### 基本数据类型与引用类型

js的基本数据类型：`number、string、boolean、null与undefined`，他们存放在栈中，JS基本数据类型的变量存放的是基本类型数据的实际值，而不是指针。
这里顺便讲下，存放在栈中的值(即js的基本数据类型)是不可改变的

	var a = '123'
	a[0] = 2
	console.log(a) // '123'

引用类型：对象（object）、数组（array）、函数（function），他们存放在堆中，引用数据类型的变量保存对它的引用，即指针。
举个例子

	var a = [1,2,3]
	var b = a
	console.log(b) // [1,2,3]
	b[0] = 2
	console.log(a) // [2,2,3]
	console.log(b) // [2,2,3]

可以看出，把数组a赋值给b，改变数组b的值，则a中的值也跟随改变。由此可以看出把a赋值给b，只是把a指向的指针赋值给了b，而并没有把值赋值给b。这就是js的引用。

##### 对于上面这种情况，如果我们想要一组和a一样的新数组，并且修改b并不影响a,那该怎么办呢？

##### 这时就可以用浅拷贝

	var a = [1,2,3]
	var b = []
	for(var i=0;i<a.length;i++)
	{
		b.push(a[i])
	}
	console.log(b) // [1,2,3]
	b[0] = 2
	console.log(a) // [1,2,3]
	console.log(b) // [2,2,3]

	//特别说明，由于引用类型比较是传地址，而这是a和b不在同一个地址中，所以 a!==b
	a === b //false

完美，我们得到了一个不改变原始变量的新数组！到这里，那深拷贝又有什么用呢？不急，往下看~

##### js的深拷贝

有一些时候引用类型不想上面那个简单==，比如

	var obj = {
		name: 'zjz',
		age: 24,
		likeNumber: [1,2,3]
	}

如果用浅拷贝是这么写：

	var newObj = {}
	for(var prop in obj){
		if(obj.hasOwnProperty(prop)){
			newObj[prop] = obj[prop]
		}
	}

这时我们得到一个新的对象newObj,
	
	console.log(newObj) 
	/* {
		name: 'zjz',
		age: 24,
		likeNumber: [1,2,3]
	}
	*/

这时改变newObj中的值

	newObj.name = 'zjz1'
	newObj.likeNumber[0] = '5'

	console.log(obj)
	/* {
		name: 'zjz',
		age: 24,
		likeNumber: [1,2,3]
	}
	*/
	console.log(newObj)
	/* {
		name: 'zjz1',
		age: 24,
		likeNumber: [5,2,3]
	}
	*/
可以看出，改变newObj的值，name属性在obj中确实没变，但是likeNumber却变了，这是怎么回事呢？

这是因为浅拷贝值赋值了一层对象的属性，并不包括对象里的引用类型数据，所以就会出现上面的改变newObj中的likeNumber而obj中的likeNumber跟随变得事情。

这种情况要怎么办呢？是时候让深拷贝登场啦\^o^/ 

什么是深拷贝？

深拷贝就是对对象以及对象的所有子对象进行拷贝，实现方法：

		var obj = {
		name: 'zjz',
		age: 24,
		likeNumber: [1,2,3]
	}
	var obj1 = {}
	//进行深拷贝操作的函数
	function inCopy(obj1,obj2) {
	    var obj1 = obj1 || {};//容错处理
	    for (var k in obj2) { 
	        if(obj2.hasOwnProperty(k)){ //只拷贝实例属性，不进行原型的拷贝
	            if(typeof obj2[k] == 'object') { //引用类型的数据单独处理
	                obj1[k] = Array.isArray(obj2[k])?[]:{};
	                inCopy(obj1[k],obj2[k]); //递归处理引用类型数据
	            }else{
	                obj1[k] = obj2[k]; //值类型的数据直接进行拷贝
	            }
	        }
	    }
	}

	inCopy(obj1,obj)
	obj1.likeNumber[0] = 5
	console.log(obj)
	/*
	{
		name: 'zjz',
		age: 24,
		likeNumber: [1,2,3]
	}
	*/
	console.log(obj1)
		/*
	{
		name: 'zjz',
		age: 24,
		likeNumber: [5,2,3]
	}
	*/

	



