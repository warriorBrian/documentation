# isTypedArray

> 检查值是否是TypedArray

## 用例

```js
_.isTypedArray(new Uint8Array);
// => true
 
_.isTypedArray([]);
// => false
```

## lodash源码

### 依赖

```js
import getTag from './.internal/getTag.js'
import nodeTypes from './.internal/nodeTypes.js'
import isObjectLike from './isObjectLike.js'
```

### 源码

```js
/** Used to match `toStringTag` values of typed arrays. */
const reTypedTag = /^\[object (?:Float(?:32|64)|(?:Int|Uint)(?:8|16|32)|Uint8Clamped)Array\]$/

/* Node.js helper references. */
const nodeIsTypedArray = nodeTypes && nodeTypes.isTypedArray

/**
 * Checks if `value` is classified as a typed array.
 *
 * @since 3.0.0
 * @category Lang
 * @param {*} value The value to check.
 * @returns {boolean} Returns `true` if `value` is a typed array, else `false`.
 * @example
 *
 * isTypedArray(new Uint8Array)
 * // => true
 *
 * isTypedArray([])
 * // => false
 */
const isTypedArray = nodeIsTypedArray
  ? (value) => nodeIsTypedArray(value)
  : (value) => isObjectLike(value) && reTypedTag.test(getTag(value))

export default isTypedArray
```

## TypedArray

一个类型化数组(TypedArray)，对象描述了一个底层的二进制数据缓冲区的一个类数组视图，**事实上没有名为`TypedArray`的全局属性，也没有一个名为`TypedArray`的构造函数。**







































