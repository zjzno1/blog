title: js深拷贝的实现
date: 2019-07-11 00:06:19
tags:
---

第一种方法，使用`JSON.stringify`和`JSON.parse`实现

    let deepClone = function (obj) {
    let _tmp = JSON.stringify(obj);//将对象转换为json字符串形式
    let result = JSON.parse(_tmp);//将转换而来的字符串转换为原生js对象
    return result;
};

第二种方法，使用递归遍历对象实现

    function deepClone(obj) {
        let result = typeof  obj.splice === "function" ? [] : {};
        if (obj && typeof obj === 'object') {
            for (let key in obj) {
                if (obj[key] && typeof obj[key] === 'object') {
                    result[key] = deepClone(obj[key]);//如果对象的属性值为object的时候，递归调用deepClone,即在吧某个值对象复制一份到新的对象的对应值中。
                } else {
                    result[key] = obj[key];//如果对象的属性值不为object的时候，直接复制参数对象的每一个键值到新的对象对应的键值对中。
                }
            }
            return result;
        }
        return obj;
    }

