---
title: TypeError __init__() got an unexpected keyword argument 'shape'
date: 2018-7-24 09:15:45
categories: 深度学习
tags: [TensorFlow]
---

### ** Preface **

在实践《TensorFlow实战Google深度学习框架》一书中的代码时,遇到了一点问题,做下记录

******************

3.1.2计算图的使用　部分

```python
g1 = tf.Graph()
with g1.as_default():
    v = tf.get_variable("v", initializer=tf.zeros_initializer(shape=[1]))
    
g2 = tf.Graph()
with g2.as_default():
    v = tf.get_variable("v", initializer=tf.ones_initializer(shape=[1])) 
    
with tf.Session(graph = g1) as sess:
    tf.initialize_all_variables().run()
    with tf.variable_scope("", reuse = True):
        print(sess.run(tf.get_variable("v")))
        
with tf.Session(graph = g2) as sess:
    tf.initialize_all_variables().run()
    with tf.variable_scope("", reuse = True):
        print(sess.run(tf.get_variable("v")))        
```

`TypeError: __init__() got an unexpected keyword argument 'shape'`

这里出现这个错误是因为`tensorflow`版本不一致,书上的是旧版本(0.9.0),而我电脑上安装的是1.8.0

```regexp
tf.__version__
'1.8.0'
```
修改为如下代码
```python
g1 = tf.Graph()
with g1.as_default():
     v = tf.get_variable("v", initializer=tf.zeros_initializer()(shape=[1]))

g2 = tf.Graph()
with g2.as_default():
     v = tf.get_variable("v", initializer=tf.zeros_initializer()(shape=[1]))

with tf.Session(graph = g1) as sess:
    tf.initialize_all_variables().run()
    with tf.variable_scope("", reuse = True):
        print(sess.run(tf.get_variable("v")))
        
with tf.Session(graph = g2) as sess:
    tf.initialize_all_variables().run()
    with tf.variable_scope("", reuse = True):
        print(sess.run(tf.get_variable("v")))        
```
这里抛出了一个警告

```
WARNING:tensorflow:From /usr/local/lib/python3.5/dist-packages/tensorflow/python/util/tf_should_use.py:118: initialize_all_variables (from tensorflow.python.ops.variables) is deprecated and will be removed after 2017-03-02.
Instructions for updating:
Use `tf.global_variables_initializer` instead.
```
替换掉`initialize_all_variables`即可

```python
g1 = tf.Graph()
with g1.as_default():
     v = tf.get_variable("v", initializer=tf.zeros_initializer()(shape=[1]))

g2 = tf.Graph()
with g2.as_default():
     v = tf.get_variable("v", initializer=tf.zeros_initializer()(shape=[1]))

with tf.Session(graph = g1) as sess:
	tf.global_variables_initializer().run()
    with tf.variable_scope("", reuse = True):
        print(sess.run(tf.get_variable("v")))
        
with tf.Session(graph = g2) as sess:
	tf.global_variables_initializer().run()
    with tf.variable_scope("", reuse = True):
        print(sess.run(tf.get_variable("v")))  
```

******************
### ** 参考 **

[《TensorFlow实战Google深度学习框架》](http://www.broadview.com.cn/book/111)
[终端命令查看TensorFlow版本号及路径](https://blog.csdn.net/Cloudox_/article/details/78004656)
[TypeError: __init__() got an unexpected keyword argument 'shape'](https://blog.csdn.net/Li_haiyu/article/details/78474831)



