title: js中高级相关问题
date: 2019-07-29 22:10:16
tags:
- js
---
#### 1. es6相比es5新增了那些东西（es6中你都用到了什么）
（常用）
扩展运算符...([1,2,3,4])
Destructuring Assignment （解构赋值）
Arrow Functions in（箭头函数）
Default Parameters（默认参数）
Template Literals（模板对象）
Promises
块作用域和构造let和const
Classes （类）in ES6
ES6 module
数组和对象新增的方法和属性

    // 对象新增的方法
    
    // 它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致
    Object.is()
    
    // Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。
    Object.assign()
    
    // 引入了Object.keys方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。
    Object.keys()
    
    // Object.values方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。
    Object.values()
    
    //  Object.entries()方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组
    
    const obj = { foo: 'bar', baz: 42 };
    Object.entries(obj)
    // [ ["foo", "bar"], ["baz", 42] ]
    
    
    //  Object.fromEntries() 该方法的主要目的，是将键值对的数据结构还原为对象，因此特别适合将 Map结构转为对象。Object.fromEntries()方法是Object.entries()的逆操作，用于将一个键值对数组转为对象。用于将一个键值对数组转为对象。该方法的一个用处是配合URLSearchParams对象，将查询字符串转为对象

    Object.fromEntries([
      ['foo', 'bar'],
      ['baz', 42]
    ])
    // { foo: "bar", baz: 42 }
    
    Object.fromEntries(new URLSearchParams('foo=bar&baz=qux'))
    // { foo: "bar", baz: "qux" }


    // 数组新增方法
    1.Array.from()方法:JSON数组格式转换
    let people={
        0:'zhangsan', 
        '1':24,     //key值必须是0,1,2......可以是数字或者字符串
        length:2    //必须有length这个特殊的属性
    };
    let trans=Array.from(people);//Array.from()方法
    console.log(trans); //['zhangsan',24]
    // 伪数组转化为数组
    var doms = document.querySelectorAll('p');
    var domsList = Array.from(doms);
    
    
    2.Array.of()方法：
    let arr =Array.of(3,4,5,'zhang','li');
    console.log(arr);  //[3, 4, 5, "zhang","li"]

    
    3.find( )实例方法:
    所谓的实例方法就是并不是以Array对象开始的，而是必须有一个已经存在的数组，然后使用的方法，这就是实例方法（不理解请看下边的代码）。这里的find方法是从数组中查找。在find方法中我们需要传入一个匿名函数，函数需要传入三个参数：

    value：表示当前查找的值。
    index：表示当前查找的数组索引。
    arr：表示当前数组。
    
    let arr=[1,2,3,4,5,6,7,8,9];
    console.log(arr.find(function(value,index,arr){
        return value > 5;
    })) 
    //输出6  注意:在函数中如果找到符合条件的数组元素就return，并停止查找 ,找不到的话就 返回的unde
    
    4. findIndex()实例方法
    let arr=[1,2,3,4,5,6,7,8,9];
    console.log(arr.findIndex(function(value,index,arr){
        return value > 5;
    })) 
    // 结果： 5 ,如果在数组中找不到该元素 则返回  -1
    
    5. includes() 方法 查看某个数组是否包含给定的值
    参数:
    第一个参数必选（待检查的给定值）
    第二个参数可选，表示搜索的起始位置，默认为0，负数表示倒数的位置
    
    [1, 2, 3].includes(2, 2);     // false
    [1, 2, 3].includes(4);     // false
    [1, 2, NaN].includes(NaN); // true
    
    返回值:Boolean 
    注意：和indexOf的区别，indexOf进行了运算符的强比对，会导致对NaN误判。
    
    [1, 2, 3].includes(2);     // true
    [1, 2, 3].includes(4);     // false
    [1, 2, NaN].includes(NaN); // true
    
    6. fill()函数，使用指定的元素替换原数组内容，会改变原来的数组。
    
    fill(value, start, end)
    
    value：替换值。
    start：替换起始位置（数组的下标），可以省略。
    end：替换结束位置（数组的下标），
    如果省略不写就默认为数组结束。有参数时为结束位置，但不替换该位置。如果结束位置大于数组的长度，那么默认也只替换到数组的实际长度结束位置。
    替换的区间为 [start,end) 。
    let oldArr1 = [];
    let oldArr2 = [1,2,3];
    let newArr1 = oldArr1.fill(6); //当为空数组时什么都不替换
    let newArr2 = oldArr2.fill(6);
    console.log(newArr1); // []
    console.log(newArr2); // [6, 6, 6]
    
    7.for..of数组索引:有时候开发中是需要数组的索引的，那我们可以使用下面的代码输出数组索引。
    
    var arr=[1,2,3,4,5];
    for(a of arr){
        console.log(a);
    }
    
    8.copyWithin()：
    选择数组的某个下标，从该位置开始复制数组元素，默认从0开始复制。也可以指定要复制的元素范围。
    
    arr.copyWithin(target, start, end)
    
    
    const arr = [1, 2, 3, 4, 5]
    console.log(arr.copyWithin(3))
     // [1,2,3,1,2] 从下标为3的元素开始，复制数组，所以4, 5被替换成1, 2
    const arr1 = [1, 2, 3, 4, 5]
    console.log(arr1.copyWithin(3, 1)) 
    // [1,2,3,2,3] 从下标为3的元素开始，复制数组，指定复制的第一个元素下标为1，所以4, 5被替换成2, 3
    const arr2 = [1, 2, 3, 4, 5]
    console.log(arr2.copyWithin(3, 1, 2)) 
    // [1,2,3,2,5] 从下标为3的元素开始，复制数组，指定复制的第一个元素下标为1，结束位置为2，所以4被替换成2
    
    9.实例方法values()，keys(), entries() 
    
    const arr = ['a', 'b', 'c'];
    for(let v of arr.values()) {
      console.log(v)
    }
    //'a' 'b' 'c'
    
    const arr = ['a', 'b', 'c'];
    for(let v of arr.keys()) {
      console.log(v)
    }
    // 0 1 2
    
    const arr = ['a', 'b', 'c'];
    for(let v of arr.entries()) {
      console.log(v)
    }
    // [0, 'a'] [1, 'b'] [2, 'c']
    
    
