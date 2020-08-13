# stubFalse

> 这个方法返回 false

## 用例

```js
_.times(2, _.stubFalse);
// => [false, false]
```

## lodash源码

```js
/**
 * This method returns `false`.
 *
 * @static
 * @memberOf _
 * @since 4.13.0
 * @category Util
 * @returns {boolean} Returns `false`.
 * @example
 *
 * _.times(2, _.stubFalse);
 * // => [false, false]
 */
function stubFalse() {
  return false;
}

export default stubFalse;
```