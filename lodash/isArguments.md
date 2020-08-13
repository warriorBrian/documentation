# isArguments

> 检查 value 是否是一个类 arguments 对象。

## 用例

```js
_.isArguments(function() { return arguments; }());
// => true
 
_.isArguments([1, 2, 3]);
// => false
```

## lodash源码

### 依赖

```js
import getTag from './.internal/getTag.js'
import isObjectLike from './isObjectLike.js'
```

[getTag 分析](lodash/internal/getTag.md)

[isObjectLike 分析](lodash/isObjectLike.md)

### 源码

```js
function isArguments(value) {
  return isObjectLike(value) && getTag(value) == '[object Arguments]'
}

export default isArguments
```

`isAguments`使用`isObjectLike`判断`value`是否为类对象，并且获取类型字符串是否等于`[objet Arguments]`则返回`true`

---
### arguments相关

[MDN: arguments](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)**是一个对应传递给函数的参数的类数组的对象**。

`arguments`对象是所有(非箭头)函数中的可用的**局部变量**，你可以使用`arguments`对象在函数中引用函数的参数。此对象包含传递给函数的每一个参数。

> [!danger|style:flat]
> 在**箭头函数**中使用`arguments`会提示 `Uncaught ReferenceError: arguments is not defined`

**`arguments`对象不是一个`Array`，它类似于`Array`,这个概念是至关重要的。**

**但除了`length`属性和索引元素之外没有任何`Array`属性，例如：它没有`pop`方法，但是它可以被转换为一个真正的`Array`:**

```js
var args = Array.prototype.slice.call(arguments);
var args = [].slice.call(arguments);

// ES2015
const args = Array.from(arguments);
const args = [...arguments];
```

> [!warning|style:flat]
> 对参数使用slice会阻止某些JavaScript引擎中的优化。如果你关心性能，尝试通过遍历arguments对象来构造一个新的数组。另一种方法是使用被忽视的Array构造函数作为一个函数：

```js
var args = (arguments.length === 1 ? [arguments[0]] : Array.apply(null, arguments));
```

#### 对参数使用`typeof`

typeof 参数返回 'object'

```js
console.log(typeof arguments);    // 'object'
// arguments 对象只能在函数内使用
function test(a){
    console.log(a,Object.prototype.toString.call(arguments));
    console.log(arguments[0],arguments[1]);
    console.log(typeof arguments[0]);
}
test(1);
/*
1 "[object Arguments]"
1 undefined
number
*/
```




























