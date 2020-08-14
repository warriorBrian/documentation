# toNumber

> 转换一个值为数字

## 用例

```js
_.toNumber(3.2);
// => 3.2
 
_.toNumber(Number.MIN_VALUE);
// => 5e-324
 
_.toNumber(Infinity);
// => Infinity
 
_.toNumber('3.2');
// => 3.2
```

## lodash源码

### 依赖

```js
import isObject from './isObject.js'
import isSymbol from './isSymbol.js'
```

[isObject 分析](lodash/isObject.md)

[isSymbol 分析](lodash/isSymbol.md)

### 源码

```js
/** Used as references for various `Number` constants. */
const NAN = 0 / 0

/** Used to match leading and trailing whitespace. */
const reTrim = /^\s+|\s+$/g

/** Used to detect bad signed hexadecimal string values. */
const reIsBadHex = /^[-+]0x[0-9a-f]+$/i

/** Used to detect binary string values. */
const reIsBinary = /^0b[01]+$/i

/** Used to detect octal string values. */
const reIsOctal = /^0o[0-7]+$/i

/** Built-in method references without a dependency on `root`. */
const freeParseInt = parseInt

function toNumber(value) {
  if (typeof value === 'number') {
    return value
  }
  if (isSymbol(value)) {
    return NAN
  }
  if (isObject(value)) {
    const other = typeof value.valueOf === 'function' ? value.valueOf() : value
    value = isObject(other) ? `${other}` : other
  }
  if (typeof value !== 'string') {
    return value === 0 ? value : +value
  }
  value = value.replace(reTrim, '')
  const isBinary = reIsBinary.test(value)
  return (isBinary || reIsOctal.test(value))
    ? freeParseInt(value.slice(2), isBinary ? 2 : 8)
    : (reIsBadHex.test(value) ? NAN : +value)
}

export default toNumber
```

#### 常量

```js
/** 使用 0 /0 返回 NaN的值 */
const NAN = 0 / 0

/** reTrim: 用来去除首尾空格 */
const reTrim = /^\s+|\s+$/g

/** 用于检测错误的带符号十六进制字符串值 */
const reIsBadHex = /^[-+]0x[0-9a-f]+$/i

/** 用于检测二进制字符串值 */
const reIsBinary = /^0b[01]+$/i

/** 用于检测八进制字符串值。 */
const reIsOctal = /^0o[0-7]+$/i

/** 内置方法引用，不依赖于root */
const freeParseInt = parseInt
```

#### 处理number类型

```js
if (typeof value === 'number') {
  return value
}
```

判断类型如果为`number`则直接返回`value`，不做任何处理。

#### Symbol类型

```js
if (isSymbol(value)) {
  return NAN
}
```

如果为`Symbol`类型，则直接返回`NaN`。

##### Symbol类型

ES5的对象属性名都是字符串，这容易造成属性名的冲突。

ES6引入了一种新的原始数据类型`Symbol`，表示独一无二的值。

`Symbol`是JavaScript语言的第七种数据类型：

* undefined
* null
* boolean
* string
* number
* object
* symbol

**Symbol值可以转为布尔值，但是不能转为数值**

```js
let sym = Symobl();

Boolean(sym) // true

!sym // false


Number(sym) // TypeError

sym + 2 // TypeError
```

#### Object类型

```js
if (isObject(value)) {
  const other = typeof value.valueOf === 'function' ? value.valueOf() : value
  value = isObject(other) ? `${other}` : other
}
```

首先判断`value`中`valueOf`是否存在，如果存在调用`value.valueOf()`。

如果不存在`valueOf`方法，判断是否为`Object`，如果为`Object`则将`other`转换为`string`类型，否则直接将`other`赋值给`value`

##### valueOf

Javascript调用`valueof`方法将对象转换为原始值，很少需要自己调用`valueOf`方法，当遇到要预期的原始值的对象时，JavaScript会自动调用它。

默认情况下，`valueOf`方法由`Object`后面的每个对象继承，每个内置的核心对象都会覆盖此方法以返回适当的值。

如果对象没有原始值，则`valueOf`将返回对象本身。

不同类型对象的valueOf()方法的返回值:

| 对象 | 	返回值 	|
| :---: | :------------:|
| Array | 返回数组对象本身	|
| Boolean | 布尔值 |
| Date | 存储的时间是从 1970 年 1 月 1 日午夜开始计数的毫秒数 UTC |
| Function | 函数本身 |
| Number | 数字值 |
| Object | 对象本身，这是默认情况 |
| String | 字符串值 |

#### 非string类型

```js
if (typeof value !== 'string') {
  return value === 0 ? value : +value
}
```

如果`value`不等于`0`，使用隐式转换`+value`将`value`转换为数字类型。

#### string类型

```js
value = value.replace(reTrim, '')
const isBinary = reIsBinary.test(value)
return (isBinary || reIsOctal.test(value))
  ? freeParseInt(value.slice(2), isBinary ? 2 : 8)
  : (reIsBadHex.test(value) ? NAN : +value)
```

首先，先将`value`去除首尾空格

然后处理进制问题：

如果是二进制(`isBinary`)或者是八进制(`reIsOctal`)，使用`parseInt`进行转换

`parseInt(string, radix)`其中`radix`为指定进制，从`2`到`36`代表改进制的数字。

如果是其他进制，例如十六进制则使用 `+value` 进行转换。































