# baseValues

## 作用

baseValues是将`object`的属性对应的值取出来，返回一个包含值的数组

## lodash源码

```js
function baseValues(object, props) {
  return props == null ? [] : props.map((key) => object[key])
}

export default baseValues
```

**如果`props`传入为`undefined`、`null`或者没有传入值，则返回一个空的数组。**

**否则将对提供的keys数组(`props`)进行遍历，利用 [map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 特性会返回一个新的数组。**