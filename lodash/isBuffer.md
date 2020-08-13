# isBuffer

> 检查 值 是否是个 buffer。

## 用例

```js
_.isBuffer(new Buffer(2));
// => true
 
_.isBuffer(new Uint8Array(2));
// => false
```

## lodash源码

### 依赖

```js
import root from './.internal/root.js'
```

[root 源码分析](lodash/internal/root.md)

### 源码

```js
/** Detect free variable `exports`. */
const freeExports = typeof exports === 'object' && exports !== null && !exports.nodeType && exports

/** Detect free variable `module`. */
const freeModule = freeExports && typeof module === 'object' && module !== null && !module.nodeType && module

/** Detect the popular CommonJS extension `module.exports`. */
const moduleExports = freeModule && freeModule.exports === freeExports

/** Built-in value references. */
const Buffer = moduleExports ? root.Buffer : undefined

/* Built-in method references for those with the same name as other `lodash` methods. */
const nativeIsBuffer = Buffer ? Buffer.isBuffer : undefined

/**
 * Checks if `value` is a buffer.
 *
 * @since 4.3.0
 * @category Lang
 * @param {*} value The value to check.
 * @returns {boolean} Returns `true` if `value` is a buffer, else `false`.
 * @example
 *
 * isBuffer(new Buffer(2))
 * // => true
 *
 * isBuffer(new Uint8Array(2))
 * // => false
 */
const isBuffer = nativeIsBuffer || (() => false)

export default isBuffer

```

#### CommonJS检测

**是否支持`exports`**， 检测是否在`Node.js`环境中，`lodash`检测当前环境是否支持`CommonJS`模块加载机制

```js
const freeExports = typeof exports === 'object' && exports !== null && !exports.nodeType && exports
```

`typeof exports === 'object' && exports !== null`这步是确定`exports`是`object`类型，并且不为`null`。

`!exports.nodeType`这步是排除`exports`对象是`html`元素（将某个元素的`id`设置为`exports`，浏览器就会自动增加一个`exports`变量指向该元素。）

**是否支持`module`**

```js
const freeModule = freeExports && typeof module === 'object' && module !== null && !module.nodeType && module
```

判断`exports`是否存在，跟上面同理，在`node.js`中肯定是同时存在`module`和`exports`。


**export 为 module.exports的引用检测**

```js
const moduleExports = freeModule && freeModule.exports === freeExports
```

检测当前环境是否支持`CommonJS`模块加载机制。


#### isBuffer 检测

虽然已经检测当前环境支持`CommonJS`模块加载机制，但是在浏览器上满足这些条件也很简单，因此还不能直接确定当前环境是否存在`Buffer`对象。


```js
const Buffer = moduleExports ? root.Buffer : undefined

const nativeIsBuffer = Buffer ? Buffer.isBuffer : undefined
```

每次取值时都做一次空值检测。

最后，就是`lodash`暴露的`isBuffer`方法：

```js
const isBuffer = nativeIsBuffer || (() => false)
```

将原生的isBuffer方法暴露出去，如果`isBuffer`不存在，则暴露出去的一个永远返回`false`值的方法。

































