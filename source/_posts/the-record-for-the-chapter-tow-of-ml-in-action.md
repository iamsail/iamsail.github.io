---
title: 《机器学习实战》第二章(KNN)记录
date: 2018-8-11 20:35:45
categories: 机器学习
tags: [KNN,机器学习实战]
mathjax: true
---
### ** Preface **

本文是对《机器学习实战》第二章KNN的一些记录.
完整代码以及数据集见[github](https://github.com/iamsail/machine-learning-in-action)
****************
### ** 图片整理 **

![1.png](/img/机器学习/the-record-for-the-chapter-tow-of-ml-in-action/1.png)
![2.png](/img/机器学习/the-record-for-the-chapter-tow-of-ml-in-action/2.png)
![3.png](/img/机器学习/the-record-for-the-chapter-tow-of-ml-in-action/3.png)

**************
### ** 核心代码 **

```python
"""　k-近邻算法
   
Args:
   inX: 用于分类的输入向量
   dataSet:　输入的训练样本集
   labels:　标签向量
   k: k表示用于选择的最近邻居数目
Returns：
   
"""
def classify0(inX, dataSet, labels, k):
    dataSetsize = dataSet.shape[0]
    
    # 计算距离
    diffMat = tile(inX, (dataSetsize, 1)) - dataSet
    sqDiffMat = diffMat**2
    sqDistances = sqDiffMat.sum(axis=1)
    distances = sqDistances**0.5
    
    sortedDistIndicies = distances.argsort()
    classCount = {}
    
    # 选取距离最近的k个点
    for i in range(k):
        voteIlabel = labels[sortedDistIndicies[i]]
        classCount[voteIlabel] = classCount.get(voteIlabel, 0) + 1
    sortedClassCount = sorted(classCount.items(),
                               key = operator.itemgetter(1), reverse=True)
    return sortedClassCount[0][0]
```

计算向量xA和xB之间的距离

$d =  \sqrt[2]{(xA_0 - xB_0)^2 + (xA_1 - xB_1)^2} $

**************
### ** 归一化 **

在处理不同取值范围的特征值,我们通常采用的方法是将数值归一化,如将取值范围处理为0到1或者-1到1之间。这章书上用到的是如下公式

$newValue = (oldValue - min) / (max - min)$

其中`min`和`max`分别是数据集中的最小特征值和最大特征值,参考代码如下

```python
def autoNorm(dataSet):
    minVals = dataSet.min(0)
    maxVals = dataSet.max(0)
    ranges = maxVals - minVals
    normDataSet = zeros(shape(dataSet))
    m = dataSet.shape[0]
    normDataSet = dataSet - tile(minVals, (m, 1))
    normDataSet = normDataSet / tile(ranges, (m, 1))
    return normDataSet, ranges, minVals
```

这面这个方法叫做** 极差变化法 **。归一化可以提升模型的收敛速度和精度,更多可以看以下链接

[数据标准化/归一化normalization](https://blog.csdn.net/pipisorry/article/details/52247379)
[机器学习中常见的几种归一化方法以及原因](https://blog.csdn.net/UESTC_C2_403/article/details/75804617)
[数据预处理：独热编码（One-Hot Encoding）](https://blog.csdn.net/pipisorry/article/details/61193868)

****************
![4.png](/img/机器学习/the-record-for-the-chapter-tow-of-ml-in-action/4.png)

****************
### ** 参考 **

[python系列】numpy中的tile函数](https://blog.csdn.net/ksearch/article/details/21388985)
[在hexo使用mathjax](http://www.sail.name/2018/05/31/use-mathjax-in-hexo/)