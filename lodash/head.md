# head

> 获取数组array的第一个元素

## 用例

```js
_.head([1, 2, 3]);
// => 1
 
_.head([]);
// => undefined
```

## lodash源码

```js
function head(array) {
  return (array != null && array.length)
    ? array[0]
    : undefined
}

export default head
```

判断`array`不能等于`null`或者`undefined`，并且`array.length`必须大于`0`。