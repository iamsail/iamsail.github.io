---
title: mac系统空间清理
date: 2019-07-07 17:39:17
categories: Mac
---
### ** Preface **
mac使用了一段时间过后,提示空间不够。在发现很大的磁盘空间都是被系统占用(关于通过本机->存储空间 进行查看)。
在网上查看了一些方案看解决这个问题,目前只找到了一个适用于我的方案，做下记录。

****************

### ** 解决办法 **

我使用的辅助清理的软件是OmniDiskSweeper。

通过该软件分析到,根目录下的`.cleverfiles`的`hlink.ref`目录占用空间很大。
这个目录存放的是之前删除过的软件,最终都跑到这个目录下了。之所以是这样，是因为电脑上安装了`disk drill`,它会把这个删除的内容部分到前面提到的目录。所以直接去删除hlink.ref目录,还是会立刻恢复,是删除不掉的。

1.需要先取消`.cleverfiles`目录的隐藏属性，才可以删除`hlink.ref`目录。
```
#取消隐藏文件夹：
chflags nohidden /.cleverfiles

#设置隐藏文件夹：
chflags hidden /.cleverfiles
```

2.再删除`hlink.ref`目录即可。
通过该方法,我清除了了20多GB的内容,但是还有很多空间被系统占用。日后找到解决的办法，再记录到本文。

****************
### ** 参考 **

[Mac 下修改文件或文件夹的隐藏状态](https://www.cnblogs.com/guansixu/p/6208295.html)
[请问大侠如何清理黄色部分](https://bbs.feng.com/forum.php?mod=viewthread&tid=8208801&mobile=2)