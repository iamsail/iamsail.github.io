---
title: mac-ssh配置
date: 2018-12-16 14:28:00
categories: Mac
tags: [ssh]
---

### ** Preface **
在windows下面连接服务器有xshell，SecureCRT这些很好的软件可以用。Mac下面没有xshell,其他的一些客户端软件也懒得尝试，所以直接用终端进行管理了。以前在linux下，也是用终端直接ssh，当然遇到了一些问题，比如`ssh空闲一段时间自动断开的问题`。这次解决了一些痛点，做一下记录。

*****************

### ** 痛点解决 **
#### ** 1.登录繁琐 **

ssh登录服务器的命令如下
```
ssh username@ip地址

# 然后输入密码
```

这样的话，每次登录我们需要记住(或者粘贴复制)用户名和密码以及ip地址，是一个不小的负担。如果管理了多台服务器就更累了。

可以通过修改配置文件`/etc/ssh/ssh_config`来解决这个问题

增加如下几行配置
```
Host tx  # tx是short_name，快捷键别名，节省输入时间。
	hostname 111.111.11.111  # ip地址
    user root # 用户名
```

增加后，配置文件相关部分如下
```
Host *
	SendEnv LANG LC_*
	Host tx
	hostname 123.207.83.243
        user root
```

此时连接服务器，执行`ssh tx`,再输入密码即可。

*****************

接下来配置文件`/etc/ssh/ssh_config`再增加如下几行配置

```
# 克隆会话功能 这样每连上一个服务器都会自动在~/.ssh/下创建一个socket文件，下次用相同用户名、端口、主机名进行连接就会自动复用
ControlMaster auto
ControlPath ~/.ssh/%h-%p-%r
ControlPersist yes
```

此时配置文件为

```
Host *
	SendEnv LANG LC_*
	ControlMaster auto
        ControlPath ~/.ssh/%h-%p-%r
        ControlPersist yes
        Compression yes

	Host tx
	hostname 123.207.83.243
        user root
```

解释如下

** <span class="under0"> 多条链接共享 </span>**

如果你需要在多个窗口中打开到同一个服务器的连接，而不想每次都输入用户名，密码，或是等待连接建立，那么你可以配置SSH的连接共享选项，在本地打开你的SSH配置文件，通常它们位于~/.ssh/config，然后添加下面2行(ControlMaster配合ControlPath一起使用), 很多人或许已经是这样配置的。

** <span class="under0">  这里解释下`~/.ssh/config`是针对当前用户的配置，仅对一个用户有效。`/etc/ssh/ssh_config`是对本机所有用户。根据自己情况选择对应的配置文件修改。我修改的是`/etc/ssh/ssh_config`，对所有用户有效。</span>**

```
ControlMaster auto
ControlPath ~/.ssh/%h-%p-%r
```


** <span class="under0"> 长连接 </span>**
如果你发现自己每条需要连接同一个服务器无数次，那么长连接选项就是为你准备的。这样后面再连接的时候就还是不用输入密码。

```
ControlPersist yes
```
打开之后即使关闭了所有的已连接ssh连接，一段时间内也能无需密码重新连接。

```
ControlPersist 4h
```
每次通过SSH与服务器建立连接之后，这条连接将被保持4个小时，即使在你退出服务器之后这条连接依然可以重用，因此，在你下一次(4小时之内)登录服务器时，你会发现连接以闪电般的速度建立完成，这个选项对于通过scp拷贝多个文件提速尤其明显，因为你不在需要为每个文件做单独的认证了。

`Compression`为压缩选项，打开之后加快数据传输速度。

*****************

#### ** 2.证书管理密码 **

