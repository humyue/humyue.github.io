---
layout: post
title:  "卷积神经网络中两种Padding方式的介绍"
date:   2018-03-08 10:22:54
categories: Tensorflow
tags: Tensorflow
author: Humy
---
* content
{:toc}

<center class>
    <img src="{{ "/asserts/img/cover/05.jpg" | prepend: site.baseurl }}"/>
</center>




**当我们计算卷积池化后的图像尺寸时，需要注意“VALID”和“SAME”两种Padding对应的输出尺寸计算方式不一样，下面就来说说具体的计算方式**

* 当Padding为“VALID”

这种情况下，当你经过最后一步步长做卷积或池化运算，超出图像边界不会补‘0’，输出的形状为：⌈(W-F+1)/S⌉

* 当Padding为“SAME”

这种情况下，当你经过最后一步步长做卷积或池化运算，超出图像边界补‘0’，输出的形状为：⌈W/S⌉

*注意：W为输入的size，F为卷集核尺寸，S为步长，⌈⌉为向上取整符号。*