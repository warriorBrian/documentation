# isEmpty

> 检查`value`是否为一个空对象，集合，映射，或者set,判断的依据是*除非是有枚举的对象，length大于0的arguments,object, array, string或类jquery选择器**
>
> 对象如果被认为空，那么他们没有自己的可枚举的属性对象。
>
> 类数组值，比如arguments对象，array，buffer，string或者类jQuery集合的length 为 0，被认为是空。类似的，map（映射）和set 的size 为 0，被认为是空。

## 用例

```js
_.isEmpty(null);
// => true
 
_.isEmpty(true);
// => true
 
_.isEmpty(1);
// => true
 
_.isEmpty([1, 2, 3]);
// => false
 
_.isEmpty({ 'a': 1 });
// => false
```

## lodash源码

### 依赖
```js
import getTag from './.internal/getTag.js'
import isArguments from './isArguments.js'
import isArrayLike from './isArrayLike.js'
import isBuffer from './isBuffer.js'
import isPrototype from './.internal/isPrototype.js'
import isTypedArray from './isTypedArray.js'
```
[getTag 分析](lodash/internal/getTag.md)

[isArguments 分析](lodash/isArguments.md)

[isArrayLike 分析](lodash/isArrayLike.md)

[isBuffer 分析](lodash/isBuffer.md)

[isPrototype 分析](lodash/internal/isPrototype.md)

[isTypedArray 分析](lodash/isTypedArray.md)

---

### 源码

```js

/** Used to check objects for own properties. */
const hasOwnProperty = Object.prototype.hasOwnProperty

function isEmpty(value) {
  if (value == null) {
    return true
  }
  if (isArrayLike(value) &&
      (Array.isArray(value) || typeof value === 'string' || typeof value.splice === 'function' ||
        isBuffer(value) || isTypedArray(value) || isArguments(value))) {
    return !value.length
  }
  const tag = getTag(value)
  if (tag == '[object Map]' || tag == '[object Set]') {
    return !value.size
  }
  if (isPrototype(value)) {
    return !Object.keys(value).length
  }
  for (const key in value) {
    if (hasOwnProperty.call(value, key)) {
      return false
    }
  }
  return true
}

export default isEmpty
```

#### 处理`null`和`undefined`

```js
if (value == null) {
    return true
}
```

#### 处理类数组对象

```js
if (isArrayLike(value) &&
      (Array.isArray(value) || typeof value === 'string' || typeof value.splice === 'function' ||
        isBuffer(value) || isTypedArray(value) || isArguments(value))
    ) {
    return !value.length
  }
```

`isArrayLike` 用来判断是否为类数组

`Array.isArray` 用来判断是否为数组

`typeof value === 'string'` 用来判断值是否为字符串

`typeof value.splice === 'function'` 用来判断值是否为数组，只有在数组存在`splice`方法。

`isBuffer` 用来判断是否为`Buffer`

`isTypedArray`用来判断是否为`TypedArray`

`isArguments` 用来判断是否为`arguments`对象

以上所有判断，都用`length`属性来判断是否为空。


#### 处理Map及Set

```js
const tag = getTag(value)
if (tag == '[object Map]' || tag == '[object Set]') {
  return !value.size
}
```

如果是`Map`及`Set`，则用`size`来判断是否为空，当`size`为`0`的时候，取反则为`true`

#### 处理原型对象

如果是原型对象，则判断自身可枚举属性是否为空。

#### 处理普通类型及对象

```js
/** Used to check objects for own properties. */
const hasOwnProperty = Object.prototype.hasOwnProperty

for (const key in value) {
  if (hasOwnProperty.call(value, key)) {
    return false
  }
}
```

`for...in`会遍历自身及原型链上的可枚举属性。

**使用`hasOwnProperty.call`来检测自身属性中是否具有执行的属性。**

> [!warning|style:flat]
> **如果直接使用`Object.prototype.hasOwnproperty`来检测，在特定条件下则会出现`undefined`情况。**
>
> **例如如果使用`Object.create(null)`来创建的对象中没有`prototype`属性，所以是没有任何方法的，在这种情况下调用`hasOwnProperty`则会得到`undefined`结果，这显然是不正确的，所以使用`Object.prototype.hasOwnProperty.call(myObj, prop)`可以确保调用到正常的方法，并且拿到正确结果。**


#### 与Object.keys的区别

为什么不用`Object.keys`来判断对象和基本类型，是因为:

在MDN中对Object.keys的`polyfill`有明确表示，使用`Object.keys`会对原始值抛出`TypeError`的错误:

```js
if (!Object.keys) {
  Object.keys = (function () {
    var hasOwnProperty = Object.prototype.hasOwnProperty,
        hasDontEnumBug = !({toString: null}).propertyIsEnumerable('toString'),
        dontEnums = [
          'toString',
          'toLocaleString',
          'valueOf',
          'hasOwnProperty',
          'isPrototypeOf',
          'propertyIsEnumerable',
          'constructor'
        ],
        dontEnumsLength = dontEnums.length;

    return function (obj) {
      if (typeof obj !== 'object' && typeof obj !== 'function' || obj === null) throw new TypeError('Object.keys called on non-object');

      var result = [];

      for (var prop in obj) {
        if (hasOwnProperty.call(obj, prop)) result.push(prop);
      }

      if (hasDontEnumBug) {
        for (var i=0; i < dontEnumsLength; i++) {
          if (hasOwnProperty.call(obj, dontEnums[i])) result.push(dontEnums[i]);
        }
      }
      return result;
    }
  })()
};
```

在判断类型中，如果是原始类型，则会抛出错误:

```js
if (typeof obj !== 'object' && typeof obj !== 'function' || obj === null) throw new TypeError('Object.keys called on non-object');
```




































