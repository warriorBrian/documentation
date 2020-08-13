# range

> 创建一个包含从 start 到 end，**但不包含 end 本身范围数字的数组**。 如果 start 是负数，而 end 或 step 没有指定，那么 step 从 -1 为开始。 如果 end 没有指定，start 设置为 0。 如果 end 小于 start ，会创建一个空数组，除非指定了 step。

## 用例

```js
_.range(4);
// => [0, 1, 2, 3]
 
_.range(-4);
// => [0, -1, -2, -3]
 
_.range(1, 5);
// => [1, 2, 3, 4]
 
_.range(0, 20, 5);
// => [0, 5, 10, 15]
 
_.range(0, -4, -1);
// => [0, -1, -2, -3]
 
_.range(1, 4, 0);
// => [1, 1, 1]
 
_.range(0);
// => []
```

## lodash源码

### 依赖

```js
import createRange from './.internal/createRange.js'
```

[createRange 分析](lodash/internal/createRange.md)

### 源码

```js
const range = createRange()

export default range
```