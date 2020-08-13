# iteratorToArray

## 作用

将遍历器转换为数组

```js
let arr = ['a', 'b', 'c'];
let iter = arr[Symbol.iterator]();

iter.next() // { value: 'a', done: false }
iter.next() // { value: 'b', done: false }
iter.next() // { value: 'c', done: false }
iter.next() // { value: undefined, done: true }
```

上面代码中，变量`arr`是一个数组，原生就具有遍历器接口，部署在`arr`的`Symbol.iterator`属性上面，所以调用这个属性就得到遍历器对象。

## 源码

```js
/**
 * Converts `iterator` to an array.
 *
 * @private
 * @param {Object} iterator The iterator to convert.
 * @returns {Array} Returns the converted array.
 */
function iteratorToArray(iterator) {
  let data
  const result = []

  while (!(data = iterator.next()).done) {
    result.push(data.value)
  }
  return result
}

export default iteratorToArray
```

首先定义一个新的数组`result`，然后一直调用`next`方法获取值并`push`进`result`中，当`done`为`true`是表示遍历完毕。


## 参考

[阮一峰: ECMAScript 6 Iterator和 for...of 循环](https://es6.ruanyifeng.com/#docs/iterator#Iterator%EF%BC%88%E9%81%8D%E5%8E%86%E5%99%A8%EF%BC%89%E7%9A%84%E6%A6%82%E5%BF%B5)