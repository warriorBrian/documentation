# Hash

## 作用

`Hash`就是一个离散的序列（散列）,根据`key`来存储数据。

`Hash`在lodash的`.internal`文件夹中，作为内部文件来使用，lodash会根据不同的数据类型选择不同的缓存方式，`Hash`便是其中一种方式，**这种方式只能缓存`key`的类型符合对象键要求的数据。**

## 参考

[pocket-lodash Hash缓存](https://github.com/yeyuqiudeng/pocket-lodash/blob/master/internal/Hash.md)