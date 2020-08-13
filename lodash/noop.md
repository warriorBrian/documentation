# noop

> 这个方法返回undefined

## 用例

```js
_.times(2, _.noop);
// => [undefined, undefined]
```

## lodash源码

```js
/**
 * This method returns `undefined`.
 *
 * @static
 * @memberOf _
 * @since 2.3.0
 * @category Util
 * @example
 *
 * _.times(2, _.noop);
 * // => [undefined, undefined]
 */
function noop() {
  // No operation performed.
}

export default noop;
```