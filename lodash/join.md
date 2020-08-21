# join

> 将 array 中的所有元素转换为由 separator 分隔的字符串

## 用例

```js
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

## lodash源码

```js
/** Used for built-in method references. */
var arrayProto = Array.prototype;

/* Built-in method references for those with the same name as other `lodash` methods. */
var nativeJoin = arrayProto.join;

function join(array, separator) {
  return array == null ? '' : nativeJoin.call(array, separator);
}

export default join;
```

如果为`null`或者`undefined`，返回空

否则调用`join`进行分隔。