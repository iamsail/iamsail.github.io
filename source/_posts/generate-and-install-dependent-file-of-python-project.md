---
title: 生成和安装python项目依赖
date: 2018-12-15 18:40:00
categories: Python
---

### ** Preface **

最近连续遇到项目依赖的问题。今天跑以前的一个旧项目，拉到本地，才意识到python的模块没有写依赖。

**********************

### ** 依赖管理 **

#### ** 生成依赖文件 **

```
pip3 freeze [options]

Description:
  Output installed packages in requirements format.

  packages are listed in a case-insensitive sorted order.
```


本地开发的项目安装好各种库过后，执行

```
pip freeze > requirements.txt
```

即可生成项目依赖文件`requirements.txt`

***********************

#### ** 使用依赖文件 **

在项目目录，执行

```
pip install -r requirements.txt

# -r, --requirement <file>    Install from the given requirements file. This option can be used multiple times.
```

即会安装所需的依赖。