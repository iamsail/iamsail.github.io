---
title: 使用serve部署静态资源在特定的端口
date: 2018-10-05 18:57:01
categories: Vue
tags: [node]
---

### ** Preface **

本文是对使用[GitHub - zeit/serve](https://github.com/zeit/serve)部署静态资源的记录。

******************

vue官方文档里推荐的静态资源部署工具是[GitHub - zeit/serve](https://github.com/zeit/serve)。

```js
npm install -g serve
# -s 参数的意思是将其架设在 Single-Page Application 模式下
# 这个模式会处理即将提到的路由问题
serve -s dist
```
会返回

```js
 ┌───────────────────────────────────────────────┐
   │                                               │
   │   Serving!                                    │
   │                                               │
   │   - Local:            http://localhost:5000   │
   │   - On Your Network:  http://127.0.1.1:5000   │
   │                                               │
   │   Copied local address to clipboard!          │
   │                                               │
   └───────────────────────────────────────────────┘

```


serve默认的端口是5000,如果想指定在特定的端口,执行以下命令即可

```js
serve -s dist --listen 4999 
```





*********************
### ** 参考 **

[部署 | Vue CLI 3](https://cli.vuejs.org/zh/guide/deployment.html#%E9%80%9A%E7%94%A8%E6%8C%87%E5%8D%97)
[Re-added `--single` and made `--listen` support ports by leo · Pull Request #384 · zeit/serve · GitHub](https://github.com/zeit/serve/pull/384)