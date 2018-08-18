---
title: one
date: 2018-06-26 22:49:30
tags: 面试
password: 0algorithm6,
---

图鸭信息科技算法实习生面试
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

#### ** 面试 **

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

我收到的是Adv测试

#### ** 上机 **

```
考试过程中需要不断同步编辑器中的代码到考试系统环境中，在提交上限次数内（Im3次/Adv5次/Pro10次）可以进行提交验证是否有error并不断修改。
八、考试过程中请不要退出考试系统，否则将视为考试结束。也不要关闭Visual Studio / Eclipse，否则Visual Studio / Eclipse中编写的程序将丢失。也不要在Visual Studio/Eclipse中创建新工程, 可能导致非预期效果。
九、考试有提交次数的限制，达到限制次数而程序仍不正确的，考试不通过。
十、提交程序后，系统会进行简单的验证，并且告诉考试者程序是否正确。注意，此时的结果只是初步判定，正式的判定将会在考试结束后进行，并使用更多的测试用例。
```

三星上机题我的题目是一道图相关的题,里面有七种类型的水管,然后要求能够探测到的数量。我是(8.9去上机的,在南京楚翘城)

挂了,不过三星有三次上机机会,今天(8.10)hr已经联系我了,后面再约时间


#### ** 网上收集到的三星相关算法题 **

