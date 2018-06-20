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

void build_heap(int arr[], int index, int len) {
    int curParent = arr[index];
    int lChild = 2 * index + 1;
    int rChild = 2 * index + 2;
    int largeIndex = lChild;

    while (lChild < len) { // 有子节点的情况
        if (rChild < len && arr[lChild] < arr[rChild]) {
            largeIndex++;  // 较大孩子的下标
        }

        if (curParent < arr[largeIndex]) {
            //没有将curParent赋值给孩子是因为还要迭代子树，
            //如果其孩子中有大的，会上移，curParent还要继续下移。
            arr[index] = arr[largeIndex];

            index = largeIndex;
            lChild = index * 2 + 1;
            largeIndex = lChild;
        } else {
            lChild = largeIndex;
            break;
        }
    }

    arr[index] = curParent;
}



//void build_heap(int arr[], int index, int len) {
//    int curParent = arr[index];
//    int lChild = 2 * index + 1;
//    int rChild = 2 * index + 2;
//
//    while (lChild < len) { // 有子节点的情况
//        if (rChild < len && arr[lChild] < arr[rChild]) {
//            lChild++;  // 较大孩子的下标
//        }
//
//        if (curParent < arr[lChild]) {
//            //没有将curParent赋值给孩子是因为还要迭代子树，
//            //如果其孩子中有大的，会上移，curParent还要继续下移。
//            arr[index] = arr[lChild];
//
//            index = lChild;
//            lChild = index * 2 + 1;
//        } else {
//            break;
//        }
//    }
//
//    arr[index] = curParent;
//}


void heapsort(int a[], int len) {
    for (int i = len / 2; i >= 0; i--) {
        build_heap(a, i, len);
    }

    for (int i = len -1; i >= 0; i--) {
        swap(a[0], a[i]);

        build_heap(a, 0, i);
    }
}


int main() {
    int a[101], len;
    cin >> len;
    for (int i = 0; i < len; i++) {
        cin >> a[i];
    }
    heapsort(a,len);
    for (int i = 0; i < len; i++) {
        cout << a[i] << " ";
    }
    return 0;
}

```


************************** 

###  ** 参考 **

[图解堆排序](https://www.cnblogs.com/MOBIN/p/5374217.html)
[堆排序C++实现](https://segmentfault.com/a/1190000002466215)
[算法入门：堆排序](https://www.jianshu.com/p/1cfdcee48003)
