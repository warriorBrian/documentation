# stubArray

> 这个方法返回一个新的空数组

## 用例

```js
var arrays = _.times(2, _.stubArray);
 
console.log(arrays);
// => [[], []]
 
console.log(arrays[0] === arrays[1]);
// => false
```

## lodash源码

```js
/**
 * This method returns a new empty array.
 *
 * @static
 * @memberOf _
 * @since 4.13.0
 * @category Util
 * @returns {Array} Returns the new empty array.
 * @example
 *
 * var arrays = _.times(2, _.stubArray);
 *
 * console.log(arrays);
 * // => [[], []]
 *
 * console.log(arrays[0] === arrays[1]);
 * // => false
 */
function stubArray() {
  return [];
}

export default stubArray;
```