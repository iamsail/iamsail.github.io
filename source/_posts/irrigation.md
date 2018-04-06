---
date: 2017-12-03 15:31:40
title: 灌溉
categories: [算法]
tags: [贪心,最小生成树,树·图]
---
### ** Preface **

本题的题目和答案依次戳 [一](https://github.com/iamsail/algorithm-homework/blob/master/question/experimentThree-Four/%E7%81%8C%E6%BA%89.md) [二](https://github.com/iamsail/algorithm-homework/blob/master/answer/experimentThree-Four/%E7%81%8C%E6%BA%89.cpp)。

***************

### ** 题目 **

到了旱季农业生产的灌溉就成了一个大问题。为了保证灌溉的顺利，某县政府决定投资为各个村之间建立灌溉管道。

输入第1行包括一个整数N，表示某县的村庄的数量。（3≤N≤100），第2行-结尾为一个N×N的矩阵,表示每个村庄之间的距离。虽然在理论上，他们是N行，每行由N个用空格分隔的数组成，实际上，他们限制在80个字符，因此，某些行会紧接着另一些行。当然，对角线将会是0，因为不会有线路从第i个村到它本身（任何两个村之间的距离都不大于100000）。

输出只有一个，为修建灌溉管道将所有村庄相连在一个灌溉系统里所需的最小管道长度。

*************

### ** 题解 **

** 本题是最小生成树问题。 **常用的算法有`prim`算法和`kruskal`算法。前者的贪心策略是从起点(S集合)开始不断寻找非起点(V集合)的点,找到距离最近的点,然后将该点移入A集合。
本文的代码就是使用的`prim`算法

***************
### ** Code **

```C++
#include <iostream>
using namespace std;
const int maxNumber = 105;

int N;
int a[maxNumber][maxNumber];

int prim(){
    int ans = 0;
   //S集合到V集合最短边的权值,最小距离
    int lowCost[maxNumber] = {0};
   //存放顶点,为S集合中距离V集合中j顶点最近的顶点
    int closest[maxNumber] = {0}; 
    bool s[maxNumber];//S集合

    s[1] = true;
   //初始化
    for(int i = 2; i <= N; i++){
        lowCost[i] = a[1][i];
        closest[i] = 1; 
		s[i] = false;
    }

    for(int i = 1; i < N; i++){
        int min = 99999999;
        int j = 1;
        //循环除最初起点的所有顶点
        for(int k = 2; k <= N; k++){
            if((!s[k]) && lowCost[k] < min){
                min = lowCost[k];
                j = k;
            }
        }
        //最优解
		cout<<j<<"  "<<closest[j]<<endl;
        s[j] = true;
        ans += min;
        //S集合加入新顶点后,更新最小距离和顶点
        for(int k = 2; k <= N; k++){
            if(a[j][k] < lowCost[k] && (!s[k])){
                lowCost[k] = a[j][k];
                closest[k] = j;
            }
        }
    }
    return ans;

}

int main() {
    cin >> N;
    for(int i = 1; i <= N; i++){
        for(int j = 1; j <= N; j++){
            cin >> a[i][j];
        }
    }

    cout << prim() <<endl;
    return 0;
}
```

### ** 测试数据 **

#### ** 输入 **
```
4
0 4 9 21
4 0 8 17
9 8 0 16
21 17 16 0
```
#### ** 输出 **
```
2  1
3  2
4  3
28
```
***************
### ** 参考 **

[普里姆算法](https://zh.wikipedia.org/wiki/%E6%99%AE%E6%9E%97%E5%A7%86%E7%AE%97%E6%B3%95)
