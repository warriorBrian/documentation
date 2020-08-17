# toString

> 转换 值 为字符串。 null 和 undefined 将返回空字符串。-0 将被转换为字符串"-0"。

## 作用

```js
_.toString(null);
// => ''
 
_.toString(-0);
// => '-0'
 
_.toString([1, 2, 3]);
// => '1,2,3'
```

## lodash源码

### 依赖

```js
import isSymbol from './isSymbol.js'
```

[isSymbol 分析](lodash/isSymbol.md)

### 源码

```js
/** Used as references for various `Number` constants. */
const INFINITY = 1 / 0

function toString(value) {
  if (value == null) {
    return ''
  }
  // Exit early for strings to avoid a performance hit in some environments.
  if (typeof value === 'string') {
    return value
  }
  if (Array.isArray(value)) {
    // Recursively convert values (susceptible to call stack limits).
    return `${value.map((other) => other == null ? other : toString(other))}`
  }
  if (isSymbol(value)) {
    return value.toString()
  }
  const result = `${value}`
  return (result == '0' && (1 / value) == -INFINITY) ? '-0' : result
}

export default toString
```

#### 处理undefined或null

```js
if (value == null) {
  return ''
}
```

#### 处理字符串

```js
if (typeof value === 'string') {
  return value
}
```

在源码中的注释是这样解释的: 尽早退出以免在某些环境下降低性能。

#### 处理数组

```js
if (Array.isArray(value)) {
  // Recursively convert values (susceptible to call stack limits).
  return `${value.map((other) => other == null ? other : toString(other))}`
}
```

遍历数组，如果数组中的值为`null`或者`undefined`则直接返回，否则递归调用

#### 处理Symbol

```js
if (isSymbol(value)) {
  return value.toString()
}
```

如果为`Symbol`类型，则调用`toString()`方法转为字符串。

例如:

```js
const b = Symbol('sss')

b.toString() // Symbol(sss)
```

#### 处理其他类型

```js
const result = `${value}`

return (result == '0' && (1 / value) == -INFINITY) ? '-0' : result
```

如果为其他类型，使用字符串模板，进行转换为字符串

**如果转换为字符串`0`**，进行`1 / value`如果为`-INFINITY`则为`-0`转为字符串`'-0'`