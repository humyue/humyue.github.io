---
layout: post
title:  "Tensorfolw使用方法(1)"
date:   2017-08-07 10:14:54
categories: Tensorflow
tags: Tensorflow
author: Humy
---
* content
{:toc}

**笔者目前正在学习Tensorflow框架，在这个系列里，我会详细记录下我学习的过程。前面多是些简单的例子方便理解语法，后面也会多介绍利用Tensorflow运行大型项目，以实践为主**




#### 一、利用梯度下降法拟合线性模型

```py
import tensorflow as tf
import numpy as np

# create data
x_data = np.random.rand(100).astype(np.float32)
y_data = x_data*0.1 + 0.3

Weights = tf.Variable(tf.random_uniform([1], -1.0, 1.0))#初始化权重在-1~1之间
biases = tf.Variable(tf.zeros([1]))#bias初始化为0
y = Weights*x_data + biases

loss = tf.reduce_mean(tf.square(y-y_data))#损失函数
optimizer = tf.train.GradientDescentOptimizer(0.5)
train = optimizer.minimize(loss)

init = tf.global_variables_initializer()
sess = tf.Session()
sess.run(init)          # Very important
for step in range(201):
    sess.run(train)
    if step % 20 == 0:
        print(step, sess.run(Weights), sess.run(biases))
``` 

#### 二、含有两个特征的线性模型

```py
import tensorflow as tf
import numpy as np
#使用 NumPy 生成假数据(phony data), 总共 100 个点.
x_data = np.float32(np.random.rand(2, 100)) # 随机输入,随机生成一个2行100列的矩阵

#x_data权重为1行2列的[0.1,0.2]，bias为0.3
y_data = np.dot([0.100, 0.200], x_data) + 0.300#1行100列


# 构造一个线性模型
b = tf.Variable(tf.zeros([1]))#初始化为0
W = tf.Variable(tf.random_uniform([1, 2], -1.0, 1.0))#返回1x2的矩阵，产生于-1~1之间
y = tf.matmul(W, x_data) + b

# 最小化方差
loss = tf.reduce_mean(tf.square(y - y_data))
optimizer = tf.train.GradientDescentOptimizer(0.5)
train = optimizer.minimize(loss)

# 初始化变量
init = tf.initialize_all_variables()

# 启动图 (graph)
sess = tf.Session()
sess.run(init)

# 拟合平面
for step in range(0, 201):
    sess.run(train)
    if step % 20 == 0:
        print(step, sess.run(W), sess.run(b))
# 得到最佳拟合结果 W: [[0.100  0.200]], b: [0.300]
```

#### 三、Session()的两种建立

```py
import tensorflow as tf

matrix1=tf.constant([[3,3]]) #建立一个一行两列的矩阵
matrix2=tf.constant([[2],
                    [2]])

product=tf.matmul(matrix1,matrix2) #matrix multiply or np.dot(m1,m2)

# 方法一
sess=tf.Session()
result=sess.run(product)

print(result)

#方法二
with tf.Session() as sess:
    result2=sess.run(product)
    print(result2)

```

#### 四、Variables()
        
```py
import tensorflow as tf
state=tf.Variable(0,name="counter")

#定义常量one
one=tf.constant(1)

#定义加法步骤(注:此步并没有直接计算)
new_value=tf.add(state,one)

#将state更新成new_state
update=tf.assign(state,new_value)

#如果定义了Variable,就一定要initialize
init=tf.global_variables_initializer()

with tf.Session() as sess:
    sess.run(init)
    for i in range(3):
        sess.run(update)
        print(sess.run(state))
#输出：
#1
#2
#3
```

#### 五、Placeholder()

```py
import tensorflow as tf
input1=tf.placeholder(tf.float32)
input2=tf.placeholder(tf.float32)

output=tf.matmul(input1,input2)

with tf.Session() as sess:
    result=sess.run(output,feed_dict={input1:[[3,2]],input2:[[4],[5]]})
    print(result)#[[22.]]
```

```py
import tensorflow as tf
x1 = tf.placeholder(dtype=tf.float32, shape=None)
y1 = tf.placeholder(dtype=tf.float32, shape=None)
z1 = x1 + y1

x2 = tf.placeholder(dtype=tf.float32, shape=[2, 1])
y2 = tf.placeholder(dtype=tf.float32, shape=[1, 2])
z2 = tf.matmul(x2, y2)

with tf.Session() as sess:
    # when only one operation to run
    z1_value = sess.run(z1, feed_dict={x1: 1, y1: 2})
    
    # when run multiple operations
    z1_value, z2_value = sess.run(
        [z1, z2],       # run them together
        feed_dict={
            x1: 1, y1: 2,
            x2: [[2], [2]], y2: [[3, 3]]
        })
    print(z1_value)
print(z2_value)

```
运行结果：![结果1]({{ "/img/res_01.jpg" | prepend: site.baseurl }})


***

Tensorflow基本用法就先介绍到这里，后面可能会介绍一些实例







