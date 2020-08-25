# groupBy

> 根据给定的回调函数，进行元素分组。

## Example

```js
groupBy([6.1, 4.2, 6.3], Math.floor); // {4: [4.2], 6: [6.1, 6.3]}
groupBy(['one', 'two', 'three'], 'length'); // {3: ['one', 'two'], 5: ['three']}
```

## 实现

```js
const groupBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val, i) => {
    acc[val] = (acc[val] || []).concat(arr[i]);
    return acc;
  }, {});
```

首先使用`Array.prototype.map()`进行处理，`map`会返回一个数组，数组是处理之后的值。

`typeof fn === 'function' ? fn : val => val[fn]`这里判断是一个方法还是字符串，如果为一个方法，则直接使用回调方法。

然后使用`Array.prototype.reduce()`进行遍历，`reduce`提供初始值为空的对象`{}`。

在`reduce`中，每个对象中的`key`对应的是在`map`中处理之后的值，而`value`是一个数组，这个数组会以合并追加(`concat`)的形式进行加入。