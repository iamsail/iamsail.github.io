---
title: (python)重新加载模块
date: 2018-05-30 12:19:00
categories: Python
---

在python2.x版本中,可以使用`reload()`重新加载模块

但是在python3.x已经不在支持该方法,需要像如下这样

```
> import importlib
> importlib.reload(moudle-name)
```

*******************

### ** 参考 **

[python reload(sys)找不到，name 'reload' is not defined](https://blog.csdn.net/x356982611/article/details/52538548)