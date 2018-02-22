---
title: 在ubuntu使用zsh
date: 2017-10-04 18:45:30
categories: Linux 
---

### ** 写在前面 **

`zsh`是`shell`的一种,比`bash`更加强大。`zsh`是兼容`bash`的。

查看系统安装了哪些shell

```
cat /etc/shells

```


***************

### ** 安装 **

安装zsh

`sudo apt-get install zsh`

确认是否安装成功
`zsh --version`

设置zsh为默认shell
`sudo chsh -s $(which zsh)`

** 注销重新登录 **
** 注销重新登录 **
** 注销重新登录 **
***************

### ** Oh-My-Zsh **

zsh是shell中的战斗机,但是配置太过复杂,令人望而却步。

[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)就是解决zsh配置的神器。

#### ** 安装 **

```
### via curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

### via wget
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

重启一下终端

***********

#### ** 主题 **

修改配置文件`~/.zshrc`

在配置文件设置主题
`ZSH_THEME="agnoster"`

```
# you might need to install a special Powerline font on your console's host for this to work
# 如果字体乱码

# clone
git clone https://github.com/powerline/fonts.git --depth=1

# install
cd fonts
./install.sh
```

[更多主题](https://github.com/robbyrussell/oh-my-zsh/wiki/External-themes)

***********


#### ** 进一步优化**

(这一步我没遇到)
精简 user@hostname：添加export DEFAULT_USER="username"到`~/.zshrc`中，可以隐藏固定的` user@hostname `信息。

***************

### ** 配置文件 **

```
# ZSH的环境变量
export ZSH=/Users/dawang/.oh-my-zsh
# 主题设置
# 主题列表在 ~/.oh-my-zsh/themes/
# 如果设置为 "random", 每次开启都会是不同的主题
ZSH_THEME="agnoster"
# 如果想要大小写敏感，可以取消注释下面的一行
# CASE_SENSITIVE="true"
# 如果想要连接符不敏感，可以取消注释下面的一行。_ 和 - 将可以互换
# HYPHEN_INSENSITIVE="true"
# 如果不想要自动更新，可以取消注释下面的一行
# DISABLE_AUTO_UPDATE="true"
# 自动更新的时间间隔，单位是天，这里设置 30 天更新一次
export UPDATE_ZSH_DAYS=30
# 如果不想要 ls 命令输出带颜色，可以取消注释下面的一行
# DISABLE_LS_COLORS="true"
# 是否禁止更改终端标题,不要禁止,不然所有终端tab只显示zsh了,而不随着目录的改变而改变显示
# DISABLE_AUTO_TITLE="true"
# 自动纠正命令,不启用,不怎么好用
# ENABLE_CORRECTION="true"
# 按tab键补全命令的时候,如果没什么可补全的就会出现三个红点,更人性化显示，这里我们启用
COMPLETION_WAITING_DOTS="true"
# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# 不要在意这些细节，不需要改动
# DISABLE_UNTRACKED_FILES_DIRTY="true"
# 历史命令日期显示格式
# 有三种方式: "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"，我比较习惯最后那种
HIST_STAMPS="yyyy-mm-dd"
# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder
# Which plugins would you like to load? (plugins can be found in ~/.oh-my-zsh/plugins/*)
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# 插件设置，如果添加太多启动速度会比较慢
plugins=(git autojump)
[[ -s ~/.autojump/etc/profile.d/autojump.zsh ]] && . ~/.autojump/etc/profile.d/autojump.zsh
# 剩下部分比较不常改动 
# User configuration
export PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/TeX/texbin"
# export MANPATH="/usr/local/man:$MANPATH"
source $ZSH/oh-my-zsh.sh
# You may need to manually set your language environment
# export LANG=en_US.UTF-8
# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi
# Compilation flags
# export ARCHFLAGS="-arch x86_64"
# ssh
# export SSH_KEY_PATH="~/.ssh/dsa_id"
# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"

```

***************

### ** 别名设置 **

查看所有的命令别名

`alias` 

`alias | grep git`



设置命令别名

`.zshrc `中添加` alias shortcut='this is the origin command' `一行就相当于添加了别名

***************

### ** 插件 **

```
# Which plugins would you like to load? (plugins can be found in ~/.oh-my-zsh/plugins/*)
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git)
```
#### ** git **

git插件是默认安装好的,更多可以看[这儿](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugin:git)

列举一些常用的别名

g | git
-|-
ga | git add
gaa	| git add --all
gapa | git add --patch
gb | git branch
gba | git branch -a
gbr	| git branch --remote
gcam | git commit -a -m
gcf | git config --list
gco | git checkout
gd | git diff
gf | git fetch
ghh | git help
gl | git pull
glgg | git log --graph --color
gm | git merge
gp | git push
gst | git status

***************

#### ** autojump **

** 这个是神器,强烈推荐 **

安装
```
## 更新源
## sudo apt-get update

## 安装
sudo apt-get install autojump

## 看readme
cat /usr/share/doc/autojump/README.Debian

.zshrc配置文件的最后一行加上. /usr/share/autojump/autojump.sh以使得qutojump生效

```

***************

### ** 一些SHELL命令 **
最常用的查看shell的命令，但不能实时反映当前shell
`echo $SHELL`

环境变量中shell的匹配查找
`env | grep SHELL`

先查看当前shell的pid，再定位到此shell进程
```
$ echo $$
xxx
$ ps -ef | grep xxx

###一条命令即可实现：
$ ps -ef | grep `echo $$` | grep -v grep | grep -v ps
```

***************

### ** 参考 **

[zsh 全程指南](http://wdxtub.com/2016/02/18/oh-my-zsh/)
[终极 Shell](http://macshuo.com/?p=676)
[Plugin:git](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugin:git)
[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)
[查看当前使用的shell](http://www.cnblogs.com/zfc2201/articles/6032292.html)
[zsh下 一些命令行效率工具](https://my.oschina.net/wolx/blog/688447)
[autojump](https://github.com/wting/autojump)
[ Ubuntu16.04LTS安装zsh+oh-my-zsh+autojump](http://blog.csdn.net/shengzhu1/article/details/54590158)
[自动补完不算什么，一键直达目录才是终极神器](https://linux.cn/article-3401-1.html)
[Mac下的效率工具autojump](http://www.barretlee.com/blog/2015/03/30/autojump-in-mac/)
[Autojump使用方法](http://oska874.cf/%E8%AF%B4%E6%98%8E/autojump%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%95.html)
***************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
