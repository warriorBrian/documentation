# initializeArrayWithRange

初始化一个数组，该数组包含指定范围内的数字。

## Example

```js
initializeArrayWithRange(5); // [0,1,2,3,4,5]
initializeArrayWithRange(7, 3); // [3,4,5,6,7]
initializeArrayWithRange(9, 0, 2); // [0,2,4,6,8]
```

## 实现

```js
const initializeArrayWithRange = (end, start = 0, step = 1) => {
	return Array.from({ length: Math.ceil( (end - start + 1) / step ) }, (v, i) => i * step + start );
}
```

`end`为结束位置

`start`为起始值，例如起始从`0`开始生成

`step`为步长，默认为`1`

### 例子：

```js
initializeArrayWithRange(5); // [0,1,2,3,4,5]
```

`Array.from`的计算`length`为:

```js
(end - start + 1) / step
// => (5 - 0 + 1) / 1 = 6
```

此时`Array.from`中的`length` 为 `6`，返回值为：

```js
i * step + start
// => 0 * 1 + 0 = 0
// => 1 * 1 + 0 = 1
// ...
// => 5 * 1 + 0 = 5
```

---

```js
initializeArrayWithRange(7, 3); // [3,4,5,6,7]
```

`Array.from`计算`length`为:

```js
(end - start + 1) / step
// => (7 - 3 + 1) / 1
// => length: 5 
```

回调返回值为:

```js
i * step + start
// => 0 * 1 + 3 = 3
// => 1 * 1 + 3 = 4
// ...
// => 4 * 1 + 3 = 7
```

---

```js
initializeArrayWithRange(9, 0, 2); // [0,2,4,6,8]
```

设置结束值为: 9

设置开始值为: 0

设置步长为: 2

`Array.from`计算`length`为:


```js
(end - start + 1) / step
// => (9 - 0 + 1) / 2
// => length: 5
```

回调返回值为:

```js
i * step + start
// 0 * 2 + 0 = 0
// 1 * 2 + 0 = 2
// 2 * 2 + 0 = 4
// 3 * 2 + 0 = 6
// 4 * 2 + 0 = 8
```


































