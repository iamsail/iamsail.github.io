---
title: JS内存溢出
date: 2019-10-29 22:05:01
tags: [node]
---

### ** Preface **

随着项目的越来越大, 最近开始遇到项目在build的时候, 报错`JavaScript heap out of memory`。

**********
### ** 内存溢出 **

`nodejs` 默认限制了最大可使用的内存大小,`nodejs V8 `引擎在 64 位机器上默认限制使用内存最大不超过 1.7GB，超过这个限制官方建议尝试优化为多线程方式。

<span class="under0">** 解决办法可以是增加 nodejs 可使用的最大内存大小，也可以从降低程序内存消耗的角度入手。**</span>

**********

### ** 解决方法 **

####  ** 修改max_old_space_size **

更改环境变量

```javascript
# windows
set NODE_OPTIONS=--max_old_space_size=4096

# mac/linux
export NODE_OPTIONS=--max_old_space_size=4096
```

修改`package.json`的`script`脚本,如下

```
"dev": "NODE_ENV=development node --max-old-space-size=4096 index",
```

#### ** 降低程序内存消耗 **

比如配置`webpack`关闭`sourceMap`

**********

### ** 参考链接 **

[nodejs 执行失败报错 “JavaScript heap out of memory” 的解决办法](https://lzw.me/a/angular-javascript-heap-out-of-memory.html)