---
title: vector学习
date: 2017-10-13 21:02:17
categories: C++
---
## ** preface **

本文是对C++,`STL`中的`vector`学习记录。

以后与`vector`相关的内容更新在此处。仅供参考。

文章尾部有一些演示代码片段

*************

## ** About **

向量` vector `是一种对象实体, 能够容纳许多其他类型相同的元素, 因此又被称为容器。 与`string`相同, `vector `同属于`STL(Standard Template Library, 标准模板库)`中的一种自定义的数据类型, 可以广义上认为是数组的增强版。
    
在使用它时, 需要包含头文件 `vector`
`#include<vector>`

`vector `容器与数组相比其优点在于它能够根据需要随时自动调整自身的大小以便容下所要放入的元素。此外,` vector `也提供了许多的方法来对自身进行操作。
************


## ** 成员函数 **

[详细请看这儿](http://zh.cppreference.com/w/cpp/container/vector)

以下列举一些我觉得常用的


### ** 元素访问 **

函数名|作用
-|-
at|访问指定的元素，同时进行越界检查 
operator[]|访问指定的元素 
front|访问第一个元素 
back|访问最后一个元素 
data|返回指向内存中数组第一个元素的指针 

***********

### ** 容量 **

函数名|作用
-|-
empty|检查容器是否为空 
size|返回容纳的元素数 
max_size|返回可容纳的最大元素数 
reserve|预留存储空间 
capacity|返回当前存储空间能够容纳的元素数 

****************

### ** 修改器 **

函数名|作用
-|-
clear|清除内容 
insert|插入元素 
erase|擦除元素 
push_back|将元素添加到容器末尾 
pop_back|移除末元素 
resize|改变容器中可存储元素的个数 
swap|交换内容 

***********

## ** 练习代码 **

### ** 一维数组 **

```C++
#include <iostream>
#include <vector>
using namespace std;

// vector 学习
int main() {
    vector<int> a;

    cout<<a.empty()<<endl;

    for(int i=0;;i++)
    {
        int tem;
        cin >> tem;
        a.push_back(tem);
        if(getchar()=='\n') //遇回车结束
            break;
    }

    for(int j=0;j<a.size();j++)
        cout<<a[j]<<" ";

    cout<<a.empty()<<endl;
    return 0;
}

```
***********

### ** 二维数组 **

```C++
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<vector<int>> a;
    int M=5,N=5;
    a.resize(M);
    for(int i = 0;i < M;i++)
        a[i].resize(N);

    for(int i = 0; i < M;i++){
        for(int j = 0; j < N;j++){
            a[i][j]= i + j;
        }
    }

    for(int i = 0; i < M;i++){
        for(int j = 0; j < N;j++){
            cout<<a[i][j]<<" ";
        }
        cout<<endl;
    }
    return 0;
}
```


***********

## ** 参考 **

[ C++中vector用法详解](http://blog.csdn.net/yas12345678/article/details/52601593)
[std::vector](http://zh.cppreference.com/w/cpp/container/vector)
[学习C++ -> 向量(vector)](http://www.cnblogs.com/mr-wid/archive/2013/01/22/2871105.html)

***********
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