#### 2. 数组相关（从最新的开始写，那些方法改变了原数组，那些没有改变）
##### 改变原数组的方法
fill()---用新元素替换掉数组内的元素，可以指定替换下标范围。

    let oldArr2 = [1,2,3];
    let newArr1 = oldArr1.fill(6); //当为空数组时什么都不替换
    let newArr2 = oldArr2.fill(6);
    console.log(oldArr1, oldArr2)

copyWithin()---选择数组的某个下标，从该位置开始复制数组元素，默认从0开始复制。也可以指定要复制的元素范围。

    console.log(arr.copyWithin(3), arr)
    //  [1, 2, 3, 1, 2]  [1, 2, 3, 1, 2]

pop()---删除数组的最后一个元素并返回删除的元素。

    let popItem = arr.pop();
    console.log(popItem, arr)
    // 1  , [9, 2, 4, 5, 6]

push()---向数组的末尾添加一个或更多元素，并返回新的长度。

    let length = arr.push(22);
    console.log(length, arr)
    // 7 ,  [9, 2, 4, 5, 6, 1, 22]

shift()---删除并返回数组的第一个元素。

    let firstItem = arr.shift();
    console.log(firstItem, arr)
    // 9 , [2, 4, 5, 6, 1]

unshift()---向数组的开头添加一个或更多元素，并返回新的长度。

    let newLength = arr.unshift(100, 20);
    console.log(newLength, arr)
    // 8 [100, 20, 9, 2, 4, 5, 6, 1]

reverse()---反转数组的元素顺序。

    arr.reverse();
    console.log(arr)
    // [1, 6, 5, 4, 2, 9]

sort()---对数组的元素进行排序。

    let arr1 = arr.sort();
    console.log(arr1, arr)
    // [1, 2, 4, 5, 6, 9] 
    // [1, 2, 4, 5, 6, 9]

splice()---用于插入、删除或替换数组的元素。

    // splice(index,howmany,item1,.....,itemX)
    index	必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
    howmany	必需。要删除的项目数量。如果设置为 0，则不会删除项目。
    item1, ..., itemX	可选。向数组添加的新项目。

    let arr =[9,2,4,5,6,1];
    arr.splice(100, 0,123,1234)
    console.log(arr)
    // [9, 2, 4, 5, 6, 1, 123, 1234]

##### 不改变原数组的方法
includes()--- 判断数组中是否存在该元素，参数：查找的值、起始位置，可以替换 ES5 时代的 indexOf 判断方式。indexOf 判断元素是否为 NaN，会判断错误。

    a.includes(2);
    console.log(a)
    //  [1, 2, 3]
    
keys()---返回键值对的key

    let brr =  arr.keys();
    console.log(arr, brr);
    //  ["a", "b", "c"]  Array Iterator {}

values()--- 返回迭代器：返回键值对的value

    let brr =  arr.values();
    console.log(arr, brr);
    // ["a", "b", "c"] Array Iterator {}
entries()--- 返回迭代器：返回键值对

    let brr =  arr.entries();
    console.log(arr, brr);
    // ["a", "b", "c"] Array Iterator {}

find()---传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它，并且终止搜索。

    let arr = [1, "2", 3, 3, "2"]
    console.log(arr.find(n => typeof n === "number") , arr) 
    // 1 , [1, "2", 3, 3, "2"]

findIndex()--- 传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它的索引，并且终止搜索

    console.log(arr.findIndex(n => typeof n === "number") , arr)// 0  , [1, "2", 3, 3, "2"]

concat()---连接两个或更多的数组，并返回结果。

    let brr = ['foo', 'boo'];
    let crr = arr.concat(brr);
    console.log(crr)
    // [9, 2, 4, 5, 6, 1, "foo", "boo"]

