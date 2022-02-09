---
title: Git文件名大小写敏感问题
date: 2022-02-09 22:07:00
categories: Git
---

### ** Preface **

前阵子在项目开发的时候遇到一个问题：代码在我本地(Mac)跑起来是正常的，丢到`github actions`跑的时候总是报错。排查了很久，最终发现是因为Git文件名大小写敏感导致的问题，本文做下记录。

*****************

当时有个组件命名是`test.tsx`，然后我改成了`Test.tsx`。代码文件中引入该组件的地方也变成了`../../path/Test.tsx`。但是在`github actions`的机器上执行的时候却提示找不到文件。


<span class="under0">**因为 mac/windows 环境下 Git在不设置大小写敏感规则的时候默认大小写是不敏感，github actions跑的机器是 Linux 的，而 Linux 下 Git是默认大小写敏感的。**</span> 所以我本地机器跑的时候是正常的。

我本地虽然改了文件名为`Test.tsx`，但在github仓库中仍然是`test.tsx `。可是代码中的引用路径已经是`../path/Test.tsx`了，所以在webpack打包编译的时候就会找不到文件。


*****************

### ** 解决办法 **

方法一
删除文件，重新添加文件。（删除之前记得备份下文件内容）


方法二
设置Git大小写敏感（这个方法我没有实际试过）
```
git config core.ignorecase false
```


*****************

### ** 杂感 **

这个问题其实我上大学时，遇到过一次，不过时间长了就忘记了，所以本次特意做下记录，避免再犯。

*****************
### ** 参考 **

- [git 大小写问题 踩坑笔记](https://blog.csdn.net/u013707249/article/details/79135639)
- [git修改文件夹/文件名大小写敏感问题解决](https://blog.csdn.net/u011350541/article/details/86517435)