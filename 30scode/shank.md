# shank

> 具有与 `Array.prototype.splice()` 相同的功能，但**返回一个新数组，而不是对原始数组进行改变**。

## Example

```js
const names = ['alpha', 'bravo', 'charlie'];
const namesAndDelta = shank(names, 1, 0, 'delta'); // [ 'alpha', 'delta', 'bravo', 'charlie' ]
const namesNoBravo = shank(names, 1, 1); // [ 'alpha', 'charlie' ]
console.log(names); // ['alpha', 'bravo', 'charlie']
```

## 实现

```js
const shank = (arr, index = 0, delCount = 0, ...elements) =>
  arr
    .slice(0, index)
    .concat(elements)
    .concat(arr.slice(index + delCount));
```

假设有这样的数组: `const arr = ["alpha", "bravo", "charlie", "apple", "adsfsdf"]`

拿删除举例，`shank(arr, 3, 1)`

此时，逐步分析:

`arr.slice(0, index)`得到的数组应该为: `["alpha", "bravo", "charlie"]`

`concat(elements)`中，目前`elements`为空

`arr.slice(index + delCount)`的结果为：`arr.slice(4)`，得到的数组为：`["adsfsdf"]`，然后使用concat追加进数组中。

其实实现方式就是，删除就是通过两次`slice`对数组的首尾进行分割，排除，删除的数组，然后`concat`追加进数组中。