# castArray

> 如果value 不是数组，那么强制转为数组。

## 用例

```js
_.castArray(1);
// => [1]
 
_.castArray({ 'a': 1 });
// => [{ 'a': 1 }]
 
_.castArray('abc');
// => ['abc']
 
_.castArray(null);
// => [null]
 
_.castArray(undefined);
// => [undefined]
 
_.castArray();
// => []
 
var array = [1, 2, 3];
console.log(_.castArray(array) === array);
// => true
```

## lodash源码

```js
function castArray(...args) {
  if (!args.length) {
    return []
  }
  const value = args[0]
  return Array.isArray(value) ? value : [value]
}

export default castArray
```

`castArray`会将传入的`value`转换成数组返回，如果传入的`value`已经是数组，则返回原值