every()---检测数组元素的每个元素是否都符合条件。

    let falg = arr.every((item, index)=>{
        return item > 4
    })
    console.log(falg);
    // false

some()---检测数组元素中是否有元素符合指定条件。

    let falg = arr.some((item, index)=>{
        return item > 4
    })
    console.log(falg);
    // true

filter()---检测数组元素，并返回符合条件所有元素的数组。

    let brr = arr.filter((item, index)=>{
        return item > 4
    })
    console.log(brr);
    //  [9, 5, 6]

indexOf()---搜索数组中的元素，并返回它所在的位置。

    let index = arr.indexOf(9);
    console.log(index);
    // 0

join()---把数组的所有元素放入一个字符串。

    let str = arr.join('-');
    console.log(str, arr);
    // 9-2-4-5-6-1  , [9, 2, 4, 5, 6, 1]

toString()---把数组转换为字符串，并返回结果。

    let str = arr.toString();
    console.log(str);
    // 9,2,4,5,6,1

lastIndexOf()---返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。

    let index = arr.lastIndexOf(9);
    console.log(index);
    // 0

map()---通过指定函数处理数组的每个元素，并返回处理后的数组。

    let brr = arr.map((item,index)=>{
        return {
            key: item,
            value: item+3
        }
    });
    console.log(brr);
    //  0: {key: 9, value: 12}
        1: {key: 2, value: 5}
        2: {key: 4, value: 7}
        3: {key: 5, value: 8}
        4: {key: 6, value: 9}
        5: {key: 1, value: 4}

slice(start,end)---选取数组的的一部分，并返回一个新数组。

    let brr = arr.slice(2,4);
    console.log(brr);
    // [4, 5]

valueOf()---返回数组对象的原始值。

    let brr = arr.valueOf();
    console.log(brr);
    // [9, 2, 4, 5, 6, 1]

#### 3. 对象相关（新增了那些方法，怎么使用（平常项目中使用过那些））

    // 对象新增的方法
    
    // 它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致
    Object.is()
    
    // Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。
    Object.assign()
    
    // 引入了Object.keys方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。
    Object.keys()
    
    // Object.values方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。
    Object.values()
    
    //  Object.entries()方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组
    
    const obj = { foo: 'bar', baz: 42 };
    Object.entries(obj)
    // [ ["foo", "bar"], ["baz", 42] ]
    
    
    //  Object.fromEntries() 该方法的主要目的，是将键值对的数据结构还原为对象，因此特别适合将 Map结构转为对象。Object.fromEntries()方法是Object.entries()的逆操作，用于将一个键值对数组转为对象。用于将一个键值对数组转为对象。该方法的一个用处是配合URLSearchParams对象，将查询字符串转为对象

    Object.fromEntries([
      ['foo', 'bar'],
      ['baz', 42]
    ])
    // { foo: "bar", baz: 42 }
    
    Object.fromEntries(new URLSearchParams('foo=bar&baz=qux'))
    // { foo: "bar", baz: "qux" }

#### 4. 字符串相关（新增了那些方法，怎么使用（平常项目中使用过那些））
indexOf()方法和lastIndexOf()方法能接收2个参数，第一个参数为要寻找的字符串，第二个为开始位置，如果不写开始位置，会在全局找，无论从哪个位置开始找，返回的都是第一次出现的位置的下标。

    console.log(str.indexOf('rf'));
    console.log(str.lastIndexOf('rf'));
    // 10
    // 10
    console.log(str.indexOf('rf', 2));
    console.log(str.lastIndexOf('rf', 5));
    // 10
    // 10

includes()方法---同样能接收2个参数，填写一个参数在全局找，填写第二个参数，则从填写的位置往后找。如果找到返回true，没找到返回false。

    console.log(str.includes('rf'));
    console.log(str.includes('rf', 20));
    // true  false

startsWith()方法---查询是否以什么什么开头，同样能接收2个参数，1个参数的话在全局找，2个参数的话则从填写的位置往后找，找到返回true，没找到返回false。

    console.log(str.startsWith('adf'));
    console.log(str.startsWith('rf', 10));
    console.log(str.startsWith('rf'));
    // true  true false

endsWith()方法---用法与第3个一样，如果填写第二个参数的话，则是从填写的位置往前找

    console.log(str.endsWith('zle'));
    console.log(str.endsWith('zl', 17));
    console.log(str.endsWith('rf'));
    // true true false

repeat() ---收一个Number类型的数据，返回一个新的字符串，表示将原字符串重复 n 次。

padStart()方法---用于头部补全，接收2个参数，第一个参数是补全后的字符串的最大长度，第二个是要补的字符串，返回的是补全后的字符串。如果原字符串长度大于第一个参数，则会返回原字符串。如果不写第二个参数，则会用空格替补。

    console.log(str.padStart(4, 'djw'));
    console.log(str.padStart(10));
    console.log(str.padStart(10, 'djw'));
    console.log(str.padStart(10, 'djwdjw'));
    // hello
    //     hello
    // djwdjhello
    // djwdjhello

