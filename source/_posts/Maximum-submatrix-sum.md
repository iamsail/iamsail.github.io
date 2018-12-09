---
date: 2018-06-29 20:29:40
title: 最大子矩阵和
categories: [算法]
tags: [动态规划]
---

### ** preface **

本文是对[最大子矩阵和](http://acm.zju.edu.cn/onlinejudge/showProblem.do?problemCode=1074)的记录。这题就是对[最大子段和](http://www.sail.name/2017/12/01/maximum-subsegment/)的扩展。

从最大子段和的一维变成了二维数组的多维。我们要做的就是将二维转为1维,转化为更简单的最大子段和求解。

这里转化的思想就是对列值就行累加

比如
```
1 2 -3 
3 4 -5
```

累计变成了`4 6 -8`就从两行变为了一行,利用最大子段和就能求解。　 

********************
### ** 问题如下 **


有一个正整数和负整数组成的NxN矩阵，请编写代码找出元素总和最大的子矩阵。请尝试使用一个高效算法。

给定一个int矩阵mat和矩阵的阶数n，请返回元素总和最大的子矩阵的元素之和。保证元素绝对值小于等于100000，且矩阵阶数小于等于200。

测试样例：

```regexp
3
1 2 -3 
3 4 -5 
-5 -6 -7 

4
0 -2 -7 0
9 2 -6 2
-4 1 -4 1
-1 8 0 -2
```

```regexp
10
15
```
******************

#### ** Code **

```C++
#include <iostream>
#include <string>
#include <cstring>

#define  MAX 1000
using namespace std;

int sum(int a[], int n) {
   // 这里就是求解最大子段和  
   int result = 0, b = 0;
   for (int i = 0; i < n; i++) {
       if (b > 0) {
           b += a[i];
       } else {
           b = a[i];
       }

       if (b > result) {
           result = b;
       }
   }
   return result;
}

int main() {
    int n;
    while(cin >> n) {
        int a[MAX][MAX];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                cin >> a[i][j];
            }
        }
        int arr[MAX];
        int final = 0;

        for (int i = 0; i < n; i++) {　// 以第0,1,2...行为起始行开始叠加
            memset(arr, 0, sizeof(arr));
            for (int j = i; j < n; j++) {
                // 增加行    
                for (int k = 0; k < n; k++) {
                    //　对列值累加    
                    arr[k] += a[j][k];
                }
                final = max(sum(arr, n), final);
            }
        }
        cout<<final<<endl;
    }
    return 0;
}
```



********************

### ** 参考 **

[动态规划：最大子矩阵](https://www.cnblogs.com/GodA/p/5237061.html)
[To the Max](http://acm.zju.edu.cn/onlinejudge/showProblem.do?problemCode=1074)
[最大子段和](http://www.sail.name/2017/12/01/maximum-subsegment/)
[最大子矩阵和的问题](http://kubicode.me/2015/06/23/Algorithm/Max-Sum-in-SubMatrix/)
[[编程题]最大和子矩阵](https://www.nowcoder.com/questionTerminal/840eee05dccd4ffd8f9433ce8085946b)