---
title: leetcode383-比特位计数
date: 2020-03-22 11:13:01
categories: leetcode
tags: [位运算,动态规划]
---

### ** 题目 **

这是一道`medium`难度的题，本题是[leetcode191-位1的个数](http://www.sail.name/2020/03/22/leetcode-191/)的进阶版。

先看看题目

给定一个非负整数 num。对于 0 ≤ i ≤ num 范围中的每个数字 i ，计算其二进制数中的 1 的数目并将它们作为数组返回。

示例 1:

>输入: 2
输出: [0,1,1]

示例 2:

>输入: 5
输出: [0,1,1,2,1,2]

进阶:

>给出时间复杂度为O(n*sizeof(integer))的解答非常容易。但你可以在线性时间O(n)内用一趟扫描做到吗？
要求算法的空间复杂度为O(n)。
你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 __builtin_popcount）来执行此操作。

********************

### ** 解答 **

### ** 十进制转二进制 **

这是最简单的思路。但是时间复杂度是O(n^2)

```javascript
/**
 * @param {number} num
 * @return {number[]}
 */
var countBits = function(num) {
    let result = [0];
    for (let i = 1; i <= num; i++) {
        let count = 0;
        let n = i;
        while (n) {
            count += n % 2; 
            n = n >> 1;
        }
        result[i] = count;
    }
    return result;
};
```


### ** 动态规划 **

动态规划最重要的是找出状态转移方程

```
十进制  =>    二进制
0      =>    0
1      =>    1
2      =>    10
3      =>    11
4      =>    100
5      =>    101
6      =>    110
7      =>    111
8      =>    1000
9      =>    1001
```

可以得出归纳方程，设 dp(n) 为数字n二进制中1的个数

\begin{cases}
dp(n) = dp(n-1) + 1, n为奇数 \\\\
dp(n) = dp(n/2)， n为偶数
\end{cases}



```javascript
/**
 * @param {number} num
 * @return {number[]}
 */
var countBits = function(num) {
    let result = [0];
    for (let i = 1; i <= num; i++) {
        if (i & 1) {
            result[i] = result[i - 1] + 1;
        } else {
            result[i] = result[i >> 1];
        }
    }
    return result;
};
```

### ** 更简洁的动态规划 **

上面的状态转移方程，其实可以转换为下面的方程。本质上还是一样的
$dp(n) = dp(n/2) + n%2 $, 即$dp(n) = dp(n\>\>1) + (n\&1) $


```javascript
/**
 * @param {number} num
 * @return {number[]}
 */
var countBits = function(num) {
    let result = [0];
    for (let i = 1; i <= num; i++) {
        result.push(result[i >> 1] + (i & 1));
    }
    return result;
};
```

********************

#### ** 参考链接 **

https://leetcode-cn.com/problems/counting-bits/
https://www.szdev.com/blog/Hexo/mathjax-config-and-tutorial/