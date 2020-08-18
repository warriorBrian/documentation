# nth

> 获取array数组的第n个元素。如果n为负数，则返回从数组结尾开始的第n个元素

## 用例

```js
var array = ['a', 'b', 'c', 'd'];
 
_.nth(array, 1);
// => 'b'
 
_.nth(array, -2);
// => 'c';
```

## lodash源码

### 依赖

```js
import isIndex from './.internal/isIndex.js'
```

[isIndex 分析](lodash/internal/isIndex.md)

### 源码

```js
function nth(array, n) {
  const length = array == null ? 0 : array.length
  if (!length) {
    return
  }
  n += n < 0 ? length : 0
  return isIndex(n, length) ? array[n] : undefined
}

export default nth
```

获取`array.length`长度，如果为`undefined`或者`null`则直接返回`undefined`

然后判断要获取的索引是否在 length 的范围内，如果在数组最大长度的范围内，则使用 `array[n]` 获取对应索引的值，否则返回 `undefined`。

可以看到 `nth` 的核心就是 `array[n]`，只不过它支持负数的索引，也对索引值的合法性做了校验。