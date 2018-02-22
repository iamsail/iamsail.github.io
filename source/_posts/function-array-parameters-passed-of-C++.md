---
title: C++函数中数组参数传递
date: 2017-11-30 16:05:17
categories: C++
---

### ** Preface **

因为只是用C++写写算法水题,代码行数鲜有破百的。

很多时候函数之间需要使用到某一个数组时,都偷懒写成全局了。一是因为代码量少,尚还不足以引起混乱,二则是因为有的时候题目测试数据比较大,数组也就开得比较大,可能会导致爆栈(new 是懒得new了)。参考我的[C++内存分配管理](http://www.sail.name/2017/11/11/memory-allocation-of-C++/)。

本文对C++中数组参数的传递做一个记录。

************

### ** 一维数组 **

一维数组比较方便。有数组和指针两种方式,且数组不需要指定大小。

这里就用一段测试代码展示下

```C++
#include<iostream>
using namespace std;

void test(int *a,int b[]){
	cout<< a[2] <<endl;
	cout<< *a <<endl;
	cout<< *a + 2 <<endl;
	cout<<"==========="<<endl;
	cout<<b<<endl;
	cout<<b[1]<<endl;
	cout<<*b<<endl;
	cout<<*b + 2<<endl;
	cout<<*(b + 2)<<endl;
}

int main(){
	int a[] = {1,2,3,4};
	int b[] = {9,8,7,6};
	test(a,b);
	return 0;
}

```

** 输出 **

```
3
1
3
===========
0x24fe30
8
9
11
7
```

在大多数情况下,C++和C一样,也将数组名视为指针。C++将数组名解释为其第一个元素的地址

`cookies == &cookies[0]`


当然也不总是这样的。具体可以看《C++Primer Plus》。最近比较忙,就不展开了。

*************

### ** 二维数组 **

同样也是数组和指针两种方式。

```C++
#include<iostream>
using namespace std;

void test(int **a,int b[][2]){
	cout<<*((int*)a + 3*1 + 1)<<endl;
	cout<<*((int*)a + 3*1)<<endl;
	cout<<*((int*)a)<<endl;
	cout<<"==========="<<endl;
	cout<<b[0][0]<<endl;
	cout<<b[0]<<endl;
	cout<<*b<<endl;
	cout<<*(b+1)<<endl;
} 

int main(){
	int a[3][3];
	int b[2][2] = {{1,2},{3,4}};
	for(int i = 0; i < 3; i++){
		for(int j = 0; j < 3; j++){
			cin >> a[i][j];
		}
	}
	
	test((int**)a,b);
	return 0;
} 
```
** 输入 **

```
1 2 3
4 5 6
7 8 9
```

** 输出 **

```
5
4
1
===========
1
0x24fe30
0x24fe30
0x24fe38
```

将二维数组当作参数的时候，必须指明所有维数大小或者省略第一维的，但是不能省略第二维或者更高维的大小。
也就是在上面的代码中,`test(int **a,int b[2][2])`也是可以的。


这是由编译器原理限制的
** 对于数组 int b[m][n]; 如果要取b[i][j]的值(i>=0 && i<m && 0<=j && j < n)，编译器是这样寻址的，它的地址为：`b + i*n + j`;**

从以上可以看出，如果我们省略了第二维或者更高维的大小，编译器将不知道如何正确的寻址。

而在使用指针时,需要按照如下的方式进行调用

`*((int*)b + n*i + j);`

***********
### ** 参考 **

[C++: 二维数组作函数参数](http://blog.csdn.net/hanpingliang/article/details/3380351)
[C/C++如何传递二维数组？](http://blog.csdn.net/liyongbao1988/article/details/7463481)
[C++,二维数组与指针,二维数组名是不是首地址?](http://blog.csdn.net/sergery/article/details/8046665#reply)

***********
<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
