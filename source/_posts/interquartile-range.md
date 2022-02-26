---
title: IQR(四分位距)
date: 2018-06-16 12:41:00
categories: [统计学]
---
### ** Preface **

读大神kernel的时候,看见一个用IQR处理异常值的方法,本文做下记录

**********************

### ** 四分位数 **

四分位数（Quartile）是统计学中分位数的一种，即把所有数值由小到大排列并分成四等份，处于三个分割点位置的数值就是四分位数。

第一四分位数 (Q1)，又称“较小四分位数”，等于该样本中所有数值由小到大排列后第25%的数字。
第二四分位数 (Q2)，又称“中位数”，等于该样本中所有数值由小到大排列后第50%的数字。
第三四分位数 (Q3)，又称“较大四分位数”，等于该样本中所有数值由小到大排列后第75%的数字。

** 第三四分位数与第一四分位数的差距又称四分位距（InterQuartile Range, IQR）。**

*********************

### ** 异常值　**

**异常值通常被定义为小于$Q_1 - 1.5IQR$ 或大于$Q_2 - 1.5IQR$的值**

#### ** code **

```regexp
# Outlier detection 

def detect_outliers(df,n,features):
    """
    Takes a dataframe df of features and returns a list of the indices
    corresponding to the observations containing more than n outliers according
    to the Tukey method.
    """
    outlier_indices = []
    
    # iterate over features(columns)
    for col in features:
        # 1st quartile (25%)
        Q1 = np.percentile(df[col], 25)
        # 3rd quartile (75%)
        Q3 = np.percentile(df[col],75)
        # Interquartile range (IQR)
        IQR = Q3 - Q1
        
        # outlier step
        outlier_step = 1.5 * IQR
        
        # Determine a list of indices of outliers for feature col
        outlier_list_col = df[(df[col] < Q1 - outlier_step) | (df[col] > Q3 + outlier_step )].index
        
        # append the found outlier indices for col to the list of outlier indices 
        outlier_indices.extend(outlier_list_col)
        
    # select observations containing more than 2 outliers
    outlier_indices = Counter(outlier_indices)        
    multiple_outliers = list( k for k, v in outlier_indices.items() if v > n )
    
    return multiple_outliers   

# detect outliers from Age, SibSp , Parch and Fare
Outliers_to_drop = detect_outliers(train,2,["Age","SibSp","Parch","Fare"])
```

**********************

### ** 参考　**

[四分位距](https://zh.wikipedia.org/wiki/%E5%9B%9B%E5%88%86%E4%BD%8D%E8%B7%9D)
[四分位数](https://zh.wikipedia.org/wiki/%E5%9B%9B%E5%88%86%E4%BD%8D%E6%95%B0)
[python 基于箱型图进行异常值分析](https://blog.csdn.net/u011489887/article/details/78973856)

