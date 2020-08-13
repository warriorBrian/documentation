# defaultTo

> _.defaultTo(value, defaultValue)
>
>检查value，以确定一个默认值是否应被返回，如果value为NaN, null或者undefined，那么返回defaultValue默认值

## 用例

```js
_.defaultTo(1, 10);
// => 1
 
_.defaultTo(undefined, 10);
// => 10
```

## lodash源码

```js
/**
 * Checks `value` to determine whether a default value should be returned in
 * its place. The `defaultValue` is returned if `value` is `NaN`, `null`,
 * or `undefined`.
 *
 * @since 4.14.0
 * @category Util
 * @param {*} value The value to check.
 * @param {*} defaultValue The default value.
 * @returns {*} Returns the resolved value.
 * @example
 *
 * defaultTo(1, 10)
 * // => 1
 *
 * defaultTo(undefined, 10)
 * // => 10
 */
function defaultTo(value, defaultValue) {
  return (value == null || value !== value) ? defaultValue : value
}

export default defaultTo
```

首先`value == null`判断是否为`null`或者`undefined`， `value !== value`判断是否为NaN (自身不等于自身)

如果为以上情况，就实用默认值`defaultValue`，否则使用传入值`value`