# setToArray

## 作用

将`set`结构转为数组

## lodash 源码

```js
/**
 * Converts `set` to an array of its values.
 *
 * @private
 * @param {Object} set The set to convert.
 * @returns {Array} Returns the values.
 */
function setToArray(set) {
  let index = -1
  const result = new Array(set.size)

  set.forEach((value) => {
    result[++index] = value
  })
  return result
}

export default setToArray
```

与`mapToArray`同理，创建一个新的数组，长度为`set.size`

将`set`结构中遍历的值赋值给新的数组，并返回新数组