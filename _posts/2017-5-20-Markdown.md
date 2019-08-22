---
layout: post
title:  "Markdown快速入门"
date:   2017-05-20 12:14:54
categories: Markdown
tags:  Markdown
author: Humy
---
* content
{:toc}

<center class>
    <img src="{{ "/asserts/img/cover/06.jpg" | prepend: site.baseurl }}"/>
</center>




#### 一、标题写法

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

*注：最好#和标题之间保留一个空格*

`效果如下：`
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

#### 二、列表写法

`无序列表：`

```
- 列表一
- 列表二
- 列表三
或者
* 列表一
* 列表二
* 列表三
或者
+ 列表一
+ 列表二
+ 列表三
```

`三者效果一样，如下所示：`

- 列表一
- 列表二
- 列表三

`有序列表：`

```
1. aaa
2. bbb
3. ccc
```

`效果如下：`
1. aaa
2. bbb
3. ccc

#### 三、引用写法

```
> 锄禾日当午
> 汗滴禾下土
> 谁知盘中餐
> 粒粒皆辛苦 
或者
> 一盏灯， 一片昏黄； 一简书， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定， 人生从此不再寂寞。
```

*注：最好>和引用之间保留一个空格*

`效果如下：`

> 锄禾日当午
> 汗滴禾下土
> 谁知盘中餐
> 粒粒皆辛苦 

#### 四、粗体斜体写法

`粗体写法:`

```
**粗体**
```

`斜体写法:`

```
*斜体*
```

*注：斜体星号和文本之间不能有空格，否则将当成列表处理了*

`效果如下：`

**粗体**

*斜体*

#### 五、代码引用

`一行代码`

```
用``将代码包起来就行了
```

`效果如下:`

` System.out.println("Hello world!") `

`多行代码`

```
用``` ```将代码包起来就行了
```

`效果如下:`

```
public class HelloWorld{
   public static void main(String[] args){
      System.out.println("Hello world!") ;
   }
}
```

#### 六、地址链接写法

```
[百度一下你就知道](http://www.baidu.com)
```

`效果如下：`

[百度一下你就知道](http://www.baidu.com)

#### 七、图片链接写法

```
![阿信](http://upload-images.jianshu.io/upload_images/2896168-e97a472df605788b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```

`效果如下:`

![阿信]({{ "/asserts/img/post/2017-5-20/head.jpg" | prepend: site.baseurl }})

`也可以这样写:`

```
![阿信][1]
[1]:http://upload-images.jianshu.io/upload_images/2896168-e97a472df605788b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
```

`同样的效果:`

![阿信][1]

[1]:{{ "/asserts/img/post/2017-5-20/head.jpg" | prepend: site.baseurl }}

#### 八、表格写法

```
|左对齐|居中|右对齐|
|-|:-:|-:|
|aa|dd|gg|
|bb|ee|hh|
|cc|ff|ii|
```

`显示效果如下:`

|左对齐|居中|右对齐|
|-|:-:|-:|
|aa|dd|gg|
|bb|ee|hh|
|cc|ff|ii|

`还可以这样写：`

```
左对齐|居中|右对齐
-|:-:|-:
aa|dd|gg
bb|ee|hh
cc|ff|ii
```

`显示效果一样:`

左对齐|居中|右对齐
-|:-:|-:
aa|dd|gg
bb|ee|hh
cc|ff|ii

#### 九、分割线

```
你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号
或是减号中间插入空格。下面每种写法都可以建立分隔线：
* * *
***
*****
- - -
---------------------------------------
```

`效果如下:`

* * *

***

*****

- - -

---------------------------------------
