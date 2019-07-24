---
layout: post
title:  "Windows、Ununtu双系统安装及设置"
date:   2017-07-28 22:14:54
categories: Ubuntu
tags:  Ubuntu
author: Humy
---
* content
{:toc}

<center class>
    <img src="{{ "/asserts/img/cover/18.jpg" | prepend: site.baseurl }}"/>
</center>




**今天心血来潮,在win7系统上装了一个Ubuntu双系统,下面记录一些基本的设置命令,持续更新...大神勿喷**

首先，简单介绍一下安装过程
* 空出一个盘符出来，内存尽量大一点，然后在磁盘管理里面右键那个空的磁盘->删除卷
* 制作U盘启动盘，我是用的[Rufus](https://rufus.akeo.ie/?locale=zh_CN)刻录工具，使用非常简单，只用指定一下你的iso文件的路径就好了，其他保持默认，然后点击开始
* 重启电脑，用U盘启动电脑，我是华硕的电脑，开机过程中按住Esc键，就弹出开机启动界面
* 出现两个按钮，安装Ubuntu和试用Ubuntu，点击安装Ubuntu，你也可以先试用一下。

### 安装后缀名为.deb文件的方式

```
sudo dpkg -i xxxxxxx.deb
```
如果出现错误是因为缺少一些安装该软件所需要的软件包,继续输入以下命令即可解决:

```
sudo apt -f install
```
### 删除该软件

```
sudo apt remove xxxxxxx
```

### 更新系统软件

```
sudo apt update #获取更新信息
sudo apt upgrade
```

### 菜单栏位置设置

```
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
```
### atom安装

```
sudo add-apt-repository ppa:webupd8team/atom  
sudo apt-get update  
sudo apt-get install atom  
```

### git安装

```
sudo apt-get install git
```

安装完成后对git进行配置

```
git config --global user.name "xxx"
git config --global user.email "xxx"
ssh-keygen -C 'you email address@gmail.com' -t rsa
```

然后将生成的.ssh文件夹下的id_rsa.pub文件里的内容复制到github的ssh key一栏

```
gedit .ssh/id_rsa.pub进行查看
```

然后新建一个目录存放你的项目,例如

```
mkdir Blog
sudo chmod 777 Blog
cd Blog
git init
```
然后将你的项目放入Blog文件夹

```
git add .
git commit -m "description infomation"
git remote add origin https://github.com/用户名/仓库.git
git push origin master
```
### 设置开机默认系统

这种方式安装的双系统，系统会默认优先启动Ubuntu，如果想设置优先启动windows，需进行如下设置：

```
sudo /etc/default/grub
```
将里面的`GRUB_DEFAULT=0`,改为`GRUB_DEFAULT=4`
`GRUB_TIMEOUT=10`,改为`GRUB_TIMEOUT=5`，然后保存,再执行

```
sudo update-grub
```

### Albert快捷搜索

```
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt-get update
sudo apt-get install albert
```
### Docky----一款类似于 MAC OS X 底部启动器的软件程序。

```
sudo add-apt-repository ppa:ricotz/docky
sudo apt-get update
sudo apt-get install docky
```
安装完成，直接运行，原来的左侧任务栏可以在外观设置里设为隐藏，并且灵敏度设为0

### Unity Tweak Tool主题管理工具

```
sudo apt-get install unity-tweak-tool
```
### flatabulous主题安装

```
sudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install flatabulous-theme
```

### numix-circle图标

```
sudo add-apt-repository ppa:numix/ppa
sudo apt-get update
sudo apt-get install numix-gtk-theme numix-icon-theme-circle
```
下载好的主题，图标，都可以通过运行Unity Tweak Tool主题管理工具，在里面进行应用