---
title: 剑指offer-Partition
date: 2018-08-07 16:55:17
categories: 算法
tags: 剑指Offer
---

### ** Preface **

《剑指offer》一书中的`Partition`函数在好些题目中都有出现,思路也是我以前没见过的,记录下。

******************
### ** Partition **

```C++
int Partition(int data[], int length, int start, int end) {
    if (data == NULL || length <= 0 || start < 0 || end >= length) {
        throw "invalid parameters";
    }
    int index = RandomInRange(start, end);
    swap(data[index], data[end]);
    int small = start - 1;
    for (index = start; index < end; index++) {
        if (data[index] < data[end]) {
            small++;
            if (small != index) {
                swap(data[index], data[small]);
            }
        }
    }
    small++;
    swap(data[small], data[end]);
    return small;
}
```
`Partition`函数,所做的工作就是选择一个数字(记为x),将数组分为两部分,比x小的移到数组左边,大的移到右边。这里的x,对应small索引指向的元素,也叫做基准数。

****************

以前我写过一篇快速排序的文章[快速排序](http://www.sail.name/2017/11/30/quick-sort/),利用`partition`又有了新的code

### ** 快速排序 **
```C++
#include <iostream>
#include <exception>
using namespace std;

int RandomInRange(int start, int end)
{
    if (end > start)
    {
        srand(time(NULL));
        return start + rand() % (end - start);
    }
    return start;
}

int Partition(int data[], int length, int start, int end) {
    if (data == NULL || length <= 0 || start < 0 || end >= length) {
        throw "invalid parameters";
    }
    int index = RandomInRange(start, end);
    swap(data[index], data[end]);
    int small = start - 1;
    for (index = start; index < end; index++) {
        if (data[index] < data[end]) {
            small++;
            if (small != index) {
                swap(data[index], data[small]);

            }
        }
    }
    small++;
    swap(data[small], data[end]);
    return small;
}

void quickSort(int data[], int length, int start, int end) {
    if (start == end) {
        return;
    }
    int index = Partition(data, length, start, end);
    if (index > start) {
        quickSort(data, length, start, index -1);
    }
    if (index < end) {
        quickSort(data, length, index+1, end);
    }
}

int main() {
    int test[] = {9, 2, 11, 5, 99, 1};
    int len = sizeof(test) / sizeof(*test);
    quickSort(test, len, 0, len-1);
    for(int i = 0; i < len; i++) {
        cout<<test[i]<<" ";
    }
    cout<<endl;
    return 0;
}

```
