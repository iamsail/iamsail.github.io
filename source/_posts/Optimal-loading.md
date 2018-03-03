---
date: 2017-12-03 14:30:40
title: 最优装载问题
categories: [算法]
tags: [贪心]
---
### ** 问题描述 **

![1.png](/img/algorithm/Optimal-loading/1.png)

****************
### ** 题解 **

因为要尽可能多的集装箱上船,且轮船的载重有限, ** <span class="under0"> 故贪心策略是:重量轻的优先上船 </span>**

****************

### ** Code **

```C++
#include<iostream>
#include<algorithm>
using namespace std;

struct node{
	int weight;
	bool get = false;//是否上船 
	int index; //存下标 
}a[2017]; 

bool cmp(node x,node y){
    //质量轻的排前面
	if(x.weight <= y.weight)return true;
	return false;
}

int main(){
	int n,c;//集装箱数量,轮船载重量
	cin >> n>>c;
	for(int i = 0; i < n; i++){
		cin>>a[i].weight;
		a[i].index = i + 1;
	} 
	sort(a,a+n,cmp);
	int sumWeight = 0;
	int count = 0;
	for(int i = 0; i < n && a[i].weight <= c ;i++){
		a[i].get = true;
		sumWeight += a[i].weight;
		count++;
		c -= a[i].weight;
	}
	cout<<"箱子个数  总重量  "<<count<<"  "<<sumWeight<<endl; 
	// 这个是用来存储下标的数组,打印出标准格式 
	int b[2017] = {0}; 
	for(int i = 1; i <=n && a[i-1].get ; i++){
		b[a[i-1].index] = 1;
	} 
	//打印标准格式
	cout<<"(";
	for(int i = 1; i <=n ; i++){
		if(b[i] == 1){
			cout<<1<<" ";
		}else{
			cout<<0<<" ";
		}
	}
	cout<<")";
	return 0;
} 
```
### ** 测试数据 **

#### ** 输入 **
```
8 400
100 200 50 90 150 50 20 80
```
#### ** 输出 **
```
箱子个数  总重量  6  390
(1 0 1 1 0 1 1 1 )
```
