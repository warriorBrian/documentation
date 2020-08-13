# stubObject

> 这个方法返回一个空对象

## 用例

```js
var objects = _.times(2, _.stubObject);
 
console.log(objects);
// => [{}, {}]
 
console.log(objects[0] === objects[1]);
// => false
```

## lodash源码

```js
/**
 * This method returns a new empty object.
 *
 * @static
 * @memberOf _
 * @since 4.13.0
 * @category Util
 * @returns {Object} Returns the new empty object.
 * @example
 *
 * var objects = _.times(2, _.stubObject);
 *
 * console.log(objects);
 * // => [{}, {}]
 *
 * console.log(objects[0] === objects[1]);
 * // => false
 */
function stubObject() {
  return {};
}

export default stubObject;
```