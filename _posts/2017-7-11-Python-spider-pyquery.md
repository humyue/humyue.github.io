---
layout: post
title:  "Python爬虫之PyQuery解析库的使用"
date:   2017-07-11 18:30:54
categories: Python
tags:  Pyquery
author: Humy
---
* content
{:toc}

*本文为笔者根据教程记录笔记，仅供学习试用*
>PyQuery解析库跟BeautifulSoup解析库一样都是方便我们解析文档的，但是PyQuery解析库跟JS的框架JQuery很相似，如果之前接触过JQuery的话，再学习这个就没有什么学习成本了。




### 1.初始化
* 字符串初始化
```
html = '''
<div>
    <ul>
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
print(doc('li'))
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-a85be79a6386fac0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* URL初始化
```
from pyquery import PyQuery as pq
doc = pq(url='http://www.baidu.com')
print(doc('head'))
```
运行结果：

![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-23502991b9b5ebce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 文件初始化
```
from pyquery import PyQuery as pq
doc = pq(filename='demo.html')
print(doc('li'))
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-a85be79a6386fac0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2.基本CSS选择器
```
html = '''
<div id="container">
    <ul class="list">
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
print(doc('#container .list li'))
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-0679bb205f2751b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3.查找元素
* 子元素
```
html = '''
<div id="container">
    <ul class="list">
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
items = doc('.list')
print(type(items))
print(items)
lis = items.find('li')
print(type(lis))
print(lis)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-0cdd7cdc9f6941f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
lis = items.children()
print(type(lis))
print(lis)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-8952c0a329bbc416.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
lis = items.children('.active')
print(lis)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-e2ea1493ee4424fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 父元素
```
html = '''
<div id="container">
    <ul class="list">
         <li class="item-0">first item</li>
         <li class="item-1"><a href="link2.html">second item</a></li>
         <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
         <li class="item-1 active"><a href="link4.html">fourth item</a></li>
         <li class="item-0"><a href="link5.html">fifth item</a></li>
     </ul>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
items = doc('.list')
container = items.parent()
print(type(container))
print(container)
```
运行结果：
![运行结果](http://upload-images.jianshu.io/upload_images/2896168-597e737f5d6249be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
items = doc('.list')
parents = items.parents()
print(type(parents))
print(parents)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-300c74b71d28ae16.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
parent = items.parents('.wrap')
print(parent)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-98658ec91fa15637.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 兄弟元素
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('.list .item-0.active')
print(li.siblings())
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-e889b7907f813d4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('.list .item-0.active')
print(li.siblings('.active'))
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-a1e1ad60ce412b0b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4.遍历
* 单个元素
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('.item-0.active')
print(li)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-60b9c1d82ff753a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 多个元素
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
lis = doc('li').items()
print(type(lis))
for li in lis:
    print(li)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-73f0095cde135468.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5.获取信息
* 获取属性
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
a = doc('.item-0.active a')
print(a)
print(a.attr('href'))
print(a.attr.href)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-b149ea6688b3b68f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 获取文本
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
a = doc('.item-0.active a')
print(a)
print(a.text())
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-ec82e6c9b34774ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 获取HTML
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('.item-0.active')
print(li)
print(li.html())
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-0aa28bdd4506995b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 6.DOM操作
* addClass、removeClass
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('.item-0.active')
print(li)
li.removeClass('active')
print(li)
li.addClass('active')
print(li)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-0e06739b7c73c552.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* attr、css
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('.item-0.active')
print(li)
li.attr('name', 'link')
print(li)
li.css('font-size', '14px')
print(li)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-40430404ac9c26fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* remove
```
html = '''
<div class="wrap">
    Hello, World
    <p>This is a paragraph.</p>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
wrap = doc('.wrap')
print(wrap.text())
wrap.find('p').remove()
print(wrap.text())
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-f5ad7a75cd8ff126.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 其他DOM方法
[http://pyquery.readthedocs.io/en/latest/api.html](http://pyquery.readthedocs.io/en/latest/api.html)

### 7.伪类选择器
```
html = '''
<div class="wrap">
    <div id="container">
        <ul class="list">
             <li class="item-0">first item</li>
             <li class="item-1"><a href="link2.html">second item</a></li>
             <li class="item-0 active"><a href="link3.html"><span class="bold">third item</span></a></li>
             <li class="item-1 active"><a href="link4.html">fourth item</a></li>
             <li class="item-0"><a href="link5.html">fifth item</a></li>
         </ul>
     </div>
 </div>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li = doc('li:first-child')
print(li)
li = doc('li:last-child')
print(li)
li = doc('li:nth-child(2)')
print(li)
li = doc('li:gt(2)')
print(li)
li = doc('li:nth-child(2n)')
print(li)
li = doc('li:contains(second)')
print(li)
```
运行结果：
![运行结果图](http://upload-images.jianshu.io/upload_images/2896168-1229bebf55918a45.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)