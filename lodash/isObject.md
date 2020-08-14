# isObject

> 检查 值 是否为 Object (例如： arrays, functions, objects, regexes,new Number(0), 以及 new String(''))

## 用例

```js
_.isObject({});
// => true
 
_.isObject([1, 2, 3]);
// => true
 
_.isObject(_.noop);
// => true
 
_.isObject(null);
// => false
```

## lodash源码

```js
function isObject(value) {
  const type = typeof value
  return value != null && (type === 'object' || type === 'function')
}

export default isObject
```

首先判断`value`不为`undefined`或`null`

类型等于`function`也视为对象，所以要特殊处理。