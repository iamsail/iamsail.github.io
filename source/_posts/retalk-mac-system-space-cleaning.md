---
title: 再谈mac系统空间清理(系统占据磁盘空间过大)
date: 2019-12-15 17:39:17
categories: Mac
---

### ** Preface **

系统提示mbp空间不够。mac磁盘空间，不知道为什么显示被系统占据，但是又不知道系统这部分到底是什么文件。如下图所示
![1.png](/img/Mac/1.png)
其中黄色部分的系统，占据了我磁盘空间的接近200GB,清理之前,黄色系统部分,几乎占据了整个长条。清理过后，只占据了70多GB。


之前写了一篇博客[mac系统空间清理](http://www.sail.name/2019/07/07/Mac-system-space-cleaning/)。但是当时只清理了20多GB的空间出来。没有找到真正空间不足的原因。

这次彻底解决了，本文做下记录。

**********************

我是通过`DaisyDisk`这个软件来分析磁盘空间的占据情况。

![2.png](/img/Mac/2.png)

根据可视化界面可以看出在`/private/var/folders/zz/zyxvpxvq6csfxvn_n00000s0000068/C/softwareupdated/com.apple.SoftwareUpdate`目录下,有一堆文件,命名类似`CFNetworkDownload*`。

直接拖拽删除，软件会提示说，是系统依赖的文件，不可以删除。难道就放任这堆文件，占据接近150GB的空间吗？

经过一番查找，弄清楚了原因:

1、`/private/var/folders/zz/zyxvpxvq6csfxvn_n00000s0000068/C/softwareupdated/com.apple.SoftwareUpdate`大量形如CFNetworkDownload_0gIeHN.tmp的文件是下载软件更新的缓存文件，可以删除。
2、`2015Mac OSX 10.11 EI Capitan`之后，OS X引入了`SIP(SystemIntegrity Protection)`系统完整性保护，这样有的目录是进不去的。
3、在网上搜索Mac关闭SIP，有一堆教程，参考执行，大致步骤：重启时按住Cmd+R进入Recovery模式，然后通过csrutil status, csrutil disable等命令关闭SIP。
4、关闭后，`sudo su`，然后就可以访问相关目录，删除文件了。
5、删除文件要谨慎，删除的时候，需要十分明白你在干什么，否则还是保守点别做了，本教程不负任何责任，删除完成后，马上重启电脑，即可重新打开SIP。
**********************
### ** SIP **

SIP 全称为`「System Integrity Protection」即「系统完整性保护」`，是 `OS X El Capitan` 时开始采用的一项安全技术，SIP 将一些文件目录和系统应用保护了起来。但这会影响我们一些使用或设置，比如：更改系统应用图标、终端操作系统目录文件提示「Operation not permitted」、Finder 无法编辑系统目录里的文件。

因为 SIP 是系统级的权限操作，我们无法直接关闭它，需要前往「macOS 恢复功能」下进行。
将 Mac 开机，立即在键盘上按住 `Command ⌘ + R`，直到看到 `Apple` 标志或旋转的地球时松开。看到「实用工具」窗口时，恢复功能启动即完成。

![3.png](/img/Mac/3.png)
![4.png](/img/Mac/4.png)
#### ** 查看状态/关闭/开启 **

```
# 查看状态
csrutil status

# 关闭sip
csrutil disable

# 开启sip
csrutil enable
```

**********************
### ** 后记 **

这个磁盘问题，我折腾了大半年了吧。知道这几天才真正解决。多出了接近150GB的空间出来。

这里有几点体会:
1. 遇到事情，可以不用一直折腾。但是不要放弃，偶尔回过头来看看。
2. 方法工具很重要。之前尝试了很多工具,比如`OmniDiskSweeper`,`腾讯柠檬`等，都没能彻底解决问题。最近和同事交流才知道了`DaisyDisk`。

**********************
### ** 参考链接 **

- [CFNetworkDownload_xxxxxxx.tmp是什么文件，怎么才能清理释放磁盘空间？](https://bbs.feng.com/read-htm-tid-11706537.html)
- [macOS 开启或关闭 SIP](https://sspai.com/post/55066)

