---
title: 机器学习(coursera 斯坦福)第五周编程作业
date: 2018-6-06 09:07:45
categories: 机器学习
tags: [Neural Networks]
---

### ** Preface **

本文是机器学习第五周的编程作业答案记录,完整题目以及代码见[github](https://github.com/iamsail/ML-Stanford/tree/master/homework/fif-week)

此外还记录我在人工智能吧看到的[一篇讲解神经网络的精品帖子](http://tieba.baidu.com/p/3013551686?see_lz=1)的部分搬运。贴吧真是大佬多啊orz

*****************

![6.png](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/6.png)

***************

### ** 作业答案 **

#### ** nnCostFunction.m **

![1.png](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/1.png)
***********
![2.png](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/2.png)
***********
![4.png](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/4.png)
***********
![5.png](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/5.png)



```regexp
function [J grad] = nnCostFunction(nn_params, ...
                                   input_layer_size, ...
                                   hidden_layer_size, ...
                                   num_labels, ...
                                   X, y, lambda)
%NNCOSTFUNCTION Implements the neural network cost function for a two layer
%neural network which performs classification
%   [J grad] = NNCOSTFUNCTON(nn_params, hidden_layer_size, num_labels, ...
%   X, y, lambda) computes the cost and gradient of the neural network. The
%   parameters for the neural network are "unrolled" into the vector
%   nn_params and need to be converted back into the weight matrices. 
% 
%   The returned parameter grad should be a "unrolled" vector of the
%   partial derivatives of the neural network.
%

% Reshape nn_params back into the parameters Theta1 and Theta2, the weight matrices
% for our 2 layer neural network
Theta1 = reshape(nn_params(1:hidden_layer_size * (input_layer_size + 1)), ...
                 hidden_layer_size, (input_layer_size + 1));

Theta2 = reshape(nn_params((1 + (hidden_layer_size * (input_layer_size + 1))):end), ...
                 num_labels, (hidden_layer_size + 1));

% Setup some useful variables
m = size(X, 1);
         
% You need to return the following variables correctly 
J = 0;
Theta1_grad = zeros(size(Theta1));
Theta2_grad = zeros(size(Theta2));

% ====================== YOUR CODE HERE ======================
% Instructions: You should complete the code by working through the
%               following parts.
%
% Part 1: Feedforward the neural network and return the cost in the
%         variable J. After implementing Part 1, you can verify that your
%         cost function computation is correct by verifying the cost
%         computed in ex4.m
%
% Part 2: Implement the backpropagation algorithm to compute the gradients
%         Theta1_grad and Theta2_grad. You should return the partial derivatives of
%         the cost function with respect to Theta1 and Theta2 in Theta1_grad and
%         Theta2_grad, respectively. After implementing Part 2, you can check
%         that your implementation is correct by running checkNNGradients
%
%         Note: The vector y passed into the function is a vector of labels
%               containing values from 1..K. You need to map this vector into a 
%               binary vector of 1's and 0's to be used with the neural network
%               cost function.
%
%         Hint: We recommend implementing backpropagation using a for-loop
%               over the training examples if you are implementing it for the 
%               first time.
%
% Part 3: Implement regularization with the cost function and gradients.
%
%         Hint: You can implement this around the code for
%               backpropagation. That is, you can compute the gradients for
%               the regularization separately and then add them to Theta1_grad
%               and Theta2_grad from Part 2.
%

ylable = eye(num_labels)(y,:);

a1 = [ones(m,1) X];
z2 = a1 * Theta1';
a2 = sigmoid(z2);
a2 = [ones(m,1) a2];
a3 = sigmoid(a2 * Theta2');

% 这里不知道为什么用向量的形式写出来是不对的?
%J = 1 / m * (-ylable' * log(a3) - (1 - ylable') * log(1 - a3));
J = 1 / m * sum( sum( -ylable.* log(a3) -  (1-ylable).*log(1-a3) )); 

% pay attention :" Theta1(:,2:end) " , no "Theta1" .  
regularized = lambda/(2*m) * (sum(sum(Theta1(:,2:end).^2)) + sum(sum(Theta2(:,2:end).^2)) );  
  
J = J + regularized;



delta3 = a3-ylable;            %5000x10  
  
  
delta2 = delta3 * Theta2 ;  
delta2 = delta2(:,2:end);     
  
delta2 = delta2 .* sigmoidGradient(z2);  %5000x25  
  
  
Delta_1 = zeros(size(Theta1));  
Delta_2 = zeros(size(Theta2));  
  
  
Delta_1 = Delta_1 + delta2' * a1 ;    
  
Delta_2 = Delta_2 + delta3' * a2 ;    
  
  
Theta1_grad = 1/m * Delta_1;   
Theta2_grad = 1/m * Delta_2;   
  
  
regularized_1 = lambda/m * Theta1;  
regularized_2 = lambda/m * Theta2;  
  
% j = 0是不需要正则化的
regularized_1(:,1) = zeros(size(regularized_1,1),1);  
regularized_2(:,1) = zeros(size(regularized_2,1),1);  
  
Theta1_grad = Theta1_grad + regularized_1;  
Theta2_grad = Theta2_grad + regularized_2;  
  


% =========================================================================

% Unroll gradients
grad = [Theta1_grad(:) ; Theta2_grad(:)];


end
```

*****************

#### ** sigmoidGradient.m **

![3.png](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/3.png)


```regexp
function g = sigmoidGradient(z)
%SIGMOIDGRADIENT returns the gradient of the sigmoid function
%evaluated at z
%   g = SIGMOIDGRADIENT(z) computes the gradient of the sigmoid function
%   evaluated at z. This should work regardless if z is a matrix or a
%   vector. In particular, if z is a vector or matrix, you should return
%   the gradient for each element.

g = zeros(size(z));

% ====================== YOUR CODE HERE ======================
% Instructions: Compute the gradient of the sigmoid function evaluated at
%               each value of z (z can be a matrix, vector or scalar).


g = sigmoid(z).*(1 - sigmoid(z));

% =============================================================

end
```

*****************

#### ** randInitializeWeights.m **

```regexp
function W = randInitializeWeights(L_in, L_out)
%RANDINITIALIZEWEIGHTS Randomly initialize the weights of a layer with L_in
%incoming connections and L_out outgoing connections
%   W = RANDINITIALIZEWEIGHTS(L_in, L_out) randomly initializes the weights 
%   of a layer with L_in incoming connections and L_out outgoing 
%   connections. 
%
%   Note that W should be set to a matrix of size(L_out, 1 + L_in) as
%   the first column of W handles the "bias" terms
%

% You need to return the following variables correctly 
W = zeros(L_out, 1 + L_in);

% ====================== YOUR CODE HERE ======================
% Instructions: Initialize W randomly so that we break the symmetry while
%               training the neural network.
%
% Note: The first column of W corresponds to the parameters for the bias unit
%


epsilon_init = 0.12;
W = rand(L_out, 1 + L_in) * 2 * epsilon_init − epsilon_init;

% =========================================================================

end
```

****************

### ** 贴吧搬运　**

参考这个帖子,仅供参考[机器学习入门——浅谈神经网络](http://tieba.baidu.com/p/3013551686?see_lz=1)

![7.jpg](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/7.jpg)
![8.jpg](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/8.jpg)
![9.jpg](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/9.jpg)
![10.jpg](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/10.jpg)
![11.jpg](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/11.jpg)
![12.jpg](/img/机器学习/the-fifth-week-homework-of-ML-Stanford/12.jpg)


这里介绍的是计算完一条记录，就马上更新权重，以后每计算完一条都即时更新权重。实际上批量更新的效果会更好，方法是在不更新权重的情况下，把记录集的每条记录都算过一遍，把要更新的增值全部累加起来求平均值，然后利用这个平均值来更新一次权重，然后利用更新后的权重进行下一轮的计算，这种方法叫批量梯度下降(Batch Gradient Descent)。


*****************
### ** 参考 **

[机器学习入门——浅谈神经网络](http://tieba.baidu.com/p/3013551686?see_lz=1)
[machine-learning第五周 上机作业](https://blog.csdn.net/dialoal/article/details/50562244)
[Coursera吴恩达机器学习课程 总结笔记及作业代码——第5周神经网络续](https://blog.csdn.net/qq_27008079/article/details/71833370)