# shuffle

> 创建一个被打乱值的集合。

## 用例

```js
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

## lodash 源码

### 依赖

```js
import copyArray from './.internal/copyArray.js'
```

[copyArray 分析](lodash/internal/copyArray.md)

### 源码

```js
function shuffle(array) {
  const length = array == null ? 0 : array.length
  if (!length) {
    return []
  }
  let index = -1
  const lastIndex = length - 1
  const result = copyArray(array)
  while (++index < length) {
    const rand = index + Math.floor(Math.random() * (lastIndex - index + 1))
    const value = result[rand]
    result[rand] = result[index]
    result[index] = value
  }
  return result
}

export default shuffle
```

首先判断`array`如果值为`null`或者`undefined`，则赋值为`0`

```js
if (!length) {
	return []
}
```

就是在判断，如果为以上值，则直接返回空数组。

定义`result`变量，深拷贝`array`值，防止改变原数组。








































