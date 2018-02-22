---
title: cmder在WSL中方向键失灵
date: 2017-05-24 15:16:30
categories: Linux
---

#### ** 今天才知道WIN10已经内置了linux子系统,也就是[WSL](https://msdn.microsoft.com/commandline/wsl/about) **

Bash on Windows provides developers with a familiar Bash shell and Linux environment in which you can run most Linux command-line tools, directly on Windows, UNMODIFIED, without needing an entire Linux virtual machine!

Bash/WSL allows you to:

Run common command-line utilities such as grep, sed, awk, etc.
Use the Linux-compatible filesystem & hierarchy and access fixed Windows storage mounted under /mnt/...
Run Bash shell scripts and Linux command-line apps. including
** Tools: vim, emacs, tmux **
** Languages: Javascript/node.js, Ruby, Python, C/C++, C# & F#, Rust, Go, etc. **
** Services: sshd, MySQL, Apache, lighttpd, **
Install additional Linux tools using apt
Invoke Windows applications from within Bash
Invoke Linux applications from within Windows!
Bash on Windows runs Ubuntu user-mode binaries provided by Canonical. This means the command-line utilities are the same as those that run within a native Ubuntu environment.

*****************************

作者向来是用cmder写命令的

中途遇到一个问题

#### ** 进入WSL后,上下键翻滚命令失效了 **

** 由于cmder和bash.exe不兼容，如果你直接输入bash ~，那么进入子系统后将无法使用方向键和Home/PageUp/PageDown等键都无法使用 **

网上常见的配置

```
    %windir%\system32\bash.exe -cur_console:p1
```
解决办法,进入setting->Startup->Command line,输入

```
    %windir%\system32\bash.exe ~ -cur_console:p:n
```

cmder + WSL,对我来说很是完美,能满足大部分需求了

*****************************

#### ** 参考/资料 **

- [WSL](https://msdn.microsoft.com/commandline/wsl/about)
- [Linux Bash on Win10 (WSL)在cmder下使用vim时方向键失灵问题解决](http://blog.csdn.net/qxoqx/article/details/54177891)
- [深夜急报，Win10下的Linux子系统之Bash](http://www.cnblogs.com/micro-chen/p/5437316.html)
- [Win下必备利器之Cmder](http://www.cnblogs.com/jadeboy/p/5132423.html)
*******************************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<script type="text/javascript" charset="utf-8" src="http://www.dashangcloud.com/static/ds.js"></script>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
