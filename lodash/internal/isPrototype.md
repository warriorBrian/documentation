# isPrototype

## 作用

用来判断传入的值是否是原型对象。

## lodash源码

```js
/** Used for built-in method references. */
const objectProto = Object.prototype

/**
 * Checks if `value` is likely a prototype object.
 *
 * @private
 * @param {*} value The value to check.
 * @returns {boolean} Returns `true` if `value` is a prototype, else `false`.
 */
function isPrototype(value) {
  const Ctor = value && value.constructor
  const proto = (typeof Ctor === 'function' && Ctor.prototype) || objectProto

  return value === proto
}

export default isPrototype
```

### JavaScript权威指南 8.2.3 构造函数调用


如果函数或者方法调用之前带有关键字`new`，它就构成构造函数调用。构造函数调用和普通的函数调用以及方法调用在**实参处理、调用上下文和返回值方面都有不同。**

如果构造函数调用在括号内包含一组实参列表，先计算这些实参表达式，然后传入函数内，这和函数调用和方法调用是一致的。

但如果构造函数没有形参，JavaScript构造函数的语法是允许省略实参列表和圆括号的。凡是没有形参的构造函数调用都可以省略圆括号，比如，下面这两行代码就是等价的：

```js
var o = new Object();

var o = new Object;
```

构造函数调用创建一个新的空对象，这个对象集成自构造函数的`prototype`属性。

构造函数试图初始化这个新创建的对象，并将这个对象用作调用上下文，因此构造函数可以使用`this`关键字来引用这个新创建的对象。

> [!tip|style:flat]
> 注意：尽管构造函数看起来像一个方法调用，它依然会使用这个新对象作为调用上下文，也就是说，在表达式`new o.m()`中，调用上下文并不是`o`。

**通常构造函数不适用`return`关键字，它们通常初始化新对象，当构造函数的函数体执行完毕时，它会显式返回。**

**在这种情况下，构造函数调用表达式的计算结果就是这个新对象的值。然而如果构造函数显式的使用`return`语句范湖一个对象，那么调用表达式的值就是这个对象。**

**如果构造函数使用`return`语句但没有执行返回值，或者返回一个原始值，那么这时将忽略返回值，同时使用这个新对象作为调用结果。**


### JavaScript权威指南 9.2 类和构造函数

**构造函数会自动创建对象，然后将构造函数作为这个对象的方法来调用一次，最后返回这个新对象。**

也就是说，`new`是一个运算符，这个运算符会触发三个动作：

1. 创建一个新的空对象

2. 把这个空对象作为参数传递给构造函数，这个参数就是`this`，也就是函数的上下文，传递过程是隐式的，然后执行构造函数

3. 返回这个新构造的对象

### new 创建实例的过程

```js
function Test () {
	this.a = a
	this.b = b
}

Test.prototype.noop = function () {}
```

在使用`new Test`创建实例时，模拟`fakeNew`函数大致还原过程:

```js
function fakeNew () {
	var obj = {}
	obj.__proto__ = Test.prototype
	return obj
}
```

这里的原型对象是`obj.__proto__`，也就是`Test.prototype`。

任何函数都有一个`prototype`对象，这个对象有一个属性`constructor`，`constructor`属性的值默认执行的是原函数。

因此要判断一个对象是否为原型对象就比较简单，只要判断这个对象是否有`constructor`属性，如果有`constructor`属性，则`constructor`的属性值应该为一个函数，并且这个函数的`prototype`属性就是这个对象。

### lodash源码中的处理

```js
const objectProto = Object.prototype
function isPrototype(value) {
  const Ctor = value && value.constructor
  const proto = (typeof Ctor === 'function' && Ctor.prototype) || objectProto

  return value === proto
}
```

源码中，如果`Ctor`找不到`constructor`，`proto`会赋值为默认的`Object.prototype`

如果传入的值为`false`，现在的`isPrototype`函数得到的`proto`也为`false`，最终的结果会返回`true`，这明显不符合预期，因此这里用`Object.prototype`来做守卫。

## 参考

[JavaScript权威指南 第六版](https://baike.baidu.com/item/Javascript%E6%9D%83%E5%A8%81%E6%8C%87%E5%8D%97/6923938?fr=aladdin)

[对角另一面: pocket-lodash isPrototype](https://github.com/yeyuqiudeng/pocket-lodash/blob/master/internal/isPrototype.md)

























