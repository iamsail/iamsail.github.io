---
title: 在Ubuntu中安装CLion
date: 2017-09-18 22:21:17
categories: C++
tags: CLion
---
### ** 写在前面 **

本文是对在Ubuntu安装C++开发环境以及CLion使用的记录。

在windows下面使用CFree,codeblocks之类的软件是集成了gcc之类的,而在linux中需要自己安装GCC和G++。

这里搬运一段[知乎上关于GCC和G++关系的解释](https://www.zhihu.com/question/20940822)

gcc 最开始的时候是 GNU C Compiler, 如你所知，就是一个c编译器。但是后来因为这个项目里边集成了更多其他不同语言的编译器，GCC就代表 the GNU Compiler Collection，所以表示一堆编译器的合集。 g++则是GCC的c++编译器。现在你在编译代码时调用的gcc，已经不是当初那个c语言编译器了，更确切的说他是一个驱动程序，根据代码的后缀名来判断调用c编译器还是c++编译器 (g++)。比如你的代码后缀是*.c，他会调用c编译器还有linker去链接c的library。如果你的代码后缀是cpp, 他会调用g++编译器，当然library call也是c++版本的。当然我说了这么多你可能感到有些混乱，没关系，你就把gcc当成c语言编译器，g++当成c++语言编译器用就是了。

**************

### ** GCC G++ 安装 **
```
sudo apt-get install build-essential
gcc --version

sudo apt-get install g++-version
g++ --version
```
**************

### ** 编译 链接 运行 **

#### ** hello.cpp **
```Ｃ++
#include <iostream>
using namespace std;
int main() {
    cout << "Hello, world" << endl;
    return 0;
}
```

编译hello.cpp
```
$ g++ -c hello.cpp
```
输出结果是一个hello.o文件，这是编译过程的生成的中间文件。-c 表示只编译，不链接。

链接hello.o生成hello.out
```
$ g++ -o hello.out hello.o
```
输出结果是一个hello.out文件，这是最终的可执行文件。-o 表示输出文件，hello.o是上一步生成的.o文件。

当然，前面两步是可以合并执行，直接执行命令
```
$ g++ -o hello.out hello.cpp
```
运行hello.out
```
$ ./hello.out
```
********************

### ** CLion **

在[官网下载](https://www.jetbrains.com/clion/download/)

然后在安装目录下的bin目录打开终端执行

```
./clion.sh
```

即可

****************

### ** 杂 **

如果在clion中编译运行文件有错误,可以考虑以下几点原因


#### ** 1.配置Cmake **
```
  sudo   apt-get install cmake
  然后运用
  whereis  cmake
  whereis  gdb
  获取到路径,填入到Clion的配置中就可以了
```
#### ** 2. **

新建项目时

仅需要改变`Ｃ++ Ｅxecutable`的路径,不需要改变`Ｃ++ Ｌibrary`。




********************

### ** 参考 **

[Clion的安装和使用](http://feixiao.github.io/2015/06/16/clion_1/)
[在ubuntu16.04下安装JetBriansClion](http://blog.csdn.net/u011596455/article/details/53271446)
[在Linux中使用VS Code编译调试C++项目](http://www.cnblogs.com/lidabo/p/5888997.html)
[ubuntu 安装 GCC 和 G++ C++ 开发环境](http://www.cnblogs.com/lidabo/p/5888997.html)


