# now

> 获取当前时间毫秒数

## 用例

```js
_.now()
// => 1597301806616
```

## lodash源码

### 依赖

```js
import root from './internal/root.js';
```

[root 分析](lodash/internal/root.md)

### 源码

```js
var now = function() {
  return root.Date.now();
};

export default now;
```