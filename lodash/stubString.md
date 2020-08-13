# stubString

> 这个方法返回一个空字符串

## 用例

```js
_.times(2, _.stubString);
// => ['', '']
```

## lodash源码

```js
/**
 * This method returns an empty string.
 *
 * @static
 * @memberOf _
 * @since 4.13.0
 * @category Util
 * @returns {string} Returns the empty string.
 * @example
 *
 * _.times(2, _.stubString);
 * // => ['', '']
 */
function stubString() {
  return '';
}

export default stubString;
```