[三星ADV考试题](http://www.dongcoder.com/detail-248538.html)
[三星ADV考试题(Tunnel Construction)](http://www.elfsong.cn/%E4%B8%89%E6%98%9Fadv%E8%80%83%E8%AF%95%E5%8E%9F%E9%A2%98%EF%BC%88tunnel-construction%EF%BC%89/)
[codevs4290 二元一次不定方程~（三星）](https://blog.csdn.net/Loi_Seavot/article/details/49407089)

**********************

### ** 丁香园自然语言处理实习生面试 **

>一、岗位信息 
 职位描述：
 1、与NLP算法团队研究和讨论包括但不仅限于知识图谱、信息检索、信息抽取、智能问答、阅读理解等领域的相关理论；
 2、参与算法模型实验及解决方案落地设计；
 3、参与模型测评体验，对相关测评指标跟踪维护；
 任职条件：
 1、 具有计算机科学、统计学、数学、自动化等相关学历及专业背景，本科及以上学历，2019年及以后毕业的在校学生，时间充裕；
 2、 编程基本功扎实，熟悉Python/Java语言，熟悉Linux环境下编程；
 3、 熟悉常规机器学习、深度学习建模、调参、评估的方案；
 4、 具有NLP相关研究/工作的实战经验
 5、 具有团队协作能力，做事耐心仔细，使命必达；
 6、 热爱学习，有钻研精神，乐于成为领域专家；


今天(8.10)下午和丁香园的面试官进行,本来以为要凉,所以面试官最后问我还有什么想问的没有,都没有问的想法了。！！可是面试官最后给我讲了一堆,那边做什么工作,过了约摸不到半小时吧，收到hr电话,面试通过,约了下周三的额杭州现场面,希望能过

#### ** 一面 **



> [ACL 2017 录用论文整理（长文）](http://friskit.me/author/botian/)


> 自我介绍

> 然后聊项目,项目问得很仔细
　1. 看你项目有做qa对的提取,这方面你用到了哪些自然语言的知识呢
　2. 分类器怎么做的   然后这里我最终还没做,尴尬,和面试官讨论了下
　3. 怎么评估分类器的效果
　4. 文本相似度是怎么计算的
　5. 数据有多少条

> 讲一个你熟悉的机器学习方法
　   讲了逻辑回归
　那逻辑回归和其他分类算法相比,有什么优势呢
    没讲出来
  也不是说优势,比如说逻辑斯第和其他分类算法有什么区别,比如svm
    我讲了下kernel
  面试官后来给我讲了,在实践当中,svm更以来我们训练出来的向量,如果向量训练得不好,实际效果挺差的,相反,lr就挺稳的
  
> 还了解自然语言的哪些知识呢
　   我讲了下语义消歧      
  面试官给我讲了下NER什么的
  https://www.paperweekly.site/papers/notes/146
  [自然语言处理 NER？](https://www.zhihu.com/question/63258883)
  [斯坦福大学深度学习与自然语言处理第四讲：词窗口分类和神经网络](http://www.52nlp.cn/%E6%96%AF%E5%9D%A6%E7%A6%8F%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0%E4%B8%8Enlp%E7%AC%AC%E5%9B%9B%E8%AE%B2%E8%AF%8D%E7%AA%97%E5%8F%A3%E5%88%86%E7%B1%BB%E5%92%8C%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C)
  [CS224n: Natural Language Processing with Deep Learning](http://web.stanford.edu/class/cs224n/)  
  [CS224n笔记1 自然语言处理与深度学习简介](http://www.hankcs.com/nlp/cs224n-introduction-to-nlp-and-deep-learning.html)
  [CS224N Natural Language Processing with Deep Learning](https://www.youtube.com/playlist?list=PLU40WL8Ol94IJzQtileLTqGZuXtGlLMP_)
  [斯坦福CS224N深度学习自然语言处理（一）](https://zhuanlan.zhihu.com/p/26259699)  
  [深度学习的自然语言处理（斯坦福cs224n，英语字幕）](https://www.bilibili.com/video/av15892671/)
  [CS224N](https://www.youtube.com/playlist?list=PLqdrfNEc5QnuV9RwUAhoJcoQvu4Q46Lja)
  [深度长文 | 复旦大学肖仰华：领域知识图谱落地实践中的问题与对策](https://mp.weixin.qq.com/s?__biz=MzIwMTc4ODE0Mw==&mid=2247490783&idx=1&sn=d5f9de4a73744941b9efe8bf08a95fce&chksm=96e9c35fa19e4a490d566c478d8debbf2c62f9841b0d47bfbb3d3b0fd0e2473c82ec6a26f347&mpshare=1&scene=1&srcid=081000pUDxNPwA8k178V7vMu&pass_ticket=%2FBNKn965F6CuXgqle0q9CdZCoMGJOp2j8rr4o9m6l%2B58sOHjanFj4AvV3dmLvqXG#rd)

> 还问了一些其他问题,最后问我有什么想问的没有
　就问了下那边主要做什么工作
  丁香园那边算法主要是有两个团队吧,一个是偏向业务的,搜索，推荐什么的,另一个就是我面试官这边,不过最终还是要落地到业务,主要做自然语言处理,知识图谱方向的工作

#### ** 二面 **
今天(8.15)去杭州丁香园去了现场终面。挂了,不过还是很有收获,而且车费也给报销
  


**********************

### ** 银联 **

月初笔试了银联算法工程师的岗位,今天(8.8)收到了邮件13号去合肥面试

#### ** 银联面经收集　**
[银联武汉人工智能开发刚面完，热乎着 ](https://www.nowcoder.com/discuss/91879?type=2&order=0&pos=8&page=1)
[银联内推面试-上海 ](https://www.nowcoder.com/discuss/91893)
[中国银联（凉凉版）数据挖掘 ](https://www.nowcoder.com/discuss/91481)
[银联广州开发面试](https://www.nowcoder.com/discuss/91151)
[银联算法面试，坐标广州，一起来分享面试经验吧](https://www.nowcoder.com/discuss/91040)
[中国银联北京场面经 ](https://www.nowcoder.com/discuss/90934)


>作者：DazzlingQQQ
 链接：https://www.nowcoder.com/discuss/91040
 来源：牛客网
 8月4日下午参加了银联的面试。共两面。
 一面群面，无领导小组讨论，资料是关于最近毒疫苗事件的，给出了一些原因，要求按重要性排序，选出重要性前三的原因，给出相应的措施。一分钟自我介绍和个人观点陈述，20分钟小组讨论，3分钟总结发言。
 基本积极参与，表达自己观点的一面都能过。
 二面1v2的面试，两个面试官，先自我介绍，然后问了一个项目(感觉面试官也不懂，聊不起来，都是我在说。。。)，问了几个基础的机器学习知识（也是简历上写了的.）最后还问了一下考研还是保研，四六级分数。
 面试难度不大，问得很浅，不过有2,3个小问题答得不好。。。。我前面的人都面了半个小时左右，我就十几二十分钟吧，没怎么问，不知道是比较满意，还是凉了。
 祝我好运，希望能拿到offer~ 
 就是介绍一下随机森林，boosting, LR，CNN，随机森林哪里随机，boosting为什么好，CNN为什么好。

>主要提问你对银联的了解程度，比如标志、历史、产品体验和有什么想法。再提问一些比较绕脑的题目，不多就一个！比如你最讨厌的人是谁。

13号高铁晚点三个多小时,没去

***********************
### ** 一些NLP文章 **
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
