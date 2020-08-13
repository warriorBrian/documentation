# compact

> 创建一个新数组，包含原数组中所有的非假值元素。例如`false`, `null`, `0`, `""`, `undefined`, 和 `NaN` 都是被认为是“假值”。

## 用例

```js
compact([0, 1, false, 2, '', 3])

// => [1, 2, 3]
```

## lodash源码

```js
/**
 * Creates an array with all falsey values removed. The values `false`, `null`,
 * `0`, `""`, `undefined`, and `NaN` are falsey.
 *
 * @since 0.1.0
 * @category Array
 * @param {Array} array The array to compact.
 * @returns {Array} Returns the new array of filtered values.
 * @example
 *
 * compact([0, 1, false, 2, '', 3])
 * // => [1, 2, 3]
 */
function compact(array) {
  let resIndex = 0
  const result = []

  if (array == null) {
    return result
  }

  for (const value of array) {
    if (value) {
      result[resIndex++] = value
    }
  }
  return result
}

export default compact
```


首先判断传入数组是否为`null` 或者 `undefined`，则返回空数组

使用`for`进行遍历，利用隐式转换，如果为非假值则进行赋值，返回新的数组

## 30s code实现方式

```js
const compact = (array) => array.filter(Boolean)
```

使用`filter`进行值过滤，回调中传递`Boolean`方法，由js自带`Boolean`进行转换。

