# keys

> 创建一个 object 的自身可枚举属性名为数组。

> [!tip]
> 非对象的值会被强制转换为对象

## 用例

```js
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.keys(new Foo);
// => ['a', 'b'] (iteration order is not guaranteed)
 
_.keys('hi');
// => ['0', '1']
```

## lodash源码

### 依赖

```js
import arrayLikeKeys from './.internal/arrayLikeKeys.js'
import isArrayLike from './isArrayLike.js'
```

[arrayLikeKeys 分析](lodash/internal/arrayLikeKeys.md)

[isArrayLike 分析](lodash/isArrayLike.md)

### 源码

```js
function keys(object) {
  return isArrayLike(object)
    ? arrayLikeKeys(object)
    : Object.keys(Object(object))
}

export default keys
```