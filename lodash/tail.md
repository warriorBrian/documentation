# tail

> 获取除了array数组第一个元素以外的全部元素。

## 用例

```js
_.tail([1, 2, 3]);
// => [2, 3]
```

## lodash源码

```js
function tail(array) {
  const length = array == null ? 0 : array.length
  if (!length) {
    return []
  }
  const [, ...result] = array
  return result
}

export default tail
```

首先判断`array`是否为`undefined`或者为`null`，如果是返回空数组

然后通过**数组解构**，使用`,`进行第一个元素占位，用**剩余运算符**获取除第一个元素以外的全部元素。