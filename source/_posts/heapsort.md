---
title: 堆排序
date: 2018-06-20 23:17:00
categories: [算法]
---

###  ** preface **

本文是自己写的堆排序做下记录,不带讲解,没什么参考价值。文末有我看的一些博客的链接。

************************** 
###  ** code（C++） **

```c++
#include <iostream>

using namespace std;
int arrs[] = { 23, 65, 12, 3, 8, 76, 345, 90, 21, 75, 34, 61 };
int arrLen = sizeof(arrs) / sizeof(arrs[0]);

void adjustHeap(int * arrs, int p, int len){
    int curParent = arrs[p];
    int child = 2* p + 1;   //左孩子
    while(child < len){     //没有孩子
        if(child+1<len&&arrs[child]<arrs[child+1]){
            child++;    //较大孩子的下标
        }
        if(curParent<arrs[child]){
            arrs[p]=arrs[child];
            //没有将curParent赋值给孩子是因为还要迭代子树，
            //如果其孩子中有大的，会上移，curParent还要继续下移。
            p=child;
            child=2*p+1;
        }
        else
            break;
    }
    arrs[p]=curParent;
}

void heapSort(int * arrs, int len){
    //建立堆，从最底层的父节点开始
    for(int i = arrLen /2 -1; i>=0; i--)
        adjustHeap(arrs, i, arrLen);
    for(int i = arrLen -1; i>=0; i--){
        int maxEle = arrs[0];
        arrs[0] = arrs[i];
        arrs[i] = maxEle;

        adjustHeap(arrs, 0, i);
    }
}

int main()
{
    heapSort(arrs, arrLen );
    for (int i = 0; i < arrLen; i++)
        cout << arrs[i] << endl;
    return 0;
}

```


************************** 

###  ** 参考 **

[图解堆排序](https://www.cnblogs.com/MOBIN/p/5374217.html)
[堆排序C++实现](https://segmentfault.com/a/1190000002466215)
[算法入门：堆排序](https://www.jianshu.com/p/1cfdcee48003)
