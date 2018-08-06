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

另外一篇**<span class="under0"> [面经总结博文](http://www.sail.name/2018/06/09/mixed/) </span>**链接贴这儿


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
[深度学习：激活函数的比较和优缺点，sigmoid，tanh，relu](https://blog.csdn.net/u011684265/article/details/78039280)
[人工神经网络有哪些常用的激活函数？](http://sofasofa.io/forum_main_post.php?postid=1000701)
[双曲正切函数](https://baike.baidu.com/item/%E5%8F%8C%E6%9B%B2%E6%AD%A3%E5%88%87%E5%87%BD%E6%95%B0/15469414?fr=aladdin)


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

******************

### ** 广州慧杨 **

今天中午收到了广州[慧杨](http://www.wisefly.cn/)hr的电话,我是做机器学习,深度学习方向的。这家公司是做医疗的,不过最近不招图像方向的,有招NLP方向的。hr让我先做下下面这道题,通过就给面试,记录下:

![面试题](/img/面试/algorithm-intern-interview-of-tucodec/1.jpg)

*****************

策略如下

** 先自定义词典,添加病症作为名词进入其中,以用作后面的分词。如: **

```regexp
肾区叩击痛　n
放散痛　n
...
```

** 分词且做词性标注 **,结合以下规则

1. 如果是`无＋名词 / 无 + 名词　+ ... 多个名词...　+名词`,这些名词所代表的特征是无效的,不相关的
如:
```regexp
无恶心呕吐
无胸闷、心悸
```


2. 如果是`不伴+名词` 或　`不伴+名词+及(和/与)+名词`,这些名词所代表的特征是无效的,不相关的
　　如果是`伴+名词` 或　`伴+名词+及(和/与)+名词`,这些名词所代表的特征是有效的,相关的

3. 如果是`无 + 若干字符　+ 名词`的情况,如
```regexp
无明显诱因出现腹部胀痛
无明显畏寒
```
    这里采用多种策略结合,分配权重的方法来计算是否有效还是无效.
    
    这里我们先基于这些动词(引起,出现,导致...等)构建一个语料库,记做A
    ** 如依据若干字符中是否含有动词,以及若干字符的长度相结合进行判断 **
    result = 0.2 `*`是否含有动词(有则值为1,无则为0) 
    　　　　　+ 　0.4 `*` (所含词　与　A 的文本相似度[这里的文本相似度使用TF-IDF算法])  
    　　　　　+ 　0.3 `*` 若干字符长度是否大于2(是则为1,否则为0)  
    
    比如分类的临界值取0.5,则有
    $ result >= 0.5 $有效;  $ result　< 0.5 $ 无效


慧杨最终没有拿到面试,hr说这个准确率只有80%多,有没有更准确的方法,cnn深度学习做...

**********************

### ** 三星 **

七月中旬在实习僧网站上投了三星研究院的算法实习僧,没几天就收到了回复,当时在从徐州去广州的火车上,和hr约了过几天面试。两天后就收到了北京打过来的面试电话,当时和希言在酒店,就没接。

直到前天三星hr再次联系了我,约了今天上午十点钟的面试,面试电话是十点四十分打过来的,面了二十多分钟,做下记录

>自我介绍

>然后开始聊简历上的项目

>看你简历上写了掌握常见的机器学习算法和理论知识,那就讲一个常见的算法吧

>然后我讲了下LR

>分类和回归有什么区别

>接着讲了kaggle比赛

>聊了下实习经历

>换了一个女面试官

>常用的编程语言

>C++　单纯模式(这里可能说的是单列模式把？听错了？)　工厂模式

>算法题目　一个数组找第k大的数　
快排
有没有效率更高的办法
[算法题（一）--找出数组中第k大的数并输出其下标（数组中的数有重复）](https://blog.csdn.net/jack__frost/article/details/66542526)
[[LeetCode]215 数组第k大的数](https://blog.csdn.net/qq_14821023/article/details/50793468)
[经典算法题：无序整数数组中找第k大的数](https://blog.csdn.net/wangbaochu/article/details/52949443)
[寻找第k大的数](https://www.jianshu.com/p/33ee33ce8699)
[LEETCODE面试题8 第K大的数](https://www.jiuzhang.com/qa/907/)
[无序数组中的第k大元素:快速排序和堆排序](https://juejin.im/post/5adc166bf265da0b9a698b32)
[[编程题]最小的K个数](https://www.nowcoder.com/questionTerminal/6a296eb82cf844ca8539b57c23e6e9bf)


>有什么想问的
这边主要是做什么　　做nlp
部分大概有多少人　一百多人

***********************

**<span class="under0">三星当天下午面试官就给我回复,面试过了,需要参加机试,等待机试时间安排 </span>**



***********************

#### ** 一些NLP文章 **

[文本数据处理的终极指南-[NLP入门]](https://juejin.im/entry/5aa34b10f265da2381553b87)

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
