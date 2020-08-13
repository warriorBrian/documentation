# isString

> 检查 值 是否是原始字符串string或者对象。

## 用例

```js
_.isString('abc');
// => true
 
_.isString(1);
// => false
```

## lodash源码

### 依赖

```js
import getTag from './.internal/getTag.js'
```

[getTag 分析](lodash/internal/getTag.md)

### 源码

```js
function isString(value) {
  const type = typeof value
  return type === 'string' || (type === 'object' && value != null && !Array.isArray(value) && getTag(value) == '[object String]')
}

export default isString
```

---

```js
type === 'string'
```

判断类型是否为基本类型`string`

```js
(type === 'object' && value != null && !Array.isArray(value) && getTag(value) == '[object String]')
```

首先判断如果：

* **`value`类型为`object`类型**

* **`value`值不等于`undefined`或`null`**

* **`value`值不为数组**

* **使用`getTag`返回类型字符串，判断是否为引用类型(使用构造函数创建：`new String()`)**
















