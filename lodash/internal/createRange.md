# createRange

## 作用

`createRange`用来创建一个生成范围数组的函数，如果`fromRight`为`true`，所创建的函数生成的范围数组从大到小排序。

## lodash源码

### 依赖

```js
import baseRange from './baseRange.js'
import toFinite from '../toFinite.js'
```
[baseRange 分析](lodash/internal/baseRange.md)

[toFinite 分析](lodash/toFinite.md)

### 源码

```js
function createRange(fromRight) {
  return (start, end, step) => {
    // Ensure the sign of `-0` is preserved.
    start = toFinite(start)
    if (end === undefined) {
      end = start
      start = 0
    } else {
      end = toFinite(end)
    }
    step = step === undefined ? (start < end ? 1 : -1) : toFinite(step)
    return baseRange(start, end, step, fromRight)
  }
}

export default createRange
```