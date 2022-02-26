---
title: 完整神经网络程序(tensorflow)
date: 2018-7-24 18:05:45
categories: 深度学习
tags: [TensorFlow, Neural Networks]
---

本文是通过tensorflow实现的一个在模拟数据集上训练神经网络,解决二分类问题

******************

```python
import tensorflow as tf
from numpy.random import RandomState


# 定义训练数据batch的大小
batch_size = 8

# 定义神经网络的参数
w1 = tf.Variable(tf.random_normal([2, 3], stddev = 1, seed = 1))
w2 = tf.Variable(tf.random_normal([3, 1], stddev = 1, seed = 1))

# 在shape的一个维度上使用None可以方便使用不同的batch大小
# 在训练时需要把数据分成比较小的batch,但是在测试时,可以一次性使用全部的数据。当数据集比较小的时,这样方便测试,但数据集比较大时，将大量数据
# 放入一个batch可能会导致内存溢出
x = tf.placeholder(tf.float32, shape=(None, 2), name='x-input')
y_ = tf.placeholder(tf.float32, shape=(None, 1), name='y-input')

# 定义神经网络前向传播过程
a = tf.matmul(x, w1)
y = tf.matmul(a, w2)

# 定义损失函数和反向传播算法
cross_entropy = -tf.reduce_mean(y_ * tf.log(tf.clip_by_value(y, 1e-10, 1.0)))
train_step = tf.train.AdamOptimizer(0.001).minimize(cross_entropy)

# 通过随机数生成一个模拟数据集
rdm = RandomState(1)
dataset_size = 128

X = rdm.rand(dataset_size, 2)

# 定义规则给出样本的标签
Y = [[int(x1 + x2 < 1)] for (x1, x2) in X]

with tf.Session() as sess:
    init_op = tf.global_variables_initializer()
    #　初始化变量
    sess.run(init_op)
    # print(sess.run(w1)) 
    # print(sess.run(w2)) 
    '''
    在训练之前神经网络参数值
    w1= [[-0.8113182   1.4845988   0.06532937]
         [-2.4427042   0.0992484   0.5912243 ]]

    w2 = [[-0.8113182 ]
         [ 1.4845988 ]
         [ 0.06532937]]
    '''
    
    # 设定训练轮数
    STEPS = 5000
    for i in range(STEPS):
        # 每次选取batch_size个样本进行训练
        start = (i * batch_size) % dataset_size
        end = min(start + batch_size, dataset_size)
        
        # 通过选取的样本训练神经网络并更新参数
        sess.run(train_step,
                 feed_dict = {x: X[start:end], y_: Y[start:end]})
        if i % 1000 == 0:
            #　每隔一段时间计算在所有数据上的交叉熵并输出
            total_cross_entropy = sess.run(cross_entropy,feed_dict = {x: X, y_: Y})
            print("After %d training step(s),cross entropy on all data is %g" % (i, total_cross_entropy))
            '''
            输出结果
            After 0 training step(s),cross entropy on all data is 0.0674925
            After 1000 training step(s),cross entropy on all data is 0.0163385
            After 2000 training step(s),cross entropy on all data is 0.00907547
            After 3000 training step(s),cross entropy on all data is 0.00714436
            After 4000 training step(s),cross entropy on all data is 0.00578471
            
            交叉熵逐渐变小,说明预测的结果和真实的结果差距越小
            '''
   
    print(sess.run(w1))
    print(sess.run(w2))
    '''
    训练之后的神经网络参数值
    w1 = [[-1.9618274  2.582354   1.6820377]
         [-3.4681718  1.0698233  2.11789  ]]
    w2 = [[-1.8247149]
         [ 2.6854665]
         [ 1.418195 ]]
    '''
```


******************
### ** 参考 **

[《TensorFlow实战Google深度学习框架》](http://www.broadview.com.cn/book/111)