padEnd()方法---用于尾部填充，用法与上面一样。

    console.log(str.padEnd(4, 'djw'));
    console.log(str.padEnd(10));
    console.log(str.padEnd(10, 'djw'));
    console.log(str.padEnd(10, 'djwdjw'));
    // hello
    // hello     
    // hellodjwdj
    // hellodjwdj

toLowerCase()---把字符串转为小写，返回新的字符串。

    var str1=str.toLowerCase();
    console.log(str); //Hello World
    console.log(str1); //hello world
toUpperCase()---串转为大写，返回新的字符串。

    var str1=str.toUpperCase();
    console.log(str); //hello world
    console.log(str1); //HELLO WORLD

charAt()---返回指定下标位置的字符。如果index不在0-str.length(不包含str.length)之间，返回空字符串。

    var str1=str.charAt(6);
    console.log(str1); // w
charCodeAt()---返回指定下标位置的字符的unicode编码,这个返回值是 0 - 65535 之间的整数。

    var str1=str.charCodeAt(1);
    var str2=str.charCodeAt(-2); //NaN
    console.log(str1); //101

slice(): 返回字符串中提取的子字符串。

    var str1=str.slice(2); //如果只有一个参数，则提取开始下标到结尾处的所有字符串
    var str2=str.slice(2,7); //两个参数，提取下标为2，到下标为7但不包含下标为7的字符串
    var str3=str.slice(-7,-2); //如果是负数，-1为字符串的最后一个字符。提取从下标-7开始到下标-2但不包含下标-2的字符串。前一个数要小于后一个数，否则返回空字符串
    
    console.log(str1); //llo World
    console.log(str2); //llo W
    console.log(str3); //o Wor
substring()---提取字符串中介于两个指定下标之间的字符。

    var str1=str.substring(2)
    var str2=str.substring(2,2);
    var str3=str.substring(2,7);
    console.log(str1); //llo World
    console.log(str2); //如果两个参数相等，返回长度为0的空串
    console.log(str3); //llo W

substr()---返回从指定下标开始指定长度的的子字符串

    var str1=str.substr(1)
    var str2=str.substr(1,3);
    var str3=str.substr(-3,2);
    console.log(str1); //ello World 
    console.log(str2); //ell
    console.log(str3); //rl

split()--- 把字符串分割成字符串数组。

    var string1="1:2:3:4:5";
    var str1=str.split("");//如果把空字符串 ("")用作分割符，那么字符串的每个字符之间都会被分割
    var str2=str.split(" "); //以空格为分隔符
    var str3=str.split("",4); //4指定返回数组的最大长度
    var str4=string1.split(":");
    console.log(str1); // ["A", "A", " ", "B", "B", " ", "C", "C", " ", "D", "D"]
    console.log(str2); //["AA" "BB" "CC" "DD"]
    console.log(str3); //["A", "A", " ", "B"]
    console.log(str4); // ["1", "2", "3", "4", "5"]

replace()---在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。

    var reg=/o/ig; //o为要替换的关键字，不能加引号，否则替换不生效，i忽略大小写，g表示全局查找。
    var str1=str.replace(reg,"**")
    console.log(str1); //hell** W**RLD

match(): 返回所有查找的关键字内容的数组。

    var reg=/to/ig;
    var str1=str.match(reg);
    console.log(str1); //["To", "to"]
    console.log(str.match("Hello")); //null


#### 5. 数组和对象相互转换，在那些情况下可以相互转换

Object.keys()

    let obj = {
        name: 'haha', 
        age: 20,
        showName:  function () {}
    }
    Object.keys(obj)   //['name','age','showName']
    
    // 组合用法
    let obj = {
        name: 'haha', 
        age: 20, 
    }
    
    Object.keys(obj).map((val, index)=>{
    　 return　obj[val] // 可以针对obj的不同属性做不同处理
    }) 

Object.values();

    let obj = {
        name: 'haha', 
        age: 20,
        showName:  function () {}
    }
    Object.values(obj)   //['haha','20', f]

Object.entries()

    console.log(Object.entries(obj)); // [ ['foo', 'bar'], ['baz', 42] ]

    const anObj = { 100: 'a', 2: 'b', 7: 'c' };
    console.log(Object.entries(anObj)); // [ ['2', 'b'], ['7', 'c'], ['100', 'a'] ]


    console.log(Object.entries('foo')); // [ ['0', 'f'], ['1', 'o'], ['2', 'o'] ]
    
    // 更优雅的遍历对象键值：
    const obj = { a: 5, b: 7, c: 9 };
    for (const [key, value] of Object.entries(obj)) {
      console.log(`${key} ${value}`); 
      // "a 5", "b 7", "c 9"
    }
    
    // 或者
    Object.entries(obj).forEach(([key, value]) => {
    console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
    });
    
Object.fromEntries()

    const obj = Object.fromEntries(arr);
    console.log(obj); // { 0: "a", 1: "b", 2: "c" }


#### 6. var，let，const 的区别，和实现原理

#### 7. 实现深拷贝

