---
layout: post
title:  "Python爬虫之PyQuery解析库的使用"
date:   2018-09-04 8:00:54
categories: Python
tags: Python爬虫 Python
author: Humy
---
* content
{:toc}

*本文为笔者根据Python静觅教程记录笔记，仅供学习使用*

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/01.png" | prepend: site.baseurl }})

* URL初始化

```
from pyquery import PyQuery as pq
doc = pq(url='http://www.baidu.com')
print(doc('head'))
```

运行结果：

![运行结果图]({{ "/asserts/img/post/2018-9-04/02.png" | prepend: site.baseurl }})

* 文件初始化

```
from pyquery import PyQuery as pq
doc = pq(filename='demo.html')
print(doc('li'))
```

运行结果：

![运行结果图]({{ "/asserts/img/post/2018-9-04/03.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/04.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/05.png" | prepend: site.baseurl }})

```
lis = items.children()
print(type(lis))
print(lis)
```

运行结果：

![运行结果图]({{ "/asserts/img/post/2018-9-04/06.png" | prepend: site.baseurl }})

```
lis = items.children('.active')
print(lis)
```

运行结果：

![运行结果图]({{ "/asserts/img/post/2018-9-04/07.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/08.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/09.png" | prepend: site.baseurl }})

```
parent = items.parents('.wrap')
print(parent)
```

运行结果：

![运行结果图]({{ "/asserts/img/post/2018-9-04/10.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/11.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/12.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/13.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/14.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/15.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/16.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/17.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/18.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/19.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/20.png" | prepend: site.baseurl }})

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

![运行结果图]({{ "/asserts/img/post/2018-9-04/21.png" | prepend: site.baseurl }})

