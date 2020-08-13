# asciiToArray

## 作用

将`ascii`(不包含`unicode`编码)的字符串转换成数组

## lodash 源码

```js
/**
 * Converts an ASCII `string` to an array.
 *
 * @private
 * @param {string} string The string to convert.
 * @returns {Array} Returns the converted array.
 */
function asciiToArray(string) {
  return string.split('')
}

export default asciiToArray
```

调用字符串的`split`方法，将每个字符串分割成数组。