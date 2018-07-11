---
title: 图鸭信息科技算法实习生面试
date: 2018-06-26 22:49:30
tags: 面试
password: 0algorithm6,
---
### ** Preface **

昨天中午收到了灵犀科技笔试gg的邮件。然后中午又收到了图鸭信息科技hr的电话,约了面试,这边是做深度学习的。灵犀我是在拉勾上投的,图鸭是在实习僧上投的。

今天中午收到了hr微信上发的消息,晚上7点半面试。

面试持续了50多分钟,接近一个小时。面试官非常非常nice,实力很强,然而我太菜了,可是这样都能面我一个小时,人也很耐心。我很多都没答上,羞愧,蛮不好意思的。面试的时候,面试官也是挑我会的面。

不出意外,是凉凉了。本文是对这次面试的记录。因为面试时间太长,有的内容没能记录下来。

***********************

### ** 面试 **

> 自我介绍。实习项目难点。

> 如果有两个模块(比如流量分析,流量采集. 推广n个模块)共用一个IP(共用一个变量),如何设计。进一步涉及到加锁的问题,高并发

> 数据持久化(避免频繁操作数据库?)

> kaggle比赛,聊了很久。这些比赛,我需要自己好好梳理下。
  svm原理。
  单个模型怎么系统训练,提升的。
  过拟合怎么做的。
  模型融合是怎么做的。(模型融合要在每个模型都不错的情况下,再融合!!!)
  
> 客户端/前端 发起的两个请求,是不是来自同一个机器 (这个问题我也很懵逼,不确定)

> 深度学习(我不会,尴尬)　

