---
title: hexo出错 ENOSPC Error 
date: 2017-10-31 20:35:17
tags: hexo&&博客记录
---

今天新写博客的时候出现了如下出错

```
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: watch /home/sail/codelife/code/repo/blog/source/ ENOSPC
    at _errnoException (util.js:1021:11)
    at FSWatcher.start (fs.js:1383:19)
    at Object.fs.watch (fs.js:1409:11)
    at createFsWatchInstance (/home/sail/codelife/code/repo/blog/node_modules/chokidar/lib/nodefs-handler.js:37:15)
    at setFsWatchListener (/home/sail/codelife/code/repo/blog/node_modules/chokidar/lib/nodefs-handler.js:80:15)
    at FSWatcher.NodeFsHandler._watchWithNodeFs (/home/sail/codelife/code/repo/blog/node_modules/chokidar/lib/nodefs-handler.js:228:14)
    at FSWatcher.NodeFsHandler._handleDir (/home/sail/codelife/code/repo/blog/node_modules/chokidar/lib/nodefs-handler.js:407:19)
    at FSWatcher.<anonymous> (/home/sail/codelife/code/repo/blog/node_modules/chokidar/lib/nodefs-handler.js:455:19)
    at FSWatcher.<anonymous> (/home/sail/codelife/code/repo/blog/node_modules/chokidar/lib/nodefs-handler.js:460:16)
    at FSReqWrap.oncomplete (fs.js:154:5)
npm ERR! code ELIFECYCLE
npm ERR! errno 2
npm ERR! hexo-site@0.0.0 start: `hexo g && hexo s`
npm ERR! Exit status 2
npm ERR! 
npm ERR! Failed at the hexo-site@0.0.0 start script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/sail/.npm/_logs/2017-10-31T11_19_48_152Z-debug.log

```

因为我在hexo的`package.json`文件中修改了一下启动脚本,如下

```javascript
"scripts": {
    "start": "hexo g && hexo s",
    "build": "hexo g && hexo d"
  },
```

我执行的`npm start`命令,所以这个错误应该是`hexo g`或者`hexo s`产生的,其实是`hexo s`

**************

## ** 错误原因 **

前面的报错信息有一个关键词`ENOSPC`

在[官方文档](https://hexo.io/docs/troubleshooting.html)查了一下,解决方案如下

ENOSPC Error (Linux)
Sometimes when running the command `$ hexo server` it returns an error:

`Error: watch ENOSPC ...`
It can be fixed by running `$ npm dedupe` or, if that doesn’t help, try the following in the Linux console:

`$ echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

<span class="under0">This will increase the limit for the number of files you can watch.</span>

以上的命令作用就是提高我们可以watch的文件数量上限

又查了一下,应该是gulp导致的

主要是因为gulp的watch需要监听很多文件的改动，但是fedora、ubuntu系统的文件句柄其实是有限制的，因此可以使用以下命令：

`$ echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

*************

## ** 后记 **

不知不觉我的博文数量已经110+,数量过多,导致出现了这个问题

甜蜜的烦恼吧23333333


