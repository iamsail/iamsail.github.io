---
title: SMTP Error Could not connect to SMTP host
date: 2017-04-1 19:53:00
categories: PHP
---
[coalball](https://github.com/iamsail/coalball/tree/gh-pages)除了提供了QQ和易班第三方登录,还实现了邮件注册。

是通过[PHPMailer](https://github.com/PHPMailer/PHPMailer/)实现的。

用于测试的邮箱是163邮箱。

使用的时候遇到了一个错误,大致如下

  ** SMTP Error: Could not connect to SMTP host. **

于是我查询了官方[wiki](https://github.com/PHPMailer/PHPMailer/wiki/Troubleshooting)

![phpmailer-error.png](/img/php/phpmailer-error.png)

无果。

最后在thinkphp论坛的一个帖子发现问题所在

    $mail->Password = '**********';

** 这儿需要填写的不是邮箱的登录密码,而是独立管理密码[管理smtp协议的那个密码(授权码或者独立管理密码)] **

*********************

** 参考 **
- [PHPMailer](https://github.com/PHPMailer/PHPMailer/)
- [关于phpmailer邮件发送失败以及解决办法](http://www.thinkphp.cn/code/1292.html)
- [网易邮箱帮助中心](http://mail.163.com/mailhelp/client.htm)
- [163邮箱如何开启POP3/SMTP/IMAP服务](http://help.163.com/10/0312/13/61J0LI3200752CLQ.html)
- [php+mysql模拟队列发送邮件](http://www.imooc.com/learn/721)

