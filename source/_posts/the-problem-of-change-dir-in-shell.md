---
title: shell脚本中cd切换目录失败
date: 2018-09-20 13:31:00
categories: Linux
tags: Shell
---
### ** Preface **

本文是对shell脚本中cd命令切换目录失败的相关记录
*****************
### ** 重现 **

`test1`脚本如下

```javascript
#!/bin/bash
jump_dir=/home/sail
if [ -d $jump_dir ]
then 
	echo "the $jump_dir directory exist"
	cd $jump_dir 
	ls
else
   	echo "the $jump_dir directory does not exist"
fi	
```

执行`./test1`,终端打印出了`$jump_dir`目录下的内容,但是最终还是在当前目录,没有跳转到`$jump_dir`目录。

之所以会出现这样的结果,是因为在终端执行`./test1`(直接运行脚本)会产生一个子shell，并在子shell中逐个执行脚本中的指令，在子shell中已经切换了目录了，但是子shell一旦执行完，马上退出，子shell中的变量和操作全部都收回。回到终端根本就看不到这个过程的变化。子shell从父shell中继承了环境变量，但是执行后不会改变父shell的环境变量；可以这样理解：在子shell中的操作和环境变量不会影响父进程，在执行完shell后又回到了父进程。

这里再通过两个脚本验证下

`test2`脚本如下,该脚本在`/home/sail/hacker/code/shell/demo`目录:

```javascript
#!/bin/bash
jump_dir=/home/sail
pwd
cd $jump_dir
pwd
```

执行`./test2`,执行结果为

```javascript
/home/sail/hacker/code/shell/demo
/home/sail
```

以上结果可以说明的确是有切换过目录的

`test3`脚本如下:

```javascript
#!/bin/bash
history
cd /home/sail
sleep 1
pwd
```
执行`./test3`,执行结果为

```javascript
/home/sail
```
`history`没有内容打印出来,说明开了一个子进程,没有历史命令。
*****************
### ** source命令 **
如果我们期望可以在shell脚本中cd切换目录,可以使用如下方式
`source shell-filename` or `. ./shell-filename`
** `source`命令又称为点命令，作用：在当前shell环境下读取并执行脚本中的命令，通常用于重新执行刚修改过的初始化文件，使之立即生效，而不必注销并登录 **

*****************
### ** 参考 **

[将Vim编辑器打造成Bash Shell脚本IDE](https://blog.csdn.net/liuchunming033/article/details/71089381)
[Shell脚本中cd命令使用](https://blog.csdn.net/firefoxbug/article/details/7317279)
[【Shell】关于shell脚本中执行cd命令无效的分析](https://blog.csdn.net/SoaringLee_fighting/article/details/78989918)
[pushd命令](http://man.linuxde.net/pushd)
[方便的目录切换——dirs、pushd、popd命令](http://www.361way.com/pushd/1118.html)