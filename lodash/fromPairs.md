# fromPairs

> 这个方法返回一个由键值对pairs构成的对象。

## 用例

```js
_.fromPairs([['fred', 30], ['barney', 40]]);
// => { 'fred': 30, 'barney': 40 }
```

## lodash源码


```js
function fromPairs(pairs) {
  var index = -1,
      length = pairs == null ? 0 : pairs.length,
      result = {};

  while (++index < length) {
    var pair = pairs[index];
    result[pair[0]] = pair[1];
  }
  return result;
}

export default fromPairs;
```

首先，判断`pairs`是否为`null`或`undefined`，如果是则直接返回一个空对象`{}`。

定义`result`作为容器，遍历pairs二维数组，每次遍历都会得到类似`['fred', 30]`，分别取下标`0`，`1`赋值给result对象，最后返回result。