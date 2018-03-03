---
date: 2017-08-01 4:20:40
title: Tow-Sum
categories: [水题]
---
### ** 前言 **
 
本文是对[daily-algorithms](https://github.com/barretlee/daily-algorithms)第一题的记录
 
**********
### ** 题目描述 **
 
 > 本题难度：★
 
 给定一个整数数组，其中有两项之和为一个特定的数字，假设每次 input 只有一个唯一解，不允许两次使用同一个元素，返回这两个数的索引。
 
 比如：
 
 ```js
 给定 nums = [2, 7, 11, 15]，target = 9
 
 由于 nums[0] + nums[1] = 9
 所以返回 [0, 1]
 ```
*********

### ** 答案 **

#### ** 解法一 **

```javascript
const resolveTwoSum = (nums, target) => {
  for (let i = 0; i < nums.length - 1; i++) {
    for (let j = i + 1; j < nums.length; j++) { 
      if (nums[i] + nums[j] === target) {
        return [i,j]; 
      }
    }
  }
}
```
这是很常规的解法,很容易就想出来了

#### ** 解法二 **
```javascript
var twoSum = function(nums, target) {
  var result = [];
  var map = {};
  var temp;
  for (var i = 0, len = nums.length; i < len; i++) {
      temp = target - nums[i];
      if (map[temp] !== undefined) {
          result[0] = map[temp] ;
          result[1] = i;
          return result;
      }
      map[nums[i]] = i;
  }
  return -1;
};
```

借用对象字面量，对 ‘“是否存在另一个数” 与 “当前遍历的数” 之和为 target’ 这个问题进行判断。化 O(n^2) 为 O(n)。
其实就是HashMap

```javascript
var hashMap = {   
    Set : function(key,value){this[key] = value},   
    Get : function(key){return this[key]},   
    Contains : function(key){return this.Get(key) === null?false:true},   
    Remove : function(key){delete this[key]}   
} 
```
**************

### ** 推荐阅读 **

[Hash表](http://www.cnblogs.com/dolphin0520/archive/2012/09/28/2700000.html)
[HashMap的JavaScript简洁实现](http://blog.csdn.net/yaya_soft/article/details/8696779)
