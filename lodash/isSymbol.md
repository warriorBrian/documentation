# isSymbol

> 检查 值 是否是原始 Symbol 或者对象。

## 用例

```js
_.isSymbol(Symbol.iterator);
// => true
 
_.isSymbol('abc');
// => false
```

## lodash源码

### 依赖

```js
import getTag from './.internal/getTag.js'
```

[getTag 分析](lodash/internal/getTag.md)

```js
function isSymbol(value) {
  const type = typeof value
  return type == 'symbol' || (type === 'object' && value != null && getTag(value) == '[object Symbol]')
}

export default isSymbol
```

与`isObject`大同小异，首先判断类型是否为`symbol`

`(type === 'object' && value != null && getTag(value) == '[object Symbol]')`

* 类型为`object`
* `value`值不等于`undefined`或`null`
* 类型字符串(`toString.call()`)等于`[object Symbol]`