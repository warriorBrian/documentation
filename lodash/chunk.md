# chunk

> 将数组（array）拆分成多个 size 长度的区块，并将这些区块组成一个新数组。 如果array 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。

## 用例

```js
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]
 
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```
---
## lodash源码

```js
import slice from './slice.js'
import toInteger from './toInteger.js'

/**
 * Creates an array of elements split into groups the length of `size`.
 * If `array` can't be split evenly, the final chunk will be the remaining
 * elements.
 *
 * @since 3.0.0
 * @category Array
 * @param {Array} array The array to process.
 * @param {number} [size=1] The length of each chunk
 * @returns {Array} Returns the new array of chunks.
 * @example
 *
 * chunk(['a', 'b', 'c', 'd'], 2)
 * // => [['a', 'b'], ['c', 'd']]
 *
 * chunk(['a', 'b', 'c', 'd'], 3)
 * // => [['a', 'b', 'c'], ['d']]
 */
function chunk(array, size = 1) {
  size = Math.max(toInteger(size), 0)
  const length = array == null ? 0 : array.length
  if (!length || size < 1) {
    return []
  }
  let index = 0
  let resIndex = 0
  const result = new Array(Math.ceil(length / size))

  while (index < length) {
    result[resIndex++] = slice(array, index, (index += size))
  }
  return result
}

export default chunk
```
---

## 30s code实现方式

> 使用`Array.from()`创建一个新的数组，长度为 `arr.length / size`，从`from`回调用进行数组分割，每个数组的长度为`size`，**如果原始数组无法进行平均分割，则最后一块包含剩余元素。**

```js
// example
chunk([1, 2, 3, 4, 5], 2); // [[1,2],[3,4],[5]]
```

```js
const chunk = (arr, size) =>
  Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
    arr.slice(i * size, i * size + size)
  );
```

`Array.from()` 方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。

`chunk`方法接收两个参数，原始数组及size长度，使用`ceil`进行向上取整`(0.01 => 1)`,`from`方法第二个参数为回调，如果指定了该参数，新数组中的每个元素会执行该回调函数。

回调用使用`slice`方法进行分割，分割长度为(假设长度为5): 

第一次迭代:

* i * size = 0 * 2 => 0
* i * size + size = 0 + 2 => 2

slice(0, 2)

第二次迭代:

* i * size = 1 * 2 => 2
* i * size + size = 2 + 2 => 4

slice(2, 4)


第三次迭代:

* i * size = 2 * 2 => 4
* i * size + size = 4 + 2 => 6

slice(4, 6)

---

## 耗时

```js
[ [1,2],[3,4],[5] ]

// lodash: 3.56298828125ms

// from分割: 0.329833984375ms
```

随着分割的块数越小，数组长度增大，而执行耗时递增。





