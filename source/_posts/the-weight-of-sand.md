---
date: 2017-12-02 13:31:40
title: 沙子的质量
categories: [算法]
tags: [动态规划]
---

### ** 题目 **

本题题目也放在了github上,[戳这儿](https://github.com/iamsail/algorithm-homework/blob/master/question/theThirdWeek/%E6%B2%99%E5%AD%90%E7%9A%84%E8%B4%A8%E9%87%8F.md)

#### ** 描述 **

设有N堆沙子排成一排，其编号为1，2，3，…，N（N< =300）。每堆沙子有一定的数量，可以用一个整数来描述，现在要将这N堆沙子合并成为一堆，每次只能合并相邻的两堆，合并的代价为这两堆沙子的数量之和，合并后与这两堆沙子相邻的沙子将和新堆相邻，合并时由于选择的顺序不同，合并的总代价也不相同，如有4堆沙子分别为 1 3 5 2 我们可以先合并1、2堆，代价为4，得到4 5 2 又合并 1，2堆，代价为9，得到9 2 ，再合并得到11，总代价为4+9+11=24，如果第二步是先合并2，3堆，则代价为7，得到4 7，最后一次合并代价为11，总代价为4+7+11=22；

问题是：找出一种合理的方法，使总的代价最小。输出最小代价。

***************

#### ** 输入格式：**

第一行一个数N表示沙子的堆数N。 第二行N个数，表示每堆沙子的质量。 < =1000

#### ** 输出格式：**

合并的最小代价

***************

#### ** 样例输入 **

4 1 3 5 2

#### ** 样例输出 **

22

****************

### ** 题解 **

刚拿到题的时候,当作了贪心写,结果可想而知。

这里有篇文章讲解了为什么不是贪心,[戳这儿](http://blog.csdn.net/ly59782/article/details/52023732)

用f(i,j)表示将 i 到 j 一段合并所需要的最小代价，枚举中间的断点K转移

sum[i]表示前i个沙子的质量和，那么(l,r)的质量就是sum[r]-sum[l-1]

即`f(i,j)=min{f(i,k)+f(k+1,j)}`

用记忆化搜索(备忘录方法)写起来会比较方便

***************

### ** Code **

```C++
#include<iostream>
#include<cstring>
#define inf 9999999
#define MAX 305
using namespace std;

int n;
int sand[MAX],sum[MAX],f[MAX][MAX];
int dp(int l,int r){
	if(f[l][r] != -1)return f[l][r];
	if(l == r)return 0;
	int ans = inf;
	for(int i = l; i < r; i++){
		ans = min(ans,dp(l,i) + dp(i+1,r));
	} 
	return f[l][r] = (ans + sum[r] - sum[l -1]);
}

int main(){
	cin >> n;
	memset(f,-1,sizeof(f));
	for(int i = 1; i <= n; i++){
		cin >> sand[i];4
		sum[i] = sum[i-1] + sand[i];
	}
	cout<<dp(1,n);
	return 0; 
} 
```
****************
### ** 参考 **

[noip1995石子合并-dp](http://blog.csdn.net/ly59782/article/details/52023732)
[【tyvj1055】沙子合并](http://hzwer.com/575.html)
[动态规划和贪心的本质区别是什么](https://www.zhihu.com/question/32096465)
[贪心法和动态规划法的区别](http://blog.csdn.net/yelbosh/article/details/7649717)

****************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
 