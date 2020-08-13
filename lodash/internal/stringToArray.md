# stringToArray

## 作用

将字符串转为数组

```js
stringToArray('123') // ['1', '2', '3']
```

## lodash 源码

### 依赖

```js
import asciiToArray from './asciiToArray.js'
import hasUnicode from './hasUnicode.js'
import unicodeToArray from './unicodeToArray.js'
```

[asciiToArray 分析](lodash/internal/asciiToArray.md)

[hasUnicode 分析](lodash/internal/hasUnicode.md)

[unicodeToArray 分析](lodash/internal/unicodeToArray.md)

### 源码

```js
/**
 * Converts `string` to an array.
 *
 * @private
 * @param {string} string The string to convert.
 * @returns {Array} Returns the converted array.
 */
function stringToArray(string) {
  return hasUnicode(string)
    ? unicodeToArray(string)
    : asciiToArray(string)
}

export default stringToArray
```

检测字符串是否包含`Unicode`，如果存在则使用`unicodeToArray`转为数组，否则使用`asciiToArray`转为数组。