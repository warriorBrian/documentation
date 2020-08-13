# toArray

> 转换值为一个数组

## 用例

```js
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]
 
_.toArray('abc');
// => ['a', 'b', 'c']
 
_.toArray(1);
// => []
 
_.toArray(null);
// => []
```

## lodash源码

### 依赖

```js
import copyArray from './.internal/copyArray.js'
import getTag from './.internal/getTag.js'
import isArrayLike from './isArrayLike.js'
import isString from './isString.js'
import iteratorToArray from './.internal/iteratorToArray.js'
import mapToArray from './.internal/mapToArray.js'
import setToArray from './.internal/setToArray.js'
import stringToArray from './.internal/stringToArray.js'
import values from './values.js'
```
[copyArray 分析](lodash/internal/copyArray.md)

[getTag 分析](lodash/internal/getTag.md)

[isArrayLike 分析](lodash/isArrayLike.md)

[isString 分析](lodash/isString.md)

[iteratorToArray 分析](lodash/internal/iteratorToArray.md)

[mapToArray 分析](lodash/internal/mapToArray.md)

[setToArray 分析](lodash/internal/setToArray.md)

[stringToArray 分析](lodash/internal/stringToArray.md)

[values 分析](lodash/values.md)

### 源码

```js
const mapTag = '[object Map]'
const setTag = '[object Set]'

/** Built-in value references. */
const symIterator = Symbol.iterator

function toArray(value) {
  if (!value) {
    return []
  }
  if (isArrayLike(value)) {
    return isString(value) ? stringToArray(value) : copyArray(value)
  }
  if (symIterator && value[symIterator]) {
    return iteratorToArray(value[symIterator]())
  }
  const tag = getTag(value)
  const func = tag == mapTag ? mapToArray : (tag == setTag ? setToArray : values)

  return func(value)
}

export default toArray

```

---

#### 假值

首先判断假值，如果value的值为:

* 空字符串 `''`
* false
* 数字 0
* null
* undefined
* NaN

**则会返回一个空数组。**

```js
if (!value) {
  return []
}
```

#### 类数组

**如果为类数组或者数组。**

在`isArrayLike`方法中，字符串也会被认为是一个类数组

首先判断如果为字符串，就将字符串转换为数组(`stringToArray`)，否则就将value值复制到新的数组中并返回(`copyArray`)。

```js
if (isArrayLike(value)) {
  return isString(value) ? stringToArray(value) : copyArray(value)
}
```

#### 遍历器

如果遍历器存在，并且`value`中有遍历器属性，则使用`iteratorToArray`转为数组

```js
if (symIterator && value[symIterator]) {
  return iteratorToArray(value[symIterator]())
}
```

#### 其他类型

获取类型字符串，如果为`map`(`[object Map]`类型字符串)，则调用`mapToArray`将`map`转为数组

判断是否为`set`类型，如果为`set`类型则调用`setToArray`将`set`转为数组

否则为其他类型，都看作对象，使用`values`进行转换

```js
const tag = getTag(value)

const func = tag == mapTag ? mapToArray : (tag == setTag ? setToArray : values)

return func(value)
```





























