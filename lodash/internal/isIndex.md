# isIndex

## lodash源码

```js
/** Used as references for various `Number` constants. */
const MAX_SAFE_INTEGER = 9007199254740991

/** Used to detect unsigned integer values. */
const reIsUint = /^(?:0|[1-9]\d*)$/

/**
 * Checks if `value` is a valid array-like index.
 *
 * @private
 * @param {*} value The value to check.
 * @param {number} [length=MAX_SAFE_INTEGER] The upper bounds of a valid index.
 * @returns {boolean} Returns `true` if `value` is a valid index, else `false`.
 */
function isIndex(value, length) {
  const type = typeof value
  length = length == null ? MAX_SAFE_INTEGER : length

  return !!length &&
    (type === 'number' ||
      (type !== 'symbol' && reIsUint.test(value))) &&
        (value > -1 && value % 1 == 0 && value < length)
}

export default isIndex
```

### 常量

```js
/** Used as references for various `Number` constants. */
const MAX_SAFE_INTEGER = 9007199254740991

/** Used to detect unsigned integer values. */
const reIsUint = /^(?:0|[1-9]\d*)$/
```

`reIsUint`用来匹配正整型数字。

### length值

```js
length = length == null ? MAX_SAFE_INTEGER : length
```

length如果为`undefined`或者为`null`时，`length`为最大安全数，否则为传入length。

### 处理类型及边界值

```js
(type === 'number' ||
      (type !== 'symbol' && reIsUint.test(value))) &&
        (value > -1 && value % 1 == 0 && value < length)
```

* number类型
* 不为`symbol`类型(如果是symbol类型，转为number类型会报错),并且使用正则匹配正整型数字。
* value大于`-1`且能被`1`整除,且value值小于`length`值

