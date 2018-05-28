---
title: 机器学习(coursera 斯坦福)第三周编程作业
date: 2018-5-28 20:06:45
categories: 机器学习
tags: [Logistic Regression,Regularization]
---

### ** Preface **

本文是机器学习第三周的编程作业答案,完整题目以及代码见[github](https://github.com/iamsail/ML-Stanford/tree/master/homework/third-week)

** 在Octave中运行.m文件,有以下两种方式(假设有文件`orz.m`) **

```
# 一
>> orz

# 二
>> run('orz.m')
```
**************************

### ** sigmoid.m **
![sigmod](/img/机器学习/the-thrid-week-homework-of-ML-Stanford/1.png)

```
function g = sigmoid(z)
%SIGMOID Compute sigmoid function
%   g = SIGMOID(z) computes the sigmoid of z.

% You need to return the following variables correctly 
g = zeros(size(z));

% ====================== YOUR CODE HERE ======================
% Instructions: Compute the sigmoid of each value of z (z can be a matrix,
%               vector or scalar).

g = 1./(1 + exp(-z));


% =============================================================

end
```

*****************

### ** costFunction.m **

![2.png](/img/机器学习/the-thrid-week-homework-of-ML-Stanford/2.png)
![3.png](/img/机器学习/the-thrid-week-homework-of-ML-Stanford/3.png)


```
function [J, grad] = costFunction(theta, X, y)
%COSTFUNCTION Compute cost and gradient for logistic regression
%   J = COSTFUNCTION(theta, X, y) computes the cost of using theta as the
%   parameter for logistic regression and the gradient of the cost
%   w.r.t. to the parameters.

% Initialize some useful values
m = length(y); % number of training examples

% You need to return the following variables correctly 
J = 0;
grad = zeros(size(theta));

% ====================== YOUR CODE HERE ======================
% Instructions: Compute the cost of a particular choice of theta.
%               You should set J to the cost.
%               Compute the partial derivatives and set grad to the partial
%               derivatives of the cost w.r.t. each parameter in theta
%
% Note: grad should have the same dimensions as theta
%

%J = 1 / m * sum(((-y) .* log(sigmoid(X * theta)) - (1 - y) .* log(1 - sigmoid(X * theta))));
J = 1 / m * sum(((-y)' * log(sigmoid(X * theta)) - (1 - y)' * log(1 - sigmoid(X * theta))));
grad = 1 / m * X' * (sigmoid(X * theta) - y);


% =============================================================

end
```
这里要注意一下,在`octave`中,`‘`是转置算符

一个向量的转置将其由行向量转为列向量或者由列向量转换为行向量。矩阵的转置将其行和列交换。在数学上,矩阵 A 的转置表示为 A^T 。在 octave 中转置操作用上引号实现。

** 而算符前面的`.`,表示元素对元素的计算 **

*****************


### ** predict.m **

```

function p = predict(theta, X)
%PREDICT Predict whether the label is 0 or 1 using learned logistic 
%regression parameters theta
%   p = PREDICT(theta, X) computes the predictions for X using a 
%   threshold at 0.5 (i.e., if sigmoid(theta'*x) >= 0.5, predict 1)

m = size(X, 1); % Number of training examples

% You need to return the following variables correctly
p = zeros(m, 1);

% ====================== YOUR CODE HERE ======================
% Instructions: Complete the following code to make predictions using
%               your learned logistic regression parameters. 
%               You should set p to a vector of 0's and 1's
%

result = sigmoid(X * theta);
p = result > 0.5;



% =========================================================================


end
```

*****************

### ** costFunctionReg.m **

![4.png](/img/机器学习/the-thrid-week-homework-of-ML-Stanford/4.png)
![5.png](/img/机器学习/the-thrid-week-homework-of-ML-Stanford/5.png)


```
function [J, grad] = costFunctionReg(theta, X, y, lambda)
%COSTFUNCTIONREG Compute cost and gradient for logistic regression with regularization
%   J = COSTFUNCTIONREG(theta, X, y, lambda) computes the cost of using
%   theta as the parameter for regularized logistic regression and the
%   gradient of the cost w.r.t. to the parameters. 

% Initialize some useful values
m = length(y); % number of training examples

% You need to return the following variables correctly 
J = 0;
grad = zeros(size(theta));

% ====================== YOUR CODE HERE ======================
% Instructions: Compute the cost of a particular choice of theta.
%               You should set J to the cost.
%               Compute the partial derivatives and set grad to the partial
%               derivatives of the cost w.r.t. each parameter in theta

[J , grad] = costFunction(theta, X, y);
J = J + lambda / (2*m) * (sum(theta.^2) - theta(1)^2);
grad = grad + lambda / m * theta;
grad(1) = grad(1) - lambda / m * theta(1);




% =============================================================

end
```