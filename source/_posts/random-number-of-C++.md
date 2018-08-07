---
title: C++随机数
date: 2018-08-07 15:44:17
categories: C++
---

### ** Preface **

本文是对C++中随机数的学习记录

************
计算机的随机数都是由伪随机数，即是由小M多项式序列生成的，其中产生每个小序列都有一个初始值，即随机种子。（注意： 小M多项式序列的周期是65535，即每次利用一个随机种子生成的随机数的周期是65535，当你取得65535个随机数后它们又重复出现了。）
### ** 低于C++11 **

C语言/C++怎样产生随机数：这里要用到的是`rand()`函数, `srand()`函数，C语言/C++里没有自带的`random(int number)`函数。 

#### ** rand() **

功能:随机数发生器
>用法:int rand(void)
所在头文件: stdlib.h
rand()的内部实现是用线性同余法做的，它不是真的随机数，因其周期特别长，故在一定的范围里可看成是随机的。
rand()返回一随机数值的范围在0至RAND_MAX 间。RAND_MAX的范围最少是在32767之间(int)。用unsigned int 双字节是65535，四字节是4294967295的整数范围。0~RAND_MAX每个数字被选中的机率是相同的。
用户未设定随机数种子时，系统默认的随机数种子为1。
rand()产生的是伪随机数字，每次执行时是相同的;若要不同,用函数srand()初始化它。

```c++
#include<iostream>
using namespace std;

int main(){

    for(int i=0;i < 10;i++)
        cout<<rand()<<endl;
    return 0;
}


1804289383
846930886
1681692777
1714636915
1957747793
424238335
719885386
1649760492
596516649
1189641421
```

如果要随机生成一个在一定范围的数
```c++
#include<iostream>
#define random(x) ((rand()% (20 - 10))) + 10
using namespace std;

int main(){

    for(int i=0;i < 10;i++)
        cout<<random(10)<<endl;
    return 0;
}

产生一定范围随机数的通用表示公式 
要取得[a,b)的随机整数，使用(rand() % (b-a))+ a; 
要取得[a,b]的随机整数，使用(rand() % (b-a+1))+ a; 
要取得(a,b]的随机整数，使用(rand() % (b-a))+ a + 1; 
通用公式:a + rand() % n；其中的a是起始值，n是整数的范围。 
要取得a到b之间的随机整数，另一种表示：a + (int)b * rand() / (RAND_MAX + 1)。 
要取得0～1之间的浮点数，可以使用rand() / double(RAND_MAX)。
```
#### ** srand() **

功能:初始化随机数发生器
>用法: void srand(unsigned int seed)
所在头文件: stdlib.h
srand()用来设置rand()产生随机数时的随机数种子。参数seed必须是个整数，如果每次seed都设相同值，rand()所产生的随机数值每次就会一样。

>rand()产生的随机数在每次运行的时候都是与上一次相同的。若要不同,用函数srand()初始化它。可以利用srand((unsigned int)(time(NULL))的方法，产生不同的随机数种子，因为每一次运行程序的时间是不同的。
1)给srand()提供一个种子，它是一个unsigned int类型； 
2)调用rand()，它会根据提供给srand()的种子值返回一个随机数(在0到RAND_MAX之间)； 
3)根据需要多次调用rand()，从而不间断地得到新的随机数； 
4)无论什么时候，都可以给srand()提供一个新的种子，从而进一步“随机化”rand()的输出结果。

```c++
#include<iostream>
#define random(x) ((rand()% (20 - 10))) + 10
using namespace std;

int main(){

    srand((unsigned)time(NULL));
    for(int i=0;i < 10;i++)
        cout<<random(10)<<endl;
    return 0;
}
```
*************
### ** C++11 **

前面提到的`rand`和`srand`使用起来还是比较麻烦的,C++11 中提供的 random 库解决了这一问题，它能让我们方便地生成需要的随机值.

#### ** random库 ** 

随机数引擎类是可以独立运行的随机数发生器，它以均匀的概率生成某一类型的随机数，但无法指定随机数的范围、概率等信息。因此，它也被称为“原始随机数发生器”，由于不能指定生成随机数的范围，它通常不会被单独使用。

随机数分布类是一个需要于随机数引擎类的支持才能运行的类，但是它能根据用户的需求利用随机数引擎生成符合条件的随机数，例如某一区间、某一分布概率的随机数。

所有随机数引擎类都支持的操作如下：

|名称|功能|
|------|------|
|Engine e |	创建一个引擎。|
|Engine e(s) |	创建一个引擎，并用 s 作为种子。|
|e.seed(s) |	使用种子 s 充值 e 的状态。|
|e.min( ), e.max( ) |	e 能生成的最小值和最大值。|
|e.discard(u) |	将 e 推进 u 步（u 的类型为 unsigned long long）|

下表随机数分布类共有的操作：

|名称|功能|
|------|------|
|U u |创建一个分布类 u |
|u(e) |用随机数引擎 e 生成随机数（u 代表随机数分布类）|
|u.min( ) | u 能生成的最小值|
|u.max( ) |	u 能生成的最大值|
|u.reset( ) | 重置 u 的状态，使随后 u 生成的值不受之前的值影响 |

*******************

#### ** 随机非负数——default_random_engine **

`default_random_engine`是一个随机数引擎类。它定义的调用运算符返回一个随机的` unsigned `类型的值。

因此，若想生成 10 个随机非负数并输出，程序可以这么写：

```C++
#include <iostream>
#include <random>
using namespace std;

int main( ){
    default_random_engine e();
    for(int i=0; i<10; ++i)
        cout<<e( )<<endl;
    return 0;
}

```
`default_random_engine`也只是一个伪随机数发生器，如果在运行一次程序，得到结果将还是这几个数。若想令每次运行程序时的生成结果不同，可以为其设置较为随机的种子，比如当前系统的时间。

```C++
#include <iostream>
#include <random>
using namespace std;

int main( ){
    default_random_engine e((unsigned)time(NULL));
    for(int i=0; i<10; ++i)
        cout<<e( )<<endl;
    return 0;
}
```
**************

#### ** 特定范围的非负数——uniform_int_distribution **

`uniform_int_distribution`是一个随机数分布类，也是个模板类，模板参数为生成随机数的类型（不过只能是 `int、unsigned、short、unsigned short、long、unsigned long、long long、unsigned long long` 中的一种）。它的构造函数接受两个值，表示随机数的分布范围（闭区间）。

```C++
#include <random>
#include <iostream>

int main()
{
    std::random_device rd;  // 将用于为随机数引擎获得种子
    std::mt19937 gen(rd()); // 以播种标准 mersenne_twister_engine
    std::uniform_int_distribution<> dis(1, 6);

    for (int n=0; n<10; ++n)
        // 用 dis 变换 gen 所生成的随机 unsigned int 到 [1, 6] 中的 int
        std::cout << dis(gen) << ' ';
    std::cout << '\n';
}
```
更多c++11中的用法看下面的参考链接吧
*************
### ** 参考 **

[std::uniform_int_distribution](https://zh.cppreference.com/w/cpp/numeric/random/uniform_int_distribution)
[C++11 随机数学习](https://blog.csdn.net/luotuo44/article/details/33690179)
[【C++11】随机值获取——random](https://www.jianshu.com/p/05863a00af8d)
[C++ 随机数](https://www.cnblogs.com/growup/archive/2011/06/05/2073301.html)
[C/C++中产生随机数(rand,srand用法)](https://www.cnblogs.com/afarmer/archive/2011/05/01/2033715.html)
[剑指offer里面提到的Partition函数](http://www.voidcn.com/article/p-euckgqfp-hc.html)