这里参考了[如何优雅地连接ssh](https://segmentfault.com/a/1190000000585526)。做下搬运工

** 使用证书来管理连接至少有如下两个好处 **

1.安全，目前生成证书的方式不管是RSA还是DSA无论从位数上还是加密方式上都比自己生成的密码安全许多。
2.方便，有了证书以后你就不用再记忆密码了，系统会自动使用证书跟服务器接驳，这一过程不需要人工干预


使用证书连接ssh也非常简单，首先你得生成一个证书，在shell中输入如下命令
```
ssh-keygen -t rsa -C joyqi -f my-key-file

# -t定义的是加密方式，一般有rsa和dsa两种
# -C定义的是注释，一般也可以不写
# -f定义了输出的证书文件名，不需要写后缀，因为生成的证书包含了公钥和私钥两个文件，它会自动帮你加文件名。
```
我们执行后可以看到如下结果
```
$ ssh-keygen -t rsa -C joyqi -f my-key-file
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in my-key-file.
Your public key has been saved in my-key-file.pub.
The key fingerprint is:
57:75:20:37:e2:53:29:ef:86:09:8e:1b:47:2b:6f:88 joyqi
The key's randomart image is:
+--[ RSA 2048]----+
|            o *o.|
|           ..*.o |
|            +o   |
|          o. ..  |
|        S+.o +   |
|        +.+ o o  |
|       . B   .   |
|      E o o      |
|         .       |
+-----------------+
```

```
$ ls
my-key-file     my-key-file.pub
```
可以在上面的命令执行完成，我们已经得到两个文件`my-key-file`和`my-key-file.pub`。前者就是你的私钥，是由你自己个人保存的，后者是公钥，你需要把它上传到任何你想用这个私钥来登录的服务器上。

ok，现在你需要把公钥文件上传到服务器上，一般我建议用scp命令

```
scp my-key-file.pub loginname@yourdomain.com:.
```
把`loginname`和`yourdomain.com`分别替换为你的登录名和服务器地址。上传完后我们需要告诉服务器，以后处理`loginname`的登录时用公钥来验证，现在最后一次用ssh密码登录你的服务器，并执行如下命令

```
cat my-key-file.pub >> ~/.ssh/authorized_keys
```
在后面我们都用`loginname`来特指你自己的登录名，用`yourdomain.com`来特指你的服务器地址，请自行脑补

其中`my-key-file.pub`是我们刚刚上传的公钥文件名。现在我们还要告诉本机，连接`yourdomain.com`的时候使用`my-key-file`这个私钥来登录

退出ssh连接，回到本地。将刚才生成的`my-key-file`文件拷贝到`~/.ssh`目录下

```
cp my-key-file ~/.ssh/
```
然后编辑`~/.ssh/config`文件，如果没有，就创建一个，在其中写入如下配置内容

```
Host yourdomain.com
     IdentityFile ~/.ssh/my-key-file
```
很简单吧，一看就懂，根据你的需要自行修改。** <span class="under0"> 最后还有一步，别忘了将本地缓存的公钥文件删掉，因为那是你以前没有上传公钥时，缓存的服务器默认公钥，现在你用了自己生成的公钥就得把这个老的记录删掉 </span>**

打开`~/.ssh/known_hosts`文件，找到包含`yourdomain.com`的那一行，将它删掉，然后保存退出

现在，你就可以正常登录服务器了，输入`ssh loginname@yourdomain.com`，第一次登录会出现

```
The authenticity of host 'yourdomain.com (xxx.xxx.xxx.xxx)' can't be established.
RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
Are you sure you want to continue connecting (yes/no)?
```
这是因为你刚才把公钥删掉了，系统在连接本地没有缓存公钥的服务器时会询问下你，输入yes即可，然后你没输入密码就登入了服务器。

此时配置文件`/etc/ssh/ssh_config`如下：
```
Host *
	SendEnv LANG LC_*
	ControlMaster auto
    	ControlPath ~/.ssh/%h-%p-%r
    	ControlPersist yes
        Compression yes
	Host tx
	hostname 123.207.83.243
        user root
	IdentityFile ~/.ssh/my-key-file
```
*****************

#### ** 3.保持ssh不自动断开 **

** ssh空闲一段时间会自动断开，这样可以节省资源。**但是如果让其不自动断开呢，网上的一些文章写得比较模糊不清，把我的方案整理如下：


在客户端中的`/etc/ssh/ssh_config`中去掉注释（如果注释没有，就添加这两句话）并改成这样:
```
ServerAliveInterval 60  
ServerAliveCountMax 60  
```

`ServerAliveInterval 60` 表示每60秒发送一次给服务器，服务器就不会断开了。
`ServerAliveCountMax 60` 表示服务器的请求60次没有响应，就自动断开。
这样就可以维持一个小时。

通过修改服务器的配置也可以,但是不太现实,保持长时间连接,耗资源。就不做介绍。

此时配置文件`/etc/ssh/ssh_config`如下：
```
Host *
	SendEnv LANG LC_*
	ControlMaster auto
    	ControlPath ~/.ssh/%h-%p-%r
    	ControlPersist yes
        Compression yes
        ServerAliveInterval 60
	ServerAliveCountMax 60
	Host tx
	hostname 111.111.11.111
        user root
	IdentityFile ~/.ssh/my-key-file


    # 如果有多台服务器，继续在该文件添加配置即可

	Host do
	hostname 222.222.22.222
	user root
```

*****************

### ** 参考 **
[Mac OS X 平台有哪些好用的 SSH 客户端？](https://www.zhihu.com/question/20541129)
[同一个Mac，配置多个SSH Key](http://shinancao.github.io/2016/12/18/Programming-Git-1/)
[如何优雅地连接ssh](https://segmentfault.com/a/1190000000585526)
[命令行如何 copy 文件内容到剪切板（clipboard）？](https://blog.csdn.net/henryhu712/article/details/84290715)
[解决mac下ssh空闲一段时间自动断开的问题](https://www.cnblogs.com/windyet/articles/7733905.html)
[mac 保持SSH连接](https://www.jianshu.com/p/1c626298028a)
[保持ssh不自动断开](https://blog.phpgao.com/keep_connect_ssh.html)
[ControlPersist自动登录](https://appo.oschina.io/2017/05/28/ControlPersist-for-ssh/)
[利用 ControlPersist 特性自动登陆 SSH 服务器](https://www.hi-linux.com/posts/39001.html)