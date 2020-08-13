# toFinite

> 转换值为一个有限数字

## 用例

```js
_.toFinite(3.2);
// => 3.2
 
_.toFinite(Number.MIN_VALUE);
// => 5e-324
 
_.toFinite(Infinity);
// => 1.7976931348623157e+308
 
_.toFinite('3.2');
// => 3.2
```

## lodash源码

### 依赖

```js
import toNumber from './toNumber.js'
```

[toNumber 分析](lodash/toNumber.md)

### 源码

```js
/** Used as references for various `Number` constants. */
const INFINITY = 1 / 0
const MAX_INTEGER = 1.7976931348623157e+308

function toFinite(value) {
  if (!value) {
    return value === 0 ? value : 0
  }
  value = toNumber(value)
  if (value === INFINITY || value === -INFINITY) {
    const sign = (value < 0 ? -1 : 1)
    return sign * MAX_INTEGER
  }
  return value === value ? value : 0
}

export default toFinite

```