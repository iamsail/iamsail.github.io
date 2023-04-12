---
title: 机器学习(coursera 斯坦福)第二周编程作业
date: 2018-6-02 18:40:45
categories: 机器学习
tags: [Linear Regression]
---

### ** Preface **

本文是机器学习第二周的编程作业答案,完整题目以及代码见[github](https://github.com/iamsail/ML-Stanford/tree/master/homework/second-week)

*****************
### ** warmUpExercise.m **

```regexp
function A = warmUpExercise()
%WARMUPEXERCISE Example function in octave
%   A = WARMUPEXERCISE() is an example function that returns the 5x5 identity matrix

A = [];
% ============= YOUR CODE HERE ==============
% Instructions: Return the 5x5 identity matrix 
%               In octave, we return values by defining which variables
%               represent the return values (at the top of the file)
%               and then set them accordingly. 

A = eye(5);

% ===========================================

end
```
******************
### ** computeCost.m　**

```regexp

function J = computeCost(X, y, theta)
%COMPUTECOST Compute cost for linear regression
%   J = COMPUTECOST(X, y, theta) computes the cost of using theta as the
%   parameter for linear regression to fit the data points in X and y

% Initialize some useful values
m = length(y); % number of training examples

% You need to return the following variables correctly 
J = 0;

% ====================== YOUR CODE HERE ======================
% Instructions: Compute the cost of a particular choice of theta
%               You should set J to the cost.
J = 1 / (2*m) * sum((X * theta - y).^2);


% =========================================================================

end
```

******************
### ** gradientDescent.m　**

```regexp
function [theta, J_history] = gradientDescent(X, y, theta, alpha, num_iters)
%GRADIENTDESCENT Performs gradient descent to learn theta
%   theta = GRADIENTDESCENT(X, y, theta, alpha, num_iters) updates theta by 
%   taking num_iters gradient steps with learning rate alpha

% Initialize some useful values
m = length(y); % number of training examples
J_history = zeros(num_iters, 1);

for iter = 1:num_iters

    % ====================== YOUR CODE HERE ======================
    % Instructions: Perform a single gradient step on the parameter vector
    %               theta. 
    %
    % Hint: While debugging, it can be useful to print out the values
    %       of the cost function (computeCost) and gradient here.
    %
    temp=X'*(X*theta-y);
    theta=theta-1/m*alpha*temp;

    % ============================================================

    % Save the cost J in every iteration    
    J_history(iter) = computeCost(X, y, theta);

end

end

```

*****************
### ** featureNormalize.m　**

```
function [X_norm, mu, sigma] = featureNormalize(X)
%FEATURENORMALIZE Normalizes the features in X 
%   FEATURENORMALIZE(X) returns a normalized version of X where
%   the mean value of each feature is 0 and the standard deviation
%   is 1. This is often a good preprocessing step to do when
%   working with learning algorithms.

% You need to set these values correctly
X_norm = X;
mu = zeros(1, size(X, 2));
sigma = zeros(1, size(X, 2));

% ====================== YOUR CODE HERE ======================
% Instructions: First, for each feature dimension, compute the mean
%               of the feature and subtract it from the dataset,
%               storing the mean value in mu. Next, compute the 
%               standard deviation of each feature and divide
%               each feature by it's standard deviation, storing
%               the standard deviation in sigma. 
%
%               Note that X is a matrix where each column is a 
%               feature and each row is an example. You need 
%               to perform the normalization separately for 
%               each feature. 
%
% Hint: You might find the 'mean' and 'std' functions useful.
%       

n = size(X_norm, 2);
for i=1:n
  X_norm(:,i)=(X_norm(:,i)- mean(X_norm(:,i)))/ std(X_norm(:,i));
end

% ============================================================

end
```

*****************

### ** computeCostMulti.m　**

```regexp
function J = computeCostMulti(X, y, theta)
%COMPUTECOSTMULTI Compute cost for linear regression with multiple variables
%   J = COMPUTECOSTMULTI(X, y, theta) computes the cost of using theta as the
%   parameter for linear regression to fit the data points in X and y

% Initialize some useful values
m = length(y); % number of training examples

% You need to return the following variables correctly 
J = 0;

% ====================== YOUR CODE HERE ======================
% Instructions: Compute the cost of a particular choice of theta
%               You should set J to the cost.

J = 1/(2*m)*sum((X*theta-y).^2);

% =========================================================================

end
```

*******************

### ** gradientDescentMulti.m　**

```regexp
function [theta, J_history] = gradientDescentMulti(X, y, theta, alpha, num_iters)
%GRADIENTDESCENTMULTI Performs gradient descent to learn theta
%   theta = GRADIENTDESCENTMULTI(x, y, theta, alpha, num_iters) updates theta by
%   taking num_iters gradient steps with learning rate alpha

% Initialize some useful values
m = length(y); % number of training examples
J_history = zeros(num_iters, 1);

for iter = 1:num_iters

    % ====================== YOUR CODE HERE ======================
    % Instructions: Perform a single gradient step on the parameter vector
    %               theta. 
    %
    % Hint: While debugging, it can be useful to print out the values
    %       of the cost function (computeCostMulti) and gradient here.
    %

temp=X'*(X*theta-y);
    theta=theta-1/m*alpha*temp;

    % ============================================================

    % Save the cost J in every iteration    
    J_history(iter) = computeCostMulti(X, y, theta);

end

end
```

*******************


### ** 　**

![1.png](/img/机器学习/the-second-week-homework-of-ML-Stanford/1.png)

### ** ex1_multi.m ** 

```regexp
% Plot the convergence graph
figure;
plot(1:numel(J_history), J_history, '-b', 'LineWidth', 2);
xlabel('Number of iterations');
ylabel('Cost J');

% Compare learning rate
hold on;
alpha = 0.03;
theta = zeros(3, 1);
[theta, J_history1] = gradientDescentMulti(X, y, theta, alpha, num_iters);
plot(1:100, J_history1(1:100), 'r', 'LineWidth', 2);

hold on;
alpha = 0.1;
theta = zeros(3, 1);
[theta, J_history2] = gradientDescentMulti(X, y, theta, alpha, num_iters);
plot(1:100, J_history2(1:100), 'g', 'LineWidth', 2);

% Display gradient descent's result
fprintf('Theta computed from gradient descent: \n');
fprintf(' %f \n', theta);
fprintf('\n');

```
*****************

### ** normalEqn.m **

```regexp
function [theta] = normalEqn(X, y)
%NORMALEQN Computes the closed-form solution to linear regression 
%   NORMALEQN(X,y) computes the closed-form solution to linear 
%   regression using the normal equations.

theta = zeros(size(X, 2), 1);

% ====================== YOUR CODE HERE ======================
% Instructions: Complete the code to compute the closed form solution
%               to linear regression and put the result in theta.
%

% ---------------------- Sample Solution ----------------------

theta = pinv(X' * X) * X' * y;

% -------------------------------------------------------------
% ============================================================

end
```
*****************
### ** 参考 **

[Coursera-AndrewNg(吴恩达)机器学习笔记——第二周编程作业（线性回归）](https://www.cnblogs.com/LoganGo/p/8532018.html)
[Linear regression with multiple variables(多特征的线型回归)算法实例_梯度下降解法(Gradient DesentMulti)以及正规方程解法(Normal Equation)](http://www.cnblogs.com/douzujun/p/5815357.html)
[机器学习第2周编程作业](https://blog.csdn.net/senketh/article/details/52049933)