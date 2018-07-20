---
layout: post
title:  "Centos6-8下安装Eclipse-for-PyDev以及图形化显示"
date:   2017-07-12 18:30:54
categories: Tensorflow
tags:  Tensorflow
author: Humy
---
* content
{:toc}

> 上一篇文章介绍了windows系统上Tensorflow环境的搭建，但是笔者电脑配置不高，运行一些demo cpu直接爆表，所以目标转向了阿里云的服务器（ps:笔者不是土豪，服务器是老师的），这里记录下搭建过程中遇到的坑，不是一点点啊~~~




#### 目录

* Centos图形化显示
* Centos下安装python3.5
* pip安装tensorflow

### 1.Centos图形化显示

首先准备三个软件：Xshell,Xftp,Xmanager,下面附上百度云链接：
[准备软件下载地址](http://pan.baidu.com/s/1eSEdii2)
先下载好上述三个软件，这里只用配置Xshell连接阿里云服务器即可，另外两个软件都可以通过这个来打开，Xshell需要进行如下配置：

#### ①
![登录口令密码]({{ "/asserts/img/post/2017-7-12/01.png" | prepend: site.baseurl }})
 
#### ②
![]({{ "/asserts/img/post/2017-7-12/02.png" | prepend: site.baseurl }})

#### ③
![Paste_Image.png]({{ "/asserts/img/post/2017-7-12/03.png" | prepend: site.baseurl }})

配置完，先不要管，连接到服务器，然后在服务器上安装相关的软件:

```
#yum groupinstall -y "X Window System"
#yum groupinstall -y "Desktop"
#yum groupinstall -y "Chinese Support"
```

安装完，重新连接服务器，输入下面的命令：
`#gnome-session`

这时应该会出现图形化界面了
然后第一步就很轻松的搞定了，下面开始讲Centos下安装python3.5

### 2.Centos下安装python3.5

因为我的服务器上默认安装的是python2.7,因为有可能linux下有的程序依赖这个环境，所以不要去动python2.7,这时需要去官网下载python3.5，我上面的链接也有提供，如果嫌百度云慢的可以直接去官网下载。下载完，利用Xftp工具将本地的安装包上传到服务器的目录中去，我这里放入了`/usr/local/src下`后面的一些安装包我也是放在了这个目录下
`tar -xzvf Python-3.5.0.tgz`
`cd Python-3.5.0`

在编译前先在/usr/local建一个文件夹python3（作为python的安装路径，以免覆盖老的版本）
然后开始编译安装

`mkdir /usr/local/python3`

```
./configure --prefix=/usr/local/python3
make
make install
```

此时没有覆盖老版本，再将原来/usr/bin/python链接改为别的名字

`mv /usr/bin/python /usr/bin/python_old2`

再建立新版本python的链接

`ln -s /usr/local/python3/bin/python3/usr/bin/python`

这个时候输入
`python -V`
　　
就会显示出python的新版本信息

```
[root@localhost home]# python -V
Python 3.5.0
```

这种方法虽然能安装成功，但是它带来了新的问题，比如yum不能正常用了
修改/usr/bin/yum的第一行为：
'#!/usr/bin/python_old2
就可以了

### 3.pip安装tensorflow

#### ①安装pip之前需要安装setuptools

这个我之前的链接也已经提供了（下面出现的工具百度云链接也都有，下面就不再赘述了）
同样是利用xftp工具上传到
`/usr/local/src`

`tar -zxvf setuptools-19.6.tar.gz`

`cd setuptools-19.6`

`python setup.py install`

报错：RuntimeError: Compression requires the (missing) zlib module
我们需要在Linux中安装zlib-devel包，进行支持。

`yum install zlib-devel`

需要对python3.5进行重新编译安装。

```
cd python-3.5.0
./configure --prefix=/usr/local/python3
make
make install
```

#### ②安装pip
将pip-9.0.1.tar.gz上传到src目录

`tar -zxvf pip-9.0.1.tar.gz`

```
cd pip-9.0.1
python setup.py install
```
如果没有意外的话，pip安装完成。
下面将新安装的pip链接到系统默认的pip

`ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3  `

#### ③使用pip安装Tensorflow

```
pip3 install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.2.1-cp35-cp35m-linux_x86_64.whl
```
不出意外的话，又会报错，这是只需要安装openssl-devel
`yum install openssl-devel`

然后重新编译python3.5

```
cd python-3.5.0
./configure --prefix=/usr/local/python3
make
make install
```

然后再安装Tensorflow，不出意外的话就安装成功了

```
pip3 install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.2.1-cp35-cp35m-linux_x86_64.whl
```

#### ④安装Eclipse
安装Eclipse之前需要先安装jdk,将下载好的jdk放入src目录下

`rpm -ivh jdk-8u131-linux-x64.rpm`

运行`java -version`如果出现版本号就说明安装成功了

然后安装Eclipse,同样的将下载好的Eclipse放入src目录下，

`tar-zxvf eclipse-inst-linux64.tar.gz`

此时可以通过图形界面来操作了，

`gnome-session`

进入图形界面，找到Eclipse解压的目录双击安装就好了
运行界面如下：
![]({{ "/asserts/img/post/2017-7-12/04.png" | prepend: site.baseurl }})
这时需要在Eclipse上扩展PyDev插件：
help-install new software-Add

![]({{ "/asserts/img/post/2017-7-12/05.png" | prepend: site.baseurl }})


一切安装完成后，新建一个PyDev项目，
这时会让你配置python解释器环境，选择自动配置就可以了，后面也可以进行如下图所示的更改：

![]({{ "/asserts/img/post/2017-7-12/06.png" | prepend: site.baseurl }})

然后运行第一个tensorflow程序，会报一下错误：

![]({{ "/asserts/img/post/2017-7-12/07.png" | prepend: site.baseurl }}

为了解决这个问题，哥哥走了许多弯路~.~
好算是最后终于搞定了！！
这里列出解决办法：
1.首先安装glibc-2.17

```
#wget http://ftp.gnu.org/pub/gnu/glibc/glibc-2.17.tar.xz
#xz -d glibc-2.17.tar.xz
#tar -xvf glibc-2.17.tar
#cd glibc-2.17
#mkdir build
#cd build
#../configure --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin  
#make
#make install
```

需要等大概10分钟。

输入`strings /lib64/libc.so.6|grep GLIBC`发现已经更新 

```
GLIBC_2.2.5
GLIBC_2.2.6
GLIBC_2.3
GLIBC_2.3.2
GLIBC_2.3.3
GLIBC_2.3.4
GLIBC_2.4
GLIBC_2.5
GLIBC_2.6
GLIBC_2.7
GLIBC_2.8
GLIBC_2.9
GLIBC_2.10
GLIBC_2.11
GLIBC_2.12
GLIBC_2.13
GLIBC_2.14
GLIBC_2.15
GLIBC_2.16
GLIBC_2.17
GLIBC_PRIVATE
```

这时还有问题，需要下载libstdc++.so.6.0.20，上面的链接已经给出。

```
cd /usr/lib64/
mv /usr/lib64/libstdc++.so.6 /usr/lib64/libstdc++.so.6.bak
ln -s libstdc++.so.6.0.20 libstdc++.so.6
```

大功告成了！测试一下
![]({{ "/asserts/img/post/2017-7-12/08.png" | prepend: site.baseurl }})

运行成功！开森~~