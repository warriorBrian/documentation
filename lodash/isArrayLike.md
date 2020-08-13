# isArrayLike

> 检查 value 是否是类数组。 如果一个值被认为是类数组，那么它不是一个函数，并且value.length是个整数，大于等于 0，小于或等于 Number.MAX_SAFE_INTEGER。

## 用例

```js
_.isArrayLike([1, 2, 3]);
// => true
 
_.isArrayLike(document.body.children);
// => true
 
_.isArrayLike('abc');
// => true
 
_.isArrayLike(_.noop);
// => false
```

## lodash源码


### 依赖

```js
import isLength from './isLength.js'
```

[isLength 源码分析](lodash/isLength.md)

### 源码

```js
function isArrayLike(value) {
  return value != null && typeof value !== 'function' && isLength(value.length)
}

export default isArrayLike
```

lodash源码中，满足三个条件即为类数组：

* value不等于`undefined`、`null`
* value不等于`function`
* value.length通过isLength检测