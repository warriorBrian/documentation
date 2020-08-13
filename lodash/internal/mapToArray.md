# mapToArray

## 作用

将`Map`转换成数组

```js
const map = new Map([
 [1, 'aaa'],
 [2, 'bbb']
]) // {1 => 'aaa', 2 => 'bbb'}

mapToArray(map) // [ [1, 'aaa'], [2, 'bbb'] ]
```

## 源码

```js
/**
 * Converts `map` to its key-value pairs.
 *
 * @private
 * @param {Object} map The map to convert.
 * @returns {Array} Returns the key-value pairs.
 */
function mapToArray(map) {
  let index = -1
  const result = new Array(map.size)

  map.forEach((value, key) => {
    result[++index] = [key, value]
  })
  return result
}

export default mapToArray
```

首先初始化一个新的数组，长度为`map.size`

遍历`map`，将`[key, value]`存入result中并返回。