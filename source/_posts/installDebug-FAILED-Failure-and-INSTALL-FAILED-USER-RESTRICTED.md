---
title: 小米8->Task :app:installDebug FAILED && INSTALL_FAILED_USER_RESTRICTED:Install canceled by user
date: 2019-07-07 17:05:17
categories: react
tags: react native
---
### ** Preface **

在想把react-native跑在真机上进行开发的时候(模拟器是没有问题的),抛出了这个错:app:installDebug FAILED

![1.jpg](/img/react/INSTALL_FAILED_USER_RESTRICTED/1.jpg)

我一开始搜索查询的关键词是`小米8 > Task :app:installDebug FAILED`

这样查找出来的结果,大多数是让关闭`启用MIUI优化`,还有一些其他的方案,也是没有效果的。

折腾了一两个小时过后,我换了一个query进行搜索,`小米8 Failure [INSTALL_FAILED_USER_RESTRICTED: Install canceled by user]`，立马解决

*********************

### ** 解决方案 **

小米手机：
1）去设置
2）点击更多设置
3）点击开发者选项
4）点击开启"USB安装（允许通过USB安装应用）"

*********************

### ** 总结 **

<span class="under0">学会换个搜索关键词,重新组织下问题描述。</span>

****************
### ** 参考 **
[16、安装APK错误 Failure [INSTALL_CANCELED_BY_USER]](https://blog.csdn.net/qq_30552993/article/details/61414620)
[[Android] Upload package to device fails](https://github.com/facebook/react-native/issues/2720)
[Adb install failure: INSTALL_CANCELED_BY_USER](https://stackoverflow.com/questions/37641670/adb-install-failure-install-canceled-by-user)