---
title: 联想R720安装双系统问题记录
date: 2018-05-27 18:19:17
categories: 代码人生
---
### ** Preface **

昨晚帮同学装了双系统,是新买的电脑,**联想拯救者R720**。记录下遇到几个问题,或许以后还会碰到。

**这个本子是512G的ssd,是在这个硬盘里装win10+Ubuntu16**。一个磁盘win10,一个磁盘Ubuntu16。

我自己电脑是ssd装的ubuntu,机械装的win10。因为之前给自己装的时候,全部装在ssd始终没成功,以后或许可以再试试。

***********
### ** 分区 **

因为我们Ubuntu是单独装在一个磁盘里的,安装的时候会涉及到一个分区的问题。

这是我以前看的一篇博文的建议如下
```
安装的过程中需要涉及到分区，为了以免日后重装，我的建议是如下分区：
1）、20G,主分区,空间起始位置,Ext4日志文件系统,挂载点/
2）、内存的大小,8G,逻辑分区,空间起始位置,swap交换空间,无挂载点
3）、200MB,逻辑分区,空间起始位置,Ext4日志文件系统,/boot
4）、剩余的空间,逻辑分区,空间起始位置,Ext4日志文件系统,/home
```
** 图表展示 **

|大小(MB)|新分区类型|新分区的位置|用于|挂载点|
|:----:|:----:|:----:|:----:|:----:|
|20000|主分区|空间起始位置|Ext4日志文件系统|/|
|8000|逻辑分区|空间起始位置|交换空间|无|
|200|逻辑分区|空间起始位置|Ext4日志文件系统|/boot|
|剩余的空间|逻辑分区|空间起始位置|Ext4日志文件系统|/home|

当然空间充足的话,可以给8000,200MB调大些,我一般都会多加几个G。

***********
### ** BIOS设置 ** 

这里我是用U盘做的Ubuntu的启动盘,因为PC本身就是win10。但是这个本子却检测不了,不能进入安装界面。

需要对BIOS(F2进入BIOS)进行如下修改

1.进入`Configuration`选项，将`SATA Controller Mode`选为`ACHI`模式（不选为这个模式的话安装的时候ubuntu读不出来硬盘）。 
2.进入`Security`选项将`Secure Boot`选为`disabled`。

当然需要自己修改为优先U盘启动电脑(F12).
如果后面不能进入windows,就将刚才那两个BIOS修改的地方改回之前的值即可。 

***********
### ** 无线网卡问题(搜不到wifi) ** 

装好系统过后,发现搜索不到WiFi,后来定位到是无线网卡问题。最终在贴吧找到了解决方法(贴吧真的大神多),**这里做下搬运工,链接已经放在了文末**。

之前，在本吧发了一篇《亲测 联想r720 双硬盘+win10+Ubuntu16.04双系统安装》的帖子。在装好Ubuntu16.04后，发现联想R720的无线网卡（RTL8821AE）存在hard blocked问题（即“Enable Wi-Fi”不起作用）以及wifi信号易断开问题。故在次将我的解决方法写出来，供大家参考。


#### ** 问题一 **
** 1.1 问题描述 **
笔记本型号：Lenovo r720笔记本（i5-7300hq，gtx1060 maxq 6g），默认装入Win10系统，然而当装入Ubuntu16.04双系统时，会出现无线网卡（型号：RTL8821AE）被hard blocked问题。
即：
在终端敲入：
```
rfkill list all
```
会出现：
```
0:ideapad_wlan: Wireless LAN
Soft blocked: no
Hard blocked:yes
1:ideapad_bluetooth: Bluetooth
Soft blocked: no
Hard blocked: yes
2:phy0: Wireless LAN
Soft blocked: no
Hard blocked:no
3:hci0: Bluetooth
Soft blocked: yes
Hard blocked: no
```
可以看到，优先级前的`ideapad_wlan`的`Hard blocked`默认为`yes`，** <span class="under0">即ubuntu默认关闭了硬件wifi开关，而联想R720的wifi只有软件开关，没有硬件开关的启动，所以引起了wifi无法开启的问题。</span> **


