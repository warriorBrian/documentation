# eq

> 比较两者的值，来确定它们是否相等，遵循[SameValueZero](http://ecma-international.org/ecma-262/6.0/#sec-samevaluezero)规范


## 用例

```js
var object = { 'a': 1 };
var other = { 'a': 1 };
 
_.eq(object, object);
// => true
 
_.eq(object, other);
// => false
 
_.eq('a', 'a');
// => true
 
_.eq('a', Object('a'));
// => false
 
_.eq(NaN, NaN);
// => true
```

## 规范对比

### Strict Equality Comparison (js中全等`===`遵循规范)

1. 如果`x` 和 `y`的类型不同，则返回false。
2. 如果`x`的类型为`number`
	* 如果`x`为`NaN`，返回`false`
	* 如果`y`为`NaN`，返回`false`
	* 如果 `x` 和 `y` 的数值一致，返回 `true`
	* 如果 `x` 为 `+0` 并且 `y` 为 `-0` ，返回 `true`
	* 如果 `x` 为 `-0` 并且 `y` 为 `+0` ，返回 `true`

### SameValue

1. 如果`x` 和 `y`的类型不同，则返回false。
2. 如果`x`的类型为`number`
	* 如果`x` 为`NaN`并且`y`为`NaN`，返回true
	* 如果`x`为`+0`并且`y` 为 `-0`， 返回false
	* 如果`x`为`-0`并且`y`为`+0`，返回false
	* 如果`x`和`y`的数值一致，返回true

### SameValueZero(x, y)

1. 如果`x` 和 `y`的类型不同，则返回false。
2. 如果`x`的类型为`number`
  * 如果`x` 为`NaN`并且`y`为`NaN`，返回true
  * 如果`x`为`+0`并且`y` 为 `-0`， 返回true
  * 如果`x`为`-0`并且`y`为`+0`，返回true
  * 如果`x`和`y`的数值一致，返回true


`Strict Equality Comparison` 、 `SameValue` 和 `SameValueZero` 只是在对待 `+0`、`-0` 和 `NaN` 上有区别。

## lodash 源码

```js
function eq(value, other) {
  return value === other || (value !== value && other !== other)
}
```

第一部分：

```js
value === other
```

遵循`Strict Equality Comparison`规范，如果`value`和`other`都为`NaN`时，返回的是`false`
`NaN === NaN`返回的就是`false`，但是lodash遵循`SomeValueZero`规范，规定为: `x`和`y`都为`NaN`时返回的是`true`。

这段便是处理`NaN`:

```js
(value !== value && other !== other)
```

在js中，只有`NaN`和自身是不相等的，当两个需要对比的值都和自身不相等时，表示这两个值都为`NaN`，返回`true`

### Object.is()

`Object.is(NaN, NaN)`返回的是`true`，但是`Object.is(+0, -0)`返回的是`false`，遵循的是`SameValue`规范。

### isNaN()
参考: [MDN isNaN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isNaN)
> [!warning|style:flat]
> 令人费解的怪异行为，如果`isNaN`函数的参数不是`Number`类型，`isNaN`函数会首先尝试将这个参数转换为数值，然后才会对转换后的结果是否是`NaN`进行判断，因此，对于能被强制转换为有效的非`NaN`数值来说(**空字符串和布尔值分别会被强制转换为数值0和1**)，返回`false`值也许会感觉莫名其妙，比如说：空字符串就明显不是数值(not a number)

也就是说传入的参数不为`Number`类型，会尝试转换成`Number`类型之后再做是否为`NaN`的判断，所以类似`isNaN('aaa')`返回的也是`true`

### Number.isNaN()

在ECMAScript(ES2015)包含`Number.isNaN()`函数，通过`Number.isNaN(x)`来检测变量`x`是否是一个`NaN`将会是一种可靠的做法，然而，在缺少`Number.isNaN`函数的情况下，通过表达式**`(x != x)`自身不等于自身，来检测变量`x`是否是`NaN`会更加可靠**

## 参考

[对角另一面: eq源码分析](https://github.com/yeyuqiudeng/pocket-lodash/blob/master/eq.md)

[MDN isNaN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/isNaN)