#### 8. 获取页面中的全部标签，并计算个数

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <div class="a">aa</div>
        <p class="b">asd</p>
        <p class="c">asd</p>
    </body>
    </html>
    <script>
    let elObj = {};
    let elTotal = document.getElementsByTagName('*');
    for(let i=0; i< elTotal.length; i++) {
        let lowerTag = elTotal[i].tagName.toLowerCase();
        if(elObj[lowerTag]){
            elObj[lowerTag]++
        } else {
            elObj[lowerTag] = 1;
        }
    }
    console.log(elObj);
    </script>

#### 9. 节流和防抖，原理以及实现
1.防抖

触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间

思路：

使用闭包，每次触发事件时都取消之前的延时调用方法

    function debounce(fn) {
      let timeout = null; // 创建一个标记用来存放定时器的返回值
      return function () {
        clearTimeout(timeout); // 每当用户输入的时候把前一个 setTimeout clear 掉
        timeout = setTimeout(() => { // 然后又创建一个新的 setTimeout, 这样就能保证输入字符后的 interval 间隔内如果还有字符输入的话，就不会执行 fn 函数
          fn.apply(this, arguments);
        }, 500);
      };
    }
    function sayHi() {
      console.log('防抖成功');
    }

    var inp = document.getElementById('inp');
    inp.addEventListener('input', debounce(sayHi)); // 防抖

2.节流

思路：

每次触发事件时都判断当前是否有等待执行的延时函数

    function throttle(fn) {
      let canRun = true; // 通过闭包保存一个标记
      return function () {
        if (!canRun) return; // 在函数开头判断标记是否为true，不为true则return
        canRun = false; // 立即设置为false
        setTimeout(() => { // 将外部传入的函数的执行放在setTimeout中
          fn.apply(this, arguments);
          // 最后在setTimeout执行完毕后再把标记设置为true(关键)表示可以执行下一次循环了。当定时器没有执行的时候标记永远是false，在开头被return掉
          canRun = true;
        }, 500);
      };
    }
    function sayHi(e) {
      console.log(e.target.innerWidth, e.target.innerHeight);
    }
    window.addEventListener('resize', throttle(sayHi));

#### 10. call，apply，bind的原理与实现
call,apply,bind的作用都是改变this的指向，不同的地方是call和apply是立即执行函数，而bind不是，call和apply的区别是入参不同，call是单个的入参，而apply是第二个参数是个数组，以数组形式入参

#### 11. promise的相关概念及实现

#### 12. 箭头函数中的this，箭头函数与function的区别

#### 13. 介绍一下set，map，weakSet和weakMap的区别

#### 14. settimeout , promise, async/await的区别

#### 15. async/await如何通过同步的方式实现异步

#### 16. js异步解决方案的发展历程及其优缺点（amd，cmd，commonjs，es6的module）

#### 17. for循环和foreach哪个执行效率更高，为什么

#### 18. js判断数字，字母，中文，符号并截取16位

#### 19. 手写实现js的多种继承方式

#### 20. 使用settimeout实现setinterval，有什么优点

#### 21. js闭包的概念，闭包的使用场景，以及闭包的优缺点

#### 22. js中this的指向

#### 23. js的原型链

#### 24. js的内存管理机制

#### 25. js的作用域与作用域链

#### 26. 什么是xss和csrf，并如何防止

#### 27. es6的class和构造函数的区别

#### 28. js中的变量提升（和函数提升）

#### 29. js的事件捕获和事件冒泡


#### 30. onclick和addeventListener（第三个参数）绑定同一个元素，那个先执行，那个后执行
根据初始化函数的注册顺序，从上往下执行。
如果是以下这样

    <button class="a">fdfasf</button>

    document.querySelector('.a').addEventListener('click', function (params) {
        console.log('addeventListener 冒泡');
    }, false);
    document.querySelector('.a').onclick = function () {
            console.log('onclick1');
        }
    document.querySelector('.a').addEventListener('click', function (params) {
        console.log('addeventListener 捕获');
    }, true);
    document.querySelector('.a').onclick = function () {
        console.log('onclick2');
    }
    // 打印 addeventListener 冒泡 onclick2  addeventListener 捕获

#### 31. 两个onclick事件，是执行第一个还是执行第二个
在js中写多个onclick事件绑定相同元素，只会触发最后一个绑定的事件。

#### 32. 怎么让函数只执行一次，addeventListener的第三个参数都有哪些
1. 设置标志位
2. 

#### 33. new一个对象的过程
1、创建一个空对象，并且 this 变量引用该对象，同时还继承了构造函数的原型。 
2、属性和方法被加入到 this 引用的对象中。
3、新创建的对象由 this 所引用，并且最后隐式的返回 this

#### 34. 如何判断一个js的变量是什么数据类型，有哪几种方式
type, instanceof, Object.prototype.toString.call();

type 只能判断 number，string，boolean，undefined，object和function，在es6中又新增了symbol，无法判断Array，object，和null（因为判断出来都是object）

在判断是否是数组的时候，可以用es6中新增的方法Array.isArray()，也可以用instanceof