** 1.2 解决方法 **
从无线模块的显示列表可以看出，序号2的wifi模块是软硬件是可以启动的，所以，只要将前面默认的模块移出即可。
#### ** <span class="under0"> a）方法一：</span> ** ####
1）移出ideapad无线模块：
```
sudo modprobe -r ideapad_laptop
```
2）使用命令查看：
```
rfkill list all
```
如下提示：
```
2:phy0: Wireless LAN
Soft blocked: no
Hard blocked:no
3:hci0: Bluetooth
Soft blocked: yes
Hard blocked: no
```
即wifi模块工作正常，然而每次重启ubuntu系统都要重新进行模块移出，故可将该命令设置为开机自启动。
3）在`/etc/rc.local`文件中添加命令：
```

#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.
#因为使用的是非管理员登录，故在执行sudo命令时要输入密码，方可自动化执行，
#此处假设用户密码为123，命令一定要在exit 0之前运行，该文件如果没有修改权限
#修改前使用 chmod 命令修改权限即可！
echo "123" |sudo modprobe -r ideapad_laptop
exit 0
```

开机启动后系统会自动执行改脚本文件，完成wifi模块的自动移出操作。



#### **<span class="under0"> b）方法二（推荐）：</span> ** ####
通过列入黑名单的方式来实现自动移出`ideapad_laptop`设备。
1）创建`/etc/modprobe.d/ideapad.conf`文件：
```
sudo touch /etc/modprobe.d/ideapad.conf
```
2）编辑`ideapad.conf`文件：
```
sudo gedit ideapad.conf
```
3) 在`ideapad.conf`文件中添加：
```
blacklist ideapad_laptop
```
4) 关闭并保存`ideapad.conf`文件，移除`ideapad_laptop`设备：
```
sudo modprobe -r ideapad_laptop
```
5) 注销重启Ubuntu系统，可以看到无线设备能够被打开，并能搜索到WiFi信号。


#### ** 问题二 **
2.1 问题描述
在解决以上无线网卡开启问题后，发现已连接的wifi容易断开并且信号强度较差

2.2 解决方法
1）插上有线网
2）打开终端
3）在终端依次执行：
```
sudo apt-get install git build-essential linux-headers-$(uname -r)

git clone https://github.com/lwfinger/rtlwifi_new.git

cd rtlwifi_new

make

sudo make install
```
4）重启计算机

***********
### ** 宽带连接问题 **

这个本子在网线连接宽带的时候，也出现了一个错误,如下

** 抱歉,扫描了2个接口,但供应商的访问集中器没有响应。请检查您的网线以及调制解调器的线缆是否接好。导致扫描失败的另一个可能原因是其他的pppoe进程正在占用调制解调器。 **

据同学反馈,解决如下

编辑`/etc/NetworkManager/NetworkManager.conf`，将`managed=false`改成`managed=true` 然后重启.

***************

Linux里面有两套管理网络连接的方案：

1、/etc/network/interfaces（/etc/init.d/networking） 
2、Network-Manager

两套方案是冲突的，不能同时共存。

**<span class="under0"> 第一个方案适用于没有X的环境，如：服务器；或者那些完全不需要改动连接的场合。 第二套方案使用于有桌面的环境，特别是笔记本，搬来搬去，网络连接情况随时会变的。 **

他们两个为了避免冲突，又能共享配置，就有了下面的解决方案：

1、当`Network-Manager`发现`/etc/network/interfaces`被改动的时候，则关闭自己（显示为未托管），除非`managed`设置成真。

2、当`managed`设置成真时，`/etc/network/interfaces`，则不生效。 

```
sudo vi /etc/NetworkManager/NetworkManager.conf 
```
将`managed=false`改成`true`，重启一下就可以了。

***********
### ** 参考 **

[Ubuntu 16.04与Win10双系统双硬盘安装图解](https://blog.csdn.net/fesdgasdgasdg/article/details/54183577)
[联想拯救者r720自带win10安装linux（ubuntu）双系统](https://blog.csdn.net/u013036495/article/details/75043228?locationNum=5&fps=1)
[解决Ubuntu16.04下联想R720的无线网卡开启问题及信号不稳定问...](http://tieba.baidu.com/p/5281696783)
[Ubuntu：未找到合法的活动链接](https://www.cnblogs.com/zhaiyf/p/8979975.html)