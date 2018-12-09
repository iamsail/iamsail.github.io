---
date: 2017-11-30 15:38:40
title: 快速排序
categories: [算法]
tags: [分治]
---

快速排序（英语：Quicksort），又称划分交换排序（partition-exchange sort），一种排序算法，最早由东尼·霍尔提出。在平均状况下，排序 n个项目要 O(nlogn)}（大O符号）次比较。在最坏状况下则需要O(n^{2})次比较，但这种状况并不常见。事实上，快速排序通常明显比其他 O(nlogn)算法更快，因为它的内部循环（inner loop）可以在大部分的架构上很有效率地被实现出来。

该算法是不稳定的排序算法。

************

### ** 基本思想 **

快速排序使用分治法（Divide and conquer）策略来把一个序列（list）分为两个子序列（sub-lists）。

步骤为：
1.从数列中挑出一个元素，称为"基准"（pivot），
2.重新排序数列，所有比基准值小的元素摆放在基准前面，所有比基准值大的元素摆在基准后面（相同的数可以到任何一边）。在这个分区结束之后，该基准就处于数列的中间位置。这个称为分区（partition）操作。
3.递归地（recursively）把小于基准值元素的子数列和大于基准值元素的子数列排序。
递归到最底部时，数列的大小是零或一，也就是已经排序好了。

************
### ** Code **

```C++
#include<iostream>
using namespace std;
int a[50];
int n;

void quickSort(int left,int right){
		if(left > right)return;

		int temp = a[left];//基准数 
		int i = left, j = right;
		while(i != j){
			
			//注意查找顺序，先从右向左查找 
			while(a[j] >= temp && i < j){
				j--;
			}
			
			//从左向右查找 
			while(a[i] <= temp && i < j){
				i++;
			}

			if( i < j){
				int t = 0;
				t = a[i];
				a[i] = a[j];
				a[j] = t;
			}		
		}

	// 基准数归位 
	a[left] = a[i];
	a[i] = temp;
	
	quickSort(left,i-1);
	quickSort(i+1,right);
}

int main(){
	cin >> n;
	for(int i = 1; i <= n; i++){
		cin >> a[i];
	}
	quickSort(1,n);
	for(int i = 1; i <= n; i++){
		cout << a[i] <<" ";
	}
	return 0; 
}

```
****************
### ** 参考 **
[稳定排序和不稳定排序](https://www.cnblogs.com/codingmylife/archive/2012/10/21/2732980.html)
[快速排序](https://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F)