> PCA原理(背后的数理知识)
[主成分分析（PCA）原理详解](https://blog.csdn.net/zhongkelee/article/details/44064401)
[主成分分析（Principal components analysis）-最大方差解释](http://www.cnblogs.com/jerrylead/archive/2011/04/18/2020209.html)

> 马尔科夫,　隐马尔科夫

> C++,python怎么样

> 编码中解耦合的方法,设计
[代码耦合是怎么回事呢？](https://www.zhihu.com/question/21386172)
[什么是耦合？解耦合的方法有哪几种？](https://blog.csdn.net/qq_24499615/article/details/77821896)
[解耦合](https://blog.csdn.net/Alex1226/article/details/8840614)


> 进程间通信有哪些方法

> 网络编程待学习
[linux下C/C++网络编程基本：socket实现tcp和udp的例子](https://blog.csdn.net/u012234115/article/details/54142273)
[有什么适合提高 C/C++ 网络编程能力的开源项目推荐？](https://www.zhihu.com/question/20124494)
[C++网络编程(一)](http://www.cnblogs.com/hlxs/archive/2011/09/09/2172351.html)

> 一道算法dp题。有一个二维数组,找出一个子矩阵,使得和最大
[最大子矩阵和](http://www.sail.name/2018/06/29/Maximum-submatrix-sum/)

***********************
学习过程中要多总结,梳理。面试也是查漏补缺的过程。

继续加油!!


***********************

### ** 其他笔试面试　**

后面的笔试面试我就补充到这篇博客,不新开文章了

******************

### ** 大疆 **

虽然投的是机器学习岗位,但是大部分内容都是深度学习相关的,CNN什么的涉及很多,我也需要抓紧补上相关的内容。

#### ** 简答题　**

简答题总共有五个

> 请阐述Adagrad优化方法的优缺点
[梯度下降优化方法总结](http://wowx.info/posts/401226963/)
[[Machine Learning] 梯度下降法的三种形式BGD、SGD以及MBGD](http://www.cnblogs.com/maybe2030/p/5089753.html)

> 请列举在训练深度学习模型中常用的防止过拟合的方法
[深度学习中防止过拟合的方法？](https://zhuanlan.zhihu.com/p/30951658)
[深度学习防止过拟合的方法](https://blog.csdn.net/taoyanqi8932/article/details/71101699)
[机器学习中的范数规则化之（一）L0、L1与L2范数](https://blog.csdn.net/zouxy09/article/details/24971995)
[机器学习中的范数规则化之（二）核范数与规则项参数选择](https://blog.csdn.net/zouxy09/article/details/24972869)

> 请阐述梯度消失产生的原因以及如何解决梯度消失的问题

> 写出Relu, sigmoid, tanh 的公式,谈谈各自的特点

> 请写出LeakyReLU的激活函数的公式,并阐述其相对Sigmoid的激活函数的优缺点

#### ** 选择题　**

这里是对选择题(单选和多选)考点做的一点记录

> RNN,梯度爆炸
[详解机器学习中的梯度消失、爆炸原因及其解决方法](https://blog.csdn.net/qq_25737169/article/details/78847691)
[机器学习总结（二）：梯度消失和梯度爆炸](https://blog.csdn.net/weixin_37933986/article/details/69255863)

> 卷积NN,加入池化层,变换的不变性会保留吗？

> 降维的方法有
　PCA LDA SVD 最小二乘?
[四大机器学习降维算法：PCA、LDA、LLE、Laplacian Eigenmaps](http://dataunion.org/13451.html)
[【机器学习算法系列之三】简述多种降维算法](https://chenrudan.github.io/blog/2016/04/01/dimensionalityreduction.html)


> Xavier

#### ** 编程题　**

> 第一题是一个最大子段和
[leetcode 55. Jump Game-贪心算法](https://blog.csdn.net/happyaaaaaaaaaaa/article/details/51636861)
[LeetCode 55 [Jump Game]](https://www.jianshu.com/p/184428f7895c)

> 第二题
  n个数的序列a[0],a[1].....a[n-1]以及一个数M,从这个数组里面选择三个数,得三个数的和　<= M, 有多少种选择方法。n不超过1000


******************

### ** 第四范式 **

昨天中午(7.10)去食堂吃饭的时候收到了第四范式hr的电话,然后约了今天(7.11)下午3点的面试。

**********************

#### ** 一面 **

面经:

>自我介绍

>了解Linux吗

>linux　杀死任务
	kill 9 杀

>查看pid
       ps -aux | grep "name"

>了解hadoop 和　spark 吗


>用程序实现下面的清洗小程序：假设输入文件每行有5列，要求对输入文件的每一行的第一列加1，对第4列去除空白字符，并输出到文件中。请注意异常处理，如有异常，请直接丢弃，并在标准错误中输出丢弃的总行数。其中：输入和输出都是文件，并且都是按照逗号分隔列，\n分隔行。例如：
```regexp
输入文件内容：
3,string,0,  3 ,2
2,star,9,1,3,5
3,more,2,1,3

输出文件内容
4,string,0,3,2
4,more,2,1,3

标准错误内容
1 error lines.
```


```c++

#include<iostream>
#include<fstream> 
#include<string>
#include <iostream>
#define Max 1002
using namespace std;

int errorLines = 0;

string& trim(string &s)
{
    if (s.empty()) 
    {
        return s;
    }
    s.erase(0,s.find_first_not_of(" "));
    s.erase(s.find_last_not_of(" ") + 1);
    return s;
}


bool handle_error(datas) {
    bool error = false;
    (datas.length != 5)?(error = true):(error = false);
    return error; 
}

string handle_files(string lineData) {
    string datas[] = {};
    datas = lineData.split(',');
    if (!handle_error(datas)) {
        for (int index = 0; index < datas.length; index++ ) {
             if (index == 0) {
                int tempFirstCol = 0;
                try {
                  tempFirstCol = (int)datas[index]++;  
                } catch(int tempFirstCol) {
                  errorLines++;
                  break;
                }
             }
             
             if (index == 3) {
                 trim(datas[index]);
             }
        }
    } else {
        errorLines++;
    }  
    return datas;
}

int main() { 
    string data;
    ifstream file("row.txt"); 
    if (!file.is_open()) { 
        cout << "未成功打开文件" << endl; 
    } 
    
    string result[];
    int i = 0;
    while(getline(myfile,data)) {
       result[i++] = handle_files(data);  
    }  
    string errorInfo = "标准错误内容\n"+ errorLines +"error lines."
    ofstream outfile("data.txt",ios::trunc);
    cout << errorInfo << endl;
    return 0;
}

```



>这个写代码异常处理没做,就是那个int如果不能转成功，不是int
 然后让我改了改

>有什么要问的吗



整个面试大概持续了50分钟左右吧,大部分时间都是我在写代码。 写代码用的这个网站[collabedit](http://collabedit.com/) 。代码写完,整个面试差不多就结束了。面试的是数据智能部的数据挖掘组,估计一面就挂了。

<span class="under0"> ** 这个面试也给我提了醒,要时刻做好面试的准备啊!已经7月了,时间很紧张了。接下来多刷算法题,加强机器学习的公式推导,多看书,多面试总结,记得时常调整简历。　**</span>



***********************
### ** 参考 **
[图鸭信息科技](http://tucodec.com/)
[《编程之法：面试和算法心得》](https://legacy.gitbook.com/book/wizardforcel/the-art-of-programming-by-july/details)


***********************
### ** 优秀面经整理 **
[机器学习算法工程师面试总结](https://blog.csdn.net/hemeinvyiqiluoben/article/details/78745596)
[北美公司面试经验笔记](https://blog.csdn.net/stdcoutzyx/article/details/42041947)


***********************
### ** 大佬博客 **
[zouxy09的专栏](https://blog.csdn.net/zouxy09)

***********************
### ** 刷算法 **
[牛客-在线编程专题](https://www.nowcoder.com/activity/oj)