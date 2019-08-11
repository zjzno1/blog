title: 'es7,es8,es9,es10新特性'
date: 2019-07-18 09:33:10
tags: 
- es
- 新特性
---

## es7的新特性：

### 新增特性：
Array.prototype.includes() 
**

### 1) Array.prototype.includes() 
用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

#### 参数
接收两个参数

1.要搜索的值
2.搜索的开始索引
#### 与indexof的区别
1.返回值不同，indexof返回是值型的，includes返回值是布尔型的
2.NaN的判断，如果数组中有NaN，indexof无法判断出来，但是includes可以
3.当数组的有空的值的时候，includes会认为空的值是undefined，而indexOf不会

### 2) ** 求幂运算符
可以使用**来替代Math.pow。

    4 ** 3  // 64
    Math.pow(4,3) // 64

但是，**还支持以下操作

    let n = 4;
    n **= 3;
    // 64

## es8 新特性

主要新功能：

### 新增特性

#### 主要特性

异步函数 Async Functions
共享内存和Atomics

#### 次要特性

Object.values / Object.entries
String padding
Object.getOwnPropertyDescriptors() 
函数参数列表和调用中的尾逗号


## es9 新特性

### 新增特性

#### 主要特性

异步迭代
Rest/Spread 属性

#### 新的正则表达式功能

RegExp named capture groups
RegExp Unicode Property Escapes
RegExp Lookbehind Assertions
s (dotAll) flag for regular expressions

#### 其他新功能

Promise.prototype.finally() 
模板字符串修改