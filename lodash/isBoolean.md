# isBoolean

> 检查值是否是原始 boolean 类型或者对象。如果只是一个布尔值，那么返回true，否则返回false

## 用例

```js
_.isBoolean(false);
// => true
 
_.isBoolean(null);
// => false
```

## lodash源码

### 依赖

```js
import getTag from './.internal/getTag.js'
import isObjectLike from './isObjectLike.js'
```
[getTag 分析](lodash/internal/getTag.md)

[isObjectLike 分析](lodash/isObjectLike.md)

### 源码

```js
/**
 * Checks if `value` is classified as a boolean primitive or object.
 *
 * @since 0.1.0
 * @category Lang
 * @param {*} value The value to check.
 * @returns {boolean} Returns `true` if `value` is a boolean, else `false`.
 * @example
 *
 * isBoolean(false)
 * // => true
 *
 * isBoolean(null)
 * // => false
 */
function isBoolean(value) {
  return value === true || value === false ||
    (isObjectLike(value) && getTag(value) == '[object Boolean]')
}

export default isBoolean
```

用来判断是否为布尔值，在`JavaScript`也可以用`Boolean`构造函数来创建布尔值

```js
new Boolean() // false

new Boolean(true) // true

typeof new Boolean(true) // object
```

可以看得出，在获取类型时，使用`typeof Boolean`构造函数得到的是`object`类型

下面的代码是用来判断普通布尔值，如果为`true`或者是`false`则就是`boolean`类型

```js
value === true || value === false
```

**如果是类对象，并且使用`getTag`获取类型字符串，来对比为类对象时是否为`Boolean`构造函数**

```js
(isObjectLike(value) && getTag(value) == '[object Boolean]')
```