# mapObject

> 将数组的值映射到对象，其中键-值对由原始值作为键，而回调函数的结果作为值。

## Example

```js
mapObject([1, 2, 3], a => a * a); // { 1: 1, 2: 4, 3: 9 }
```

## 实现

```js
const mapObject = (arr, fn) =>
  arr.reduce((acc, el, i) => {
    acc[el] = fn(el, i, arr);
    return acc;
  }, {});
```

使用 `Array.prototype.reduce()`方法进行遍历，`reduce`返回一个对象`{}`

使用`el`作为对象中每个键(`key`)属性，将`fn`(回调)最为值进行赋值，**当存在重复值，会存在覆盖情况**。