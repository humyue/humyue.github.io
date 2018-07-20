---
layout: post
title:  "超精简图像分类教程"
date:   2018-07-21 8:00:54
categories: Tensorflow
tags: Tensorflow
author: Humy
---
* content
{:toc}

**学习深度学习有一段时间了，今天教给大家自己学会做一个图像识别的实例**




在正式开始之前，首先大家要自己动手去搭建Tensorflow环境(gpu,cpu版均可)，如何搭建请参考我前面的教程。环境搭好过后，就可以往下看了：

####1.收集数据

首先，大家要准备好数据集，至少两类。没有也没关系，博主已经写了一个小程序，帮你们自动去收集。
程序结构如下所示：

![image.png]({{ "/asserts/img/post/2018-7-21/01.png" | prepend: site.baseurl }})

打开`config.py`，具体设置如下所示：

![image.png]({{ "/asserts/img/post/2018-7-21/02.png" | prepend: site.baseurl }})
设置好过后，运行`main.py`:

![运行结果]({{ "/asserts/img/post/2018-7-21/03.png" | prepend: site.baseurl }})
这样，苹果和梨的两类数据就收集好了。

####2.模型训练

模型训练和测试只需要用到两个代码文件，如下所示：

![image.png]({{ "/asserts/img/post/2018-7-21/04.png" | prepend: site.baseurl }})

- `retrain.py`：训练代码
- `test.py`：识别代码

下面具体说一下训练代码`retrain.py`需要配置的地方：

```
--image_dir:设置为刚刚收集的数据集存放的路径，例如‘f:/Test/Image’
--output_graph:表示模型训练完成以后保存的路径，如‘f:/test/output_graph.pb’
--output_labels：表示标签存放的路径，如‘f:/test/output_labels.txt’
--summaries_dir：生成的日志文件路径，可以用tensorboard查看训练过程中生成的图，如‘f:/test/retrain_logs’
--how_many_training_steps：步长，视情况而定，数据少的情况下设为1000步就够了
--model_dir：下载预训练模型保存的地址，可设为‘f:/test/inception_model’
--bottleneck_dir:瓶颈层输出的特征值保存路径，如‘f:/test/bottleneck’
```

设置完，接着就可以运行`retrain.py`，如果没出错的话，会出现刚刚设置的路径（code除外，这个目录是我存放代码的路径）

![image.png]({{ "/asserts/img/post/2018-7-21/05.png" | prepend: site.baseurl }})

####3.模型测试

模型训练好以后，接着就可以运行`test.py`进行识别了，在运行之前，需要对 `test.py`进行一些设置(自行找到对应地方进行设置)：

```
#模型训练后保存的标签路径 
lines = tf.gfile.GFile('F:\\Test\\output_labels.txt').readlines()

#模型训练后保存的模型路径 
with tf.gfile.FastGFile('F:\\Test\\output_graph.pb', 'rb') as f:

#需要测试的图片路径，测试该文件下所有图片 
for root,dirs,files in os.walk('F:\\Test\\code\\test_image'):
```

运行`test.py`:

`F:\\Test\\code\\test_image`路径下只放了下面这张图片：

![u=2443737649,4181581860&fm=200&gp=0.jpg]({{ "/asserts/img/post/2018-7-21/06.jpg" | prepend: site.baseurl }})

运行结果如下所示：

![image.png]({{ "/asserts/img/post/2018-7-21/07.png" | prepend: site.baseurl }})
所以，简单的图像识别实例就完成了。
