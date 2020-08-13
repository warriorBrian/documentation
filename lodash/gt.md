# gt

> 检查 value是否大于 other。

## 用例

```js
_.gt(3, 1);
// => true
 
_.gt(3, 3);
// => false
 
_.gt(1, 3);
// => false
```

## lodash源码

```js
/**
 * Checks if `value` is greater than `other`.
 *
 * @since 3.9.0
 * @category Lang
 * @param {*} value The value to compare.
 * @param {*} other The other value to compare.
 * @returns {boolean} Returns `true` if `value` is greater than `other`,
 *  else `false`.
 * @see gte, lt, lte
 * @example
 *
 * gt(3, 1)
 * // => true
 *
 * gt(3, 3)
 * // => false
 *
 * gt(1, 3)
 * // => false
 */
function gt(value, other) {
  if (!(typeof value === 'string' && typeof other === 'string')) {
    value = +value
    other = +other
  }
  return value > other
}

export default gt
```

`gt`用来比较传入的`value`值是否比传入的`other`值大

在`value`和 `other`不同时为`string`类型的时候，都转换为数字进行比较。

如果`value`和`other`同时为`string`，则不进行转换，`>`操作符会逐个字符转换成`ascii`比较，直至比较出全部字符相等，或者第一个不相等的字符为止，这两个不相等的比较结果即为最终对比结果。




































