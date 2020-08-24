# sample

> 从 collection(集合)中获取一个随机元素。

## 用例

```js
_.sample([1, 2, 3, 4]);
// => 2
```

## lodash源码

```js
function sample(array) {
  const length = array == null ? 0 : array.length
  return length ? array[Math.floor(Math.random() * length)] : undefined
}

export default sample

```

首先，如果为`undefined`或者为`null`直接返回`undefined`

否则创建一个范围(`Math.floor(Math.random() * length)`)随机获取范围内的值