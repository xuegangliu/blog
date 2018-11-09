title: Ubuntu结构
comments: true
date: 2018-11-09 15:28:01
updated: 2018-11-09 15:28:01
tags:
  - Linux
  - Ubuntu
categories: Linux
---
## 目录结构

![目录结构1](/images/linux/dir1.png)
![目录结构2](/images/linux/dir2.png)
![目录结构2](/images/linux/dir3.png)
![目录结构2](/images/linux/dir4.png)

## 软件包管理
Ubuntu更新软件时的软件源配置文件是/etc/apt/sources.list。
ubuntu的官方软件源分为4类：
 - main：这个是官方维护的基本库。
 - restricted：官方维护的其他自由软件。
 - universe：自由软件，但是官方不维护。
 - multiverse：非自由软件，官方不维护。

apt
apt是一套完整的软件包管理方案。除了最常用apt-get之外，还包括了一系列的客户端和服务器软件。
例如：
```
sudo apt-cache search gstreamer 搜索名字中包含gstreamer的软件包。
sudo add-apt-repository ppa:tualatrix/ppa添加新的软件源。
```
### 安装命令
```
sudo  apt-get install foo
dpkg -i *.deb
wget http://*
```
### 卸载命令
```
sudo apt-get --purge remove foo
sudo  apt-get remove  foo
```
