# root

## 作用

**为了统一返回环境中的this对象**

## lodash源码

## 依赖

```js
/* global globalThis, self */
import freeGlobal from './freeGlobal.js'
```

`freeGlobal`是用来在`node`环境中捕获`global`变量，这个`global`变量有点相当于浏览器环境中的`window`对象。

```js
const freeGlobal = typeof global === 'object' && global !== null && global.Object === Object && global

export default freeGlobal
```

与下面的`freeGlobalThis`的判断方式大同小异，`freeGlobal`不过是用来判断是否在环境中存在`global`对象。这在`node`环境中指向全局。

---

## 源码

```js
/** Detect free variable `globalThis` */
const freeGlobalThis = typeof globalThis === 'object' && globalThis !== null && globalThis.Object == Object && globalThis

/** Detect free variable `self`. */
const freeSelf = typeof self === 'object' && self !== null && self.Object === Object && self

/** Used as a reference to the global object. */
const root = freeGlobalThis || freeGlobal || freeSelf || Function('return this')()

export default root
```

### 检测globalThis

> 全局属性`globalThis`包含全局的`this`值，类似于全局对象

在以前，从不同的JavaScript环境中获取全局对象需要不同的语句，在web中，可以通过`window`、`self`或者`frames`取到全局对象，但是在`(web workers)[https://developer.mozilla.org/zh-CN/docs/Web/API/Worker]`中，只有`self`可以，在`Node.js`中它们都无法获取，必须使用`global`。

`globalThis`提供了一个标准的方式来获取不同环境下的全局`this`对象(也就是全局对象自身)。不像`window`或者`self`这些属性，它确保可以在有无窗口的各种环境下正常工作，所以你可以安心的使用`globalThis`，不必担心它的运行环境，为了便于记忆，你只需要记住：**全局作用于的`this`就是`globalThis`。**

```js
const freeGlobalThis = typeof globalThis === 'object' && globalThis !== null && globalThis.Object == Object && globalThis
```

是否支持`globalThis`，`typeof globalThis === 'object' && globalThis !== null`这步是确定`globalThis`是`object`类型，并且不为`null`。

`globalThis.Object == Object && globalThis` 将返回一个`window`顶层对象(在web中)

### 检测self

> `self`返回一个指向当前的`window`对象的引用。

```js
if (window.parent.frames[0] != window.self) {
    // 当前对象不是frames列表中的第一个时
 }
```

`window.self`几乎总是用于上面示例的比较，用来判断当前`window`是不是父`frameset`中的第一个`frame`

```js
const freeSelf = typeof self === 'object' && self !== null && self.Object === Object && self
```
与`freeGlobalThis`的判断方式相同。

## 参考

[MDN: self](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/self)

[MDN: globalThis](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/globalThis)

[pocket-lodash: lodash源码分析之root](https://github.com/yeyuqiudeng/pocket-lodash/blob/master/internal/root.md)






















































