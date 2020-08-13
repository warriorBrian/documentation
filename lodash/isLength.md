# isLength

> 检查value是否为有效的类数组长度，是否为可用的`length`属性。

## 用例

```js
_.isLength(3);
// => true
 
_.isLength(Number.MIN_VALUE);
// => false
 
_.isLength(Infinity);
// => false
 
_.isLength('3');
// => false
```

## lodash源码

```js
/** Used as references for various `Number` constants. */
const MAX_SAFE_INTEGER = 9007199254740991

function isLength(value) {
  return typeof value === 'number' &&
    value > -1 && value % 1 == 0 && value <= MAX_SAFE_INTEGER
}

export default isLength
```

`typeof value === 'number'`, `length`属性必须为`number`类型。

`value > -1 && value % 1 == 0`，数组下标是从 `0` 开始的，因此可以用大于 `-1` 来判断，`value % 1`如果为正整数，则是为`0`，则条件合并起来为，`value`必须大于 `-1`的正整数。

`value <= MAX_SAFE_INTEGER`，`value`小于等于 最大的安全整数(Number.MAX_SAFE_INTEGER)