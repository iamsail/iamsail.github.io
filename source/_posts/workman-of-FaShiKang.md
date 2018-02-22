---
date: 2017-12-02 23:59:40
title: 法师康的工人
categories: [水题]
---
### ** Preface **

本题的题目和答案依次戳 [一](https://github.com/iamsail/algorithm-homework/blob/master/question/theFourthWeek/%E6%B3%95%E5%B8%88%E5%BA%B7%E7%9A%84%E5%B7%A5%E4%BA%BA.md) [二](https://github.com/iamsail/algorithm-homework/blob/master/answer/theFourthWeek/%E6%B3%95%E5%B8%88%E5%BA%B7%E7%9A%84%E5%B7%A5%E4%BA%BA.cpp)。

*****************

### ** 题目 **


三个法师康的工人每天早上6点到工厂开始到三条产品生产线上组装桔子手机。第一个工人在200时刻开始（从6点开始计时，以秒作为单位）在生产线上开始生产，一直到1000时刻。第二个工人，在700时刻开始，在1100时刻结束。第三个工人从1500时刻工作到2100时刻。期间最长至少有一个工人在生产线上工作的连续时间为900秒（从200时刻到1100时刻），而最长的无人生产的连续时间（从生产开始到生产结束）为400时刻（1100时刻到1500时刻）。

你的任务是用一个程序衡量N个工人在N条产品线上的工作时间列表（1≤N≤5000，以秒为单位）。

最长的至少有一个工人在工作的时间段

最长的无人工作的时间段（从有人工作开始计）

输入第1行为一个整数N，第2-N+1行每行包括两个均小于1000000的非负整数数据，表示其中一个工人的生产开始时间与结束时间。输出为一行，用空格分隔开两个我们所求的数。

*****************

### ** 样例输入 **

```
3
200 1000
700 1100
1500 2100
```
### ** 样例输出 **

`900 400`

**************
### ** 题解 **

本题思路挺简单的。先将工人时间排序,开始时间越小越靠前,开始时间相同则结束时间越小的越靠前。
然后遍历的同时,更新求解的值即可。

**************
### ** Code **

```C++
#include <iostream>
#include <algorithm>
#define max(a,b) (a>b)?a:b;
using namespace std;

int n;
struct node{
    int left,right;
}a[5050];

bool cmp(node x,node y){
    if(x.left == y.left) return  x.right < y.right;
    else return x.left < y.left;
}

int main() {
    cin >> n;
    for(int i = 0; i < n; i++){
        cin>>a[i].left>>a[i].right;
    }
    sort(a,a+n,cmp);

    int personTime = a[0].right - a[0].left;
    int noPersonTime = 0;
    int startTime = a[0].left,endTime = a[0].right;

    for(int i = 1; i < n; i++){
        if(a[i].left > endTime){
            noPersonTime =max(noPersonTime,a[i].left - endTime);
            startTime = a[i].left;
        }
        endTime = max(endTime,a[i].right);
        personTime = max(personTime,endTime - startTime);
    }
    cout << personTime <<" "<<noPersonTime<<endl;
    return 0;
}

```
****************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
 