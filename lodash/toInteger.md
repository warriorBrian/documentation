# toInteger

> 转换value为一个整数

## 用例

```js
_.toInteger(3.2);
// => 3
 
_.toInteger(Number.MIN_VALUE);
// => 0
 
_.toInteger(Infinity);
// => 1.7976931348623157e+308
 
_.toInteger('3.2');
// => 3
```

## lodash 源码

### 依赖

```js
import toFinite from './toFinite.js'
```

[toFinite 分析](lodash/toFinite.md)

### 源码

```js
function toInteger(value) {
  const result = toFinite(value)
  const remainder = result % 1

  return remainder ? result - remainder : result
}

export default toInteger
```

#### 正整数

将有效数进行取模`result % 1`,如果为正整数，则返回`0`，并直接返回值。

#### 负数

如果为负数，则直接返回负数

#### 小数

如果为小数，此时`remainder`得到的值为: `0.20000000000000018`

使用`3.2`进行相减，应该为: `3.2 - 0.20000000000000018`, 得到`3`

#### 字符串和其他超出范围值

如果为字符串，则进行隐式转换，在使用取模`%`会进行转换为有效的数值。

如果超出范围，则使用 [toFinite](lodash/toFinite.md) 进行转为有效值。