# values

> 创建 object 自身可枚举属性的值为数组。

> [!warning]
> 注意: 非对象的值会强制转换为对象。

## 用例

```js
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.values(new Foo);
// => [1, 2] (无法保证遍历的顺序)
 
_.values('hi');
// => ['h', 'i']
```

## lodash源码

### 依赖

```js
import baseValues from './.internal/baseValues.js'
import keys from './keys.js'
```

[baseValues 分析](lodash/internal/baseValues.md)

[keys 分析](lodash/keys.md)

### 源码

```js
function values(object) {
  return object == null ? [] : baseValues(object, keys(object))
}

export default values
```

首先判断`object`，如果没有传入值，或者为`undefined`、`null`，将会返回一个空数组

否则返回`object`中的每一个值，并将转换为数组返回。