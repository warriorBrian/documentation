# uniqueId

> 生成唯一ID。 如果提供了 prefix ，会被添加到ID前缀上

## 用例

```js
_.uniqueId('contact_');
// => 'contact_104'
 
_.uniqueId();
// => '105'
```

## lodash源码

```js
/** Used to generate unique IDs. */
const idCounter = {}

function uniqueId(prefix='$lodash$') {
  if (!idCounter[prefix]) {
    idCounter[prefix] = 0
  }

  const id =++idCounter[prefix]
  if (prefix === '$lodash$') {
    return `${id}`
  }

  return `${prefix}${id}`
}

export default uniqueId
```

首先定义`idCounter`用来记录生成的id, 不同的`prefix`都有单独的计数，`prefix`默认为`$lodash$`,如果为默认不会拼接前缀。

调用`uniqueId`时会判断指定的前缀是否生成过id,如果没有生成过默认起始位置为`0`

定义变量`id`，第一次调用时前置增加，生成`id`为`1`

如果没有传入`prefix`默认`$lodash$`，直接返回`id`

如果传入前缀，拼接前缀 `prefix + id`