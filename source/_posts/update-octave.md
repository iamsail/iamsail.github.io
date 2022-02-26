---
title: 更新octave
date: 2018-5-26 15:01:45
categories: 机器学习
tags: [octave]
---

### ** Preface **

提交作业的时候报了这个错误

```
error: structure has no member 'message' 
error: called from
     submitWithConfiguration at line 35 column 5
     submit at line 40 column 3
error: evaluating argument list element number 2 
error: called from     
     submitWithConfiguration at line 35 column 5     
     submit at line 40 column 3
```

我的系统是Ubutu16,octave是4.0.0版本。

报这个错误的原因是因为octave4.0.0版本,提交作业的脚本在ubuntu上不是能够很好的工作。所以需要对其进行更新。

************************

### ** 安装 **

```
sudo apt-get install octave
```

### ** 更新 **

```
# 查看当前版本

octave --version

========================

sudo add-apt-repository ppa:octave/stable

sudo apt update

sudo apt-get install octave
```


************************
### ** 参考 **

[Submitting Assignment on Coursera ML in Octave](https://stackoverflow.com/questions/45972413/submitting-assignment-on-coursera-ml-in-octave)