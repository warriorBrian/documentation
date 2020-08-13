# getTag

## 作用

获取`value`中的类型字符串，使用`Object.prototype.toString.call`方法

## 源码

```js
const toString = Object.prototype.toString

/**
 * Gets the `toStringTag` of `value`.
 *
 * @private
 * @param {*} value The value to query.
 * @returns {string} Returns the `toStringTag`.
 */
function getTag(value) {
  if (value == null) {
    return value === undefined ? '[object Undefined]' : '[object Null]'
  }
  return toString.call(value)
}

export default getTag
```

lodash不在需要使用`baseGetTag`，而[用方法 getTag 替换 baseGetTag实现 #4115](https://github.com/lodash/lodash/pull/4115)

如果`value`等于 `undefined` 、`null`,则返回自定义类型字符串，与`toString.call()`相同

**因此可以直接只用`Object.prototype.toString.call()`方法来返回类型字符串。**

因为在`getTag`方法中除了判断`undefined`、`null`以外，直接返回了`Object.prototype.toString.call()`的类型字符串。

## 参考

[MDN: Object.prototype.toSting](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)