# isObjectLike

> 检查 value 是否是 类对象。 如果一个值是类对象，那么它不应该是 null，而且 typeof 后的结果是 "object"。

## 用例

```js
_.isObjectLike({});
// => true
 
_.isObjectLike([1, 2, 3]);
// => true
 
_.isObjectLike(_.noop);
// => false
 
_.isObjectLike(null);
// => false
```

## lodash源码

```js
/**
 * Checks if `value` is object-like. A value is object-like if it's not `null`
 * and has a `typeof` result of "object".
 *
 * @since 4.0.0
 * @category Lang
 * @param {*} value The value to check.
 * @returns {boolean} Returns `true` if `value` is object-like, else `false`.
 * @example
 *
 * isObjectLike({})
 * // => true
 *
 * isObjectLike([1, 2, 3])
 * // => true
 *
 * isObjectLike(Function)
 * // => false
 *
 * isObjectLike(null)
 * // => false
 */
function isObjectLike(value) {
  return typeof value === 'object' && value !== null
}

export default isObjectLike

```

**使用`typeof`操作符，如果返回值为`object`，并且值不为`null`时，就认为是类似对象。**

关于`typeof`操作符，遵循以下规则返回:


|     类型     |                             结果                             |
| :----------: | :----------------------------------------------------------: |
|  Undefined   |                         'undefined'                          |
|     Null     |                           'object'                           |
|   Boolean    |                          'boolean'                           |
|    Number    |                           'number'                           |
|    String    |                           'string'                           |
|    Symbol    |                           'symbol'                           |
|   宿主对象   | 由宿主实现，但是不能为 `'undefined'`, `'boolean'`, `'number'` 和  `'string'` |
|   函数对象   |                          'function'                          |
| 任意其它对象 |                           'object'                           |


这里需要重点说一下`null`，也是`isObjectLike`的关键所在，使用`typeof`操作符时，`null`会返回`object`。

> [!warning]
> **MDN:**
>
> 在Javascript最初的实现中，Javascript中的值是有一个表示类型的标签和实际数据值表示的，对象的类型标签是0，**由于`null`代表的是空指针（大多数平台下值为 0x00），因此，null 的类型标签是 0，`typeof null` 也因此返回 `"object"`。**
>
> 曾经一个ECMAScript的修复提案（通过选择性加入的方式），但被拒绝了，该提案会导致`typeof null == 'null'`



## 参考

[mdn typeof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)




























