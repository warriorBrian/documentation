# times

```js
_.times(n, [iteratee=_.identity])
```

> 调用 iteratee n 次，每次调用返回的结果存入到数组中。 iteratee 调用入1个参数： (index)。
>
> 这个方法会返回一个数组。

## 用例

```js
_.times(3, String);
// => ['0', '1', '2']
 
 _.times(4, _.constant(0));
// => [0, 0, 0, 0]
```

## lodash源码

```js
/** Used as references for various `Number` constants. */
const MAX_SAFE_INTEGER = 9007199254740991

/** Used as references for the maximum length and index of an array. */
const MAX_ARRAY_LENGTH = 4294967295

function times(n, iteratee) {
  if (n < 1 || n > MAX_SAFE_INTEGER) {
    return []
  }
  let index = -1
  const length = Math.min(n, MAX_ARRAY_LENGTH)
  const result = new Array(length)
  while (++index < length) {
    result[index] = iteratee(index)
  }
  index = MAX_ARRAY_LENGTH
  n -= MAX_ARRAY_LENGTH
  while (++index < n) {
    iteratee(index)
  }
  return result
}

export default times
```
#### 处理边界值

```js
if (n < 1 || n > MAX_SAFE_INTEGER) {
  return []
}
```

处理边界，当`n`小于1或者大于最大安全数，直接返回空数组。

#### 按计数调用函数

```js
let index = -1
const length = Math.min(n, MAX_ARRAY_LENGTH)
const result = new Array(length)
while (++index < length) {
  result[index] = iteratee(index)
}
```

开始计数调用方法，首先对比值，赋值给`length`，创建新数组。

遍历计数，将`iteratee`返回值赋值给`result`数组对应索引中。

---
#### 不会进入的循环

```js
index = MAX_ARRAY_LENGTH
n -= MAX_ARRAY_LENGTH
while (++index < n) {
  iteratee(index)
}
```

但是在上面，函数已经调用完毕，没有进入`while`中，但是`index`实质性被改变。

此时:

`index = 4294967295`

`n = -4294967295`

在正常情况，`index(4294967296)`不可能小于`n(-4294967295)`

而在上面已经处理了边界值的情况，这里显然不会被调用。

