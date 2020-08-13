# studTrue

> 这个方法返回 true

## 用例

```js
_.times(2, _.stubTrue);
// => [true, true]
```

## lodash源码

```js
/**
 * This method returns `true`.
 *
 * @static
 * @memberOf _
 * @since 4.13.0
 * @category Util
 * @returns {boolean} Returns `true`.
 * @example
 *
 * _.times(2, _.stubTrue);
 * // => [true, true]
 */
function stubTrue() {
  return true;
}

export default stubTrue;
```