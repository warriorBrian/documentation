# baseRange

## 源码

```js
function baseRange(start, end, step, fromRight) {
  let index = -1
  let length = Math.max(Math.ceil((end - start) / (step || 1)), 0)
  const result = new Array(length)

  while (length--) {
    result[fromRight ? length : ++index] = start
    start += step
  }
  return result
}

export default baseRange
```

首先创建`length`: 

`Math.ceil( (end - start) / (step || 1) )`

`(end -start)`可以得到数组的长度，不包含`end`本身范围数字，例如：

* start: 1
* end: 4

那么数组的长度为`3`，当然还有第二个关键条件`step`。

假设步长为`2`，那么数组的长度应该为 `3 / 2`，并使用向上取整`Math.ceil()`，结果为 `2`

使用`Math.max()`防止计算得出的数为负数，与`0`做对比避免出现负数。


使用`while`进行遍历，这时`length`是逐步递减。

`result[fromRight ? length : ++index] = start`，如果`fromRight`为`true`，则使用`length`作为索引，否则使用`index`，而`index`是递增的。

而`fromRight`为`true`时，是从大到小排序。

每次遍历`start`都自加`step`，如果`step`为正数则递增，如果为负数，则递减。


































