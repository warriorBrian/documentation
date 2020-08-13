# copyArray

## 作用

将`source`的值复制到`array`中。

`copyArray`接收两个参数`source`, `array`。

如果`array`不传，则默认使用`new Array(length)`（空数组）

> [!note]
> 如果不传入`array`也可以做到数组的深拷贝。

## lodash源码

```js
function copyArray(source, array) {
  let index = -1
  const length = source.length

  array || (array = new Array(length))
  while (++index < length) {
    array[index] = source[index]
  }
  return array
}

export default copyArray
```

首先，获取`length`为`source`长度，如果第二个参数(`array`)不传，则创建一个与`source`长度一致的空数组。

然后遍历`source`,将`source`中的每一个值，对应`array`下标进行赋值

然后返回新创建的数组或传入的数组。