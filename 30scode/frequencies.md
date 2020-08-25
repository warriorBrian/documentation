# frequencies

> 计算数组中元素出现的次数，返回一个对象，key为元素值，value为次数

## Example

```js
frequencies(['a', 'b', 'a', 'c', 'a', 'a', 'b']); // { a: 4, b: 2, c: 1 }
```

## 实现


```js
const frequencies = arr =>
  arr.reduce((a, v) => {
    a[v] = a[v] ? a[v] + 1 : 1;
    return a;
  }, {});
```

使用`Array.prototype.reduce()`方法进行遍历，初始值为对象`{}`

将每个元素作为key

value为：`a[v]`存在情况下，次数`+1`，否则使用`1`

最后返回这个对象。