title: js的数组与数组降纬
date: 2019-07-13 17:20:47
tags:
---
数组的方法



#### 数组降纬

二位数组降纬

    [1, [2], 3].flatMap((v) => v + 1)
    // -> [2, 3, 4]

多维数组降纬

    const flattenDeep = (arr) => Array.isArray(arr)
  ? arr.reduce( (a, b) => [...a, ...flattenDeep(b)] , [])
  : [arr]

    flattenDeep([1, [[2], [3, [4]], 5]])

