---
title: 在C++中以回车结束数组(不定长)输入
date: 2017-10-11 17:48:17
categories: C++
---

### ** preface **

本文是对<span class="under0">在C++中以回车结束数组(不定长)输入</span>的记录。

其实这个问题,在遥远的曾经应该是解决过,可是今天却忘了,网上搜索的一些方案也不太靠谱。

这告诉我,一些当时觉得简单的坑,或者刚学习的知识点,如果时间允许,最好还是记录下。

看似慢,实则节约了更多的时间。

**********

直接上代码了,逻辑相当简单。

### ** 定长的数组 **

```C++
#include<iostream>
using namespace std;
int main()
{

    int a[999];
    int i;

    for(i=0;;i++)
    {
        cin>>a[i];
        if(getchar()=='\n') //遇回车结束
            break;
    }
    for(int j=0;j<i+1;j++)
        cout<<a[j]<<" ";
    cout<<endl;
    int test;
    cin >> test;
    cout<<test<<endl;
    return 0;
}
```
**********

### ** 不定长的数组 **

```C++
#include <iostream>
#include <vector>
using namespace std;
int main()
{

    vector<int> a;
    int i;

    for(i=0;;i++)
    {   int tem;
        cin >> tem;
        a.push_back(tem);
        if(getchar()=='\n') //遇回车结束
            break;
    }
    for(int j=0;j<i+1;j++)
        cout<<a[j]<<" ";
    cout<<a.size()<<endl;
    cout<<endl;
    int test;
    cin >> test;
    cout<<test<<endl;
    return 0;
}
```
***********

### ** 参考 **
[c++输入一组整型数据 不知道长度 回车键结束 并将其存入数组当中](http://www.cnblogs.com/banyanqianmian/p/6241602.html)
[学习C++ -> 向量(vector)](http://www.cnblogs.com/mr-wid/archive/2013/01/22/2871105.html)
[c++中vector的用法详解](http://blog.csdn.net/hancunai0017/article/details/7032383)
