---
layout: post
title:  "Window7下Tensorflow安装简述"
date:   2017-07-13 16:30:54
categories: Tensorflow
tags:  Tensorflow
author: Humy
---
* content
{:toc}

<center class>
    <img src="{{ "/asserts/img/cover/19.jpeg" | prepend: site.baseurl }}"/>
</center>




>一、安装 cpu版本的tensorflow

1.首先安装python环境，建议安装python3.5版本的

2.升级pip
`python.exe -m pip install --upgrade pip`

3.安装cpu版本的Tensorflow

```
pip install --upgrade https://storage.googleapis.com/tensorflow/windows/cpu/tensorflow-1.2.1-cp35-cp35m-win_amd64.whl
```
网址最好在官网找最新的

4.安装完成后在导入模块的时候

`import tensorflow as tf`

可能会找不到模块
这是还需要下载下面的插件
[插件下载地址](https://www.microsoft.com/en-us/download/details.aspx?id=53587)
下载完成后就可以运行起来了

5.测试

```
>>>import tensorflow as tf
>>>hello=tf.constant('Hello,TensorFlow!')
>>>sess=tf.Session()
>>>print(sess.run(hello))
Hello,TensorFlow!
```

***

>二、安装 gpu版本的tensorflow

1.假设前面Python环境已经装好了，pip也已经升级

2.安装gpu版本的Tensorflow

```
pip install --upgrade https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-1.2.1-cp35-cp35m-win_amd64.whl
```
安装完之后你试着在python中`import tensorflow as tf`
 会告诉你没有找到 CUDA 和 cuDNN，所以下一步就是安装这两个东西。

3.安装CUDA和cuDnn
安装CUDA之前请确保你的显卡型号支持CUDA,百度一下即可，不支持的话你就只有装cpu版的了

①[下载CUDA](https://developer.nvidia.com/cuda-downloads)
![CUDA下载页面]({{ "/asserts/img/post/2017-7-13/01.png" | prepend: site.baseurl }})

②[cuDnn库下载](https://developer.nvidia.com/cudnn)

③解压cudnn文件，解压目录如下所示

![cuda解压目录]({{ "/asserts/img/post/2017-7-13/02.png" | prepend: site.baseurl }})

**重点来了：将bin目录填入到path环境变量**

4.测试

```
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
a=tf.constant(10)
b=tf.constant(20)
print(sess.run(a+b))
print(tf.__path__)
print(tf.__version__)
```
运行结果如下所示：

![运行结果图]({{ "/asserts/img/post/2017-7-13/03.png" | prepend: site.baseurl }})

**ps:显卡有点渣~~   ^..^**

事实证明：我的显卡装了GPU版本的tensorflow也没用
`
Ignoring visible gpu device (device: 0, name: GeForce GT 720M, pci bus id: 0000:01:00.0) with Cuda compute capability 2.1. The minimum required Cuda capability is 3.0.
`