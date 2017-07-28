---
layout: post
title:  "Ununtu系统一些基本设置"
date:   2017-07-28 22:14:54
categories: Ubuntu
tags:  Ubuntu
author: Humy
---
* content
{:toc}

**今天心血来潮,在win7系统上装了一个Ubuntu双系统,下面记录一些基本的设置命令,持续更新...大神勿喷**




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
sudo apt removw xxxxxxx
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
