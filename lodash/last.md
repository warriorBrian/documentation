# last

> 获取array中的最后一个元素

## 用例

```js
_.last([1, 2, 3]);
// => 3
```

## lodash源码

```js
function last(array) {
  const length = array == null ? 0 : array.length
  return length ? array[length - 1] : undefined
}
export default last
```

length的判断，如果`array`为`null`或者`undefined`则`length`为`0`，否则使用数组的`length`

返回值，如果为`0`或者隐式转换为`false`，则直接返回`undefined`

否则返回 `array[length - 1]`