instanceof的原理：
构造函数的prototype属性是否出现在对象的原型链中的任何位置

如果想精确判断是那种数据类型，建议使用`Object.prototype.toString.call()`

#### 35. js中如何防止一个对象被修改（删除，添加）
1. 不可扩展对象（不能再给对象添加属性和方法）

    Object.preventExtensions(person);//设置为防拓展对象
    Object.isExtensible(person);//用来确定对象是否可扩展。

2. 密封对象（不能删除属性和方法）

    Object.seal(person);//将对象密封
    Object.isSealed(person）; // 检测对象是否被密封

3. 冻结对象（不能修改属性和方法）

    Object.freeze(man); // 冻结对象
    Object.isFrozen(man); // 检测对象是否被冻结

4. 使用Object.defineProperty的writable

    var person = function() {
        this.name = 'a'
    }
    var p = new person();
    Object.defineProperty(p, 'name', {
        writable: false
    })
    p.name = 'b';
    console.log(p.name) // a

#### 36. 浏览器中的event-loop
JS 在执行的过程中会产生执行环境，这些执行环境会被顺序的加入到执行栈中。如果遇到异步的代码，会被挂起并加入到 Task（有多种 task） 队列中。一旦执行栈为空，Event Loop 就会从 Task 队列中拿出需要执行的代码并放入执行栈中执行，所以本质上来说 JS 中的异步还是同步行为。

setTimeout的第二个参数不得小于 4 毫秒，不足会自动增加

同的任务源会被分配到不同的 Task 队列中，任务源可以分为 微任务（microtask） 和 宏任务（macrotask）。在 ES6 规范中，microtask 称为 jobs，macrotask 称为 task。

微任务包括 `process.nextTick ，promise ，Object.observe ，MutationObserver`
宏任务包括 `script ， setTimeout ，setInterval ，setImmediate ，I/O ，UI rendering`

很多人有个误区，认为微任务快于宏任务，其实是错误的。因为宏任务中包括了 script ，浏览器会先执行一个宏任务，接下来有异步代码的话就先执行微任务。

所以正确的一次 Event loop 顺序是这样的

执行同步代码，这属于宏任务
执行栈为空，查询是否有微任务需要执行
执行所有微任务
必要的话渲染 UI
然后开始下一轮 Event loop，执行宏任务中的异步代码

#### 37. cookie，sessionStorage，localStorage和indexDB的使用场景和优缺点
cookie：key/value 一般大小4k，每次访问都要传送cookie给服务器，可以设置过期时间，和域名绑定
localstorage：key/value 一直存储于本地硬盘（浏览器中可以删除），一般数据最大5MB（各个浏览器不一样），和域名绑定
sessionStorage：key/value 关闭页面或浏览器后被清除，最大5MB，和域名绑定
indexDB：key/object 可以存储对象，浏览器中的数据库，异步，支持事务，和域名绑定，存储空间大

总结：
LocalStorage、SessionStorage和Cookie都是通过域名进行隔离的。

全局存储：LocalStorage、Cookie
自动参与HTTP通信：Cookie
实现不同tab保存不同的数据：SessionStorage
存储大量数据：IndexDB

应用：登录相关可以考虑使用Cookie。

#### 38. 什么是函数式编程，什么是纯函数
https://www.jianshu.com/p/01cbebd9655d

函数式编程：
通过最小化变化使得代码更易理解

纯函数定义：
对于相同的输入，永远得到相同的输出，它不依赖外部环境，也不会改变外部环境

#### 39. 如何优化递归（尾递归）
[尾调用和尾递归](https://juejin.im/post/5acdd7486fb9a028ca53547c)
递归
当一个函数在内部调用自身，就可以称为一个递归

    function foo () {
        foo();
    }

这里没有结束条件，是死递归，所以会报栈溢出错误的，写代码时千万注意给递归添加结束条件。

什么是尾递归
当一个函数尾调用自身，就叫做尾递归。

例子：
    function foo () {
        return foo();
    }

好处：
#### 40. 函数柯里化
是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术。
好处：
1. 参数复用
2. 提前确认
3. 延迟运行

curry的一些性能问题你只要知道下面四点就差不多了：

(1) 存取arguments对象通常要比存取命名参数要慢一点
(2) 一些老版本的浏览器在arguments.length的实现上是相当慢的
(3) 使用fn.apply( … ) 和 fn.call( … )通常比直接调用fn( … ) 稍微慢点
(4) 创建大量嵌套作用域和闭包函数会带来花销，无论是在内存还是速度上

例子： 

    // 实现一个add方法，使计算结果能够满足如下预期：
    add(1)(2)(3) = 6;
    add(1, 2, 3)(4) = 10;
    add(1)(2)(3)(4)(5) = 15;

    function add() {
        // 第一次执行时，定义一个数组专门用来存储所有的参数
        var _args = Array.prototype.slice.call(arguments);

        // 在内部声明一个函数，利用闭包的特性保存_args并收集所有的参数值
        var _adder = function() {
            _args.push(...arguments);
            return _adder;
        };

        // 利用toString隐式转换的特性，当最后执行时隐式转换，并计算最终的值返回
        _adder.toString = function () {
            return _args.reduce(function (a, b) {
                return a + b;
            });
        }
        return _adder;
    }

    add(1)(2)(3)                // 6
    add(1, 2, 3)(4)             // 10
    add(1)(2)(3)(4)(5)          // 15
    add(2, 6)(1)                // 9

#### 41. 函数的arguments，arguments中都有什么属性
作用：
用于储存调用函数时的所有实参（arguments数组的个数，取决于实参列表，与形参无关）
arguments.callee()是arguments的重要属性。表示arguments所在函数的引用地址

    function name() {
        console.log(arguments);
    }
    name(1,2,3)
    // 打印出
    arguments {
        0: 1
        1: 2
        2: 3
        callee: ƒ name()
        length: 3
        Symbol(Symbol.iterator): ƒ values()
        __proto__: Object
    }

#### 42. js的跨域通信
当域名不是同一协议，同一域名或者同一端口号，则会根据浏览器的默认安全策略会产生跨域的问题。
#### 43. js如何实现懒加载
原理:
每个图片的src会有一个get请求，我们把不能看到的图片src设置为相同的图片，这些图片发一次请求即可，设置属性data-src为真正的图片路径。当图片滚动到可视区，我们就用js把data-src 赋值给 src，简单的懒加载就可以实现了。

如何判断是否在可视区
##### 就是 图片的 offsetTop <  scrollTop + clientHeigth 即可

    offsetTop // 元素距离文档顶部的距离
    scrollTop // 滚动的距离
    clientHeigth // 窗口的高度

代码：

    let imgArr = document.querySelectorAll('img');
    let len = imgArr.length;
    window.onscroll = function () {
        let seeHeight = document.documentElement.clientHeight;
        console.log("seeHeight ="+seeHeight);
        let scrollTop =  document.body.scrollTop || document.documentElement.scrollTop;
        console.log("scrollTop ="+scrollTop);
        for(let i=0; i<len; i++){
            console.log(imgArr[i].offsetTop);
            if(imgArr[i].offsetTop < seeHeight + scrollTop){
                    if(imgArr[i].getAttribute('src')=='timg.jpg'){
                        imgArr[i].src = imgArr[i].getAttribute('data-src');
                    }
            }
        }
    }

优化：
1.在初始条件下，应该有图片显示，只要在加载完毕之后滚动之前执行图片的加载即可

2.函数节流，但我们在高频度的滚动时，每隔一段事件开始图片的渲染。实现原理是 加入一个开关变量, 控制每隔固定的一段时间,函数才可能被触发

优化后代码：

    let imgArr = document.querySelectorAll('img');
    let len = imgArr.length;
    let n = 0; //记录加载图片的位置，避免从第一张开始加载
    let canrun = true;
    let seeHeight = document.documentElement.clientHeight;
    console.log("seeHeight ="+seeHeight);

    lazyLoad();
    window.onscroll = function () {
        if(!canrun){
            return ;
        }
        canrun = false;
        setTimeout(function () {
            console.log('*****');
            lazyLoad();
            canrun= true;
        },1000);

    }

    function lazyLoad() {
        let scrollTop =  document.body.scrollTop || document.documentElement.scrollTop;
        console.log("scrollTop ="+scrollTop);
        for(let i=0; i<len; i++){
            console.log(imgArr[i].offsetTop);
            if(imgArr[i].offsetTop < seeHeight + scrollTop){
                if(imgArr[i].getAttribute('src')=='timg.jpg'){
                    imgArr[i].src = imgArr[i].getAttribute('data-src');
                }
                n = i+1;
                console.log("n="+n);
            }
        }
    }

#### 44. js对象转化为字符串的步骤，数组与对象的相互转化（存疑）
js对象转化为字符串的步骤：
首先调用toString方法，只有当toString不返回一个原始值的时候，才会调用valueOf()。toString方法但是基本上所有对象都返回字符串。所以对象到字符串形式的转换基本都是使用toString方法。
俩个方法都不返回原始值时，会抛出错误。

数组转对象：


#### 45. 什么是防御式编程
主要思想
子程序应该不因传入错误数据而被破坏，哪怕是由其他子程序产生的错误数据。

#### 46. 有没有写过npm包，怎么设计的，用什么模块化方式（commonjs，es6的module，ump等）

#### 47. js中有几种方法定义函数
1、使用function关键字定义函数 -- 具有优先级，优先将function关键字定义的函数优先执行

　　function  functionName(arg0, arg1 ,..., argN){
　　　　　　statements
　　}
　　函数的调用：functionName()

2、使用函数表达式的形式定义函数（即将匿名函数复制给变量）

 　　var  variable = function(arg0, arg1 ,..., argN){
　　　　statements
　　 }
　　console.log(typeof  variable);     //function
　　函数调用：variable();

3、使用new Function构造函数定义函数

　　var  variable = new Function('name','alert("hello,"+name)');      //最末尾的是函数体，其前面的都是参数
　　console.log(typeof  variable);     //function
　　函数调用：variable('world');

注意：

（1）使用fucntion关键字定义的函数，函数一旦声明，允许任意调用（在函数定义前、函数定义后、函数内部，可以在任意位置调用）
（2）使用函数表达式、new Function构造函数定义的函数，不能在函数定义前使用

#### 48. focus/blur与focusin/focusout的区别与联系
focus/blur不冒泡，focusin/focusout冒泡
focus/blur兼容性好，focusin/focusout在除FireFox外的浏览器下都保持良好兼容性，如需使用事件托管，可考虑在FireFox下使用事件捕获elem.addEventListener(‘focus’, handler, true)

#### 49. 用js实现千位分隔符

    function format (num) {
        var reg=/\d{1,3}(?=(\d{3})+$)/g; 
        return (num + '').replace(reg, '$&,');
    }

正则表达式 \d{1,3}(?=(\d{3})+$)  表示前面有1~3个数字，后面的至少由一组3个数字结尾。

?=表示正向引用，可以作为匹配的条件，但匹配到的内容不获取，并且作为下一次查询的开始。

 $& 表示与正则表达式相匹配的内容，具体的使用可以查看字符串replace()方法的

#### 50. ie和dom事件流区别

1. 事件流的区别 

IE采用冒泡型事件 Netscape使用捕获型事件 DOM使用先捕获后冒泡型事件 
示例： 

复制代码代码如下:

    <body> 
    <div> 
    <button>点击这里</button> 
    </div> 
    </body> 

冒泡型事件模型： button->div->body (IE事件流) 

捕获型事件模型： body->div->button (Netscape事件流) 

DOM事件模型： body->div->button->button->div->body (先捕获后冒泡) 

2. 事件侦听函数的区别 

IE使用: 

    [Object].attachEvent("name_of_event_handler", fnHandler); //绑定函数 
    [Object].detachEvent("name_of_event_handler", fnHandler); //移除绑定 

DOM使用： 

    [Object].addEventListener("name_of_event", fnHandler, bCapture); //绑定函数 
    [Object].removeEventListener("name_of_event", fnHandler, bCapture); //移除绑定 

bCapture参数用于设置事件绑定的阶段，true为捕获阶段，false为冒泡阶段。

#### 51. js怎么实现精确倒计时
http://www.xuanfengge.com/js-realizes-precise-countdown.html

#### 52. js的数组降纬
1. 使用flat

    [1, [2, [3]]].flat(Infinity) // 参数可以是数字，可以拉平传入数字的n+1层，不写默认两层，Infinity默认全部拉平

2. flatMap() 只能拉平二维数组

3. 使用递归

    let newArr = [];
    function flatArr (arr) {
        for(let i=0; i<arr.length; i++) {
            if(arr[i] instanceof Array) {
               flatArr(arr[i]);
            }else {
                newArr.push(arr[i]);
            }
        }
    }
4. 使用reduce

    const flattenDeep = (arr) => Array.isArray(arr)
    ? arr.reduce( (a, b) => [...a, ...flattenDeep(b)] , [])
    : [arr]
    flattenDeep([1, [[2], [3, [4]], 5]])

#### 53. script的标签上都有什么属性
type：表示编写代码使用的脚本语言的内容类型
src ：表示包含要执行代码的外部文件（带有src属性的元素中，不应该包含额外的js代码，如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略 。）
charset：设置字符集，例如utf-8等
defer：表示脚本可以延迟到文档全部被解析和显示之后再执行（defer脚本会在文档渲染完毕后，DOMContentLoaded事件调用前执行）
async： 表示应该立即下载脚本，但不应妨碍页面中的其他操作，比如下载其他资源或等待加载其他脚本。（async的执行，并不会按着script在页面中的顺序来执行，而是谁先加载完谁执行）

defer和async的区别：
  有了async属性，表示后续文档的加载和渲染与js脚本的加载和执行是并行进行的，即异步执行；
  有了defer属性，加载后续文档的过程和js脚本的加载(此时仅加载不执行)是并行进行的(异步)，js脚本的执行需要等到文档所有元素解析完成之后，DOMContentLoaded事件触发执行之前。

#### 54. jquery为什么可以一直链式调用
因为在每次使用完jquery的方法之后，都会返回一个当前的jquery对象，因此jquery可以一直链式调用

#### 55. 请简单实现一个下拉加载

#### 56. {}+[]与[]+{}分别返回什么，为什么

#### 57. addeventListener的第三个参数都可以是什么

#### 58. 什么是Cookie 隔离？（或者说：请求资源的时候不要让它带cookie怎么做）
如果静态文件都放在主域名下，那静态文件请求的时候都带有的cookie的数据提交给server的，非常浪费流量，所以不如隔离开。

因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，
这样可以降低请求头的大小，降低请求时间，从而达到降低整体请求延时的目的。

同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，
提高了webserver的http请求的解析速度。
