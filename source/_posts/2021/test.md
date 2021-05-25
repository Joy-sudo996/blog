---
title: YoloV4首发使用体验
permalink: YoloV4首发使用体验
date: 2020-05-27 22:46:31
tags:
categories:
---
 最近在学习吴恩达老师的机器学习课程，推荐使用的是Octave工具，这里配一波环境（默认已经装好VS Code和WSL，没装的友友看别的友友的博客）有错误或者有疑问的欢迎底下评论。

#  1、安装conda并创建conda虚拟环境
[百度网盘链接](https://pan.baidu.com/s/1Eai8e8VAKzhEzFkIEPZziA)  提取码：nezq
```shell
bash Anaconda3-2020.11-Linux-x86_64.sh
```

这里创建一个名为octave，python版本为3.8的虚拟环境（名称和版本根据自己的更改）
```shell
conda create -n octave python=3.8
```


#  2、安装Octave(在base环境下安装)
a.![在这里插入图片描述](https://img-blog.csdnimg.cn/20210510093123118.png)

```shell
sudo apt-get install octave
```
b.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210510093217308.png)
```shell
sudo apt-get install octave-control octave-image octave-io octave-optim octave-signal octave-statistics
```
c.添加环境变量

   我这里shell用的是zsh所以打开这个文件编辑，如果是bash，则用~/.bashrc
```shell
vim ~/.zshrc
```
在最后一行加上
```shell
export PATH="/usr/bin/octave:$PATH"
```
保存退出后激活一下
```shell
source ~/.zshrc
```

#  3、安装Octave_kernel(在conda虚拟环境下安装)
a.激活虚拟环境

```shell
conda activate octave
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504210049470.png)
b.安装

```shell
pip install metakernel
pip install octave_kernel
python -m octave_kernel install --user
```

# 4、VS Code连接WSL
a.安装如图插件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504202134566.png)
b.点击绿色的地方
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504202400661.png)
c.选择New Window或者Reopen Folder in WSL
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504202042842.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDYwMDQwMA==,size_16,color_FFFFFF,t_70)
d.打开wsl挂载的文件夹，这里的Machine_learning是我自己新建的
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504205321615.png)
d.连接成功
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504205526150.png)
#  5、安装jupyter notebook
a.安装python插件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504210609330.png)
b.安装jupyter插件（一般装了python插件之后这个插件就装好了）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210504210633746.png)
c.新建一个jupyter notebook
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210506143908657.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210506144016358.png)
d. 右上角Python 3.8.5。。。为这个notebook的核，可选择
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210506144336946.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDYwMDQwMA==,size_16,color_FFFFFF,t_70)
选择Octave
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210510105536865.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDYwMDQwMA==,size_16,color_FFFFFF,t_70)
e.测试代码

```python
clear all;
clc;
x=-2:0.01:2;
y=sqrt(2*sqrt(x.^2)-x.^2);
z=asin(abs(x)-1)-pi./2;
plot(x,y)
grid on;
hold on;
plot(x,z);
axis([-2,2,-2,2]);
```
运行成功如图
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021051010542274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDYwMDQwMA==,size_16,color_FFFFFF,t_70)
#  6、过程中遇到的bug
a.如果运行代码出现如下图错误![在这里插入图片描述](https://img-blog.csdnimg.cn/20210510104656555.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDYwMDQwMA==,size_16,color_FFFFFF,t_70)
解决方法：(选其一，主要是看后面的包是在哪里)

```shell
sudo strip --remove-section=.note.ABI-tag /usr/lib/x86_64-linux-gnu/libQt5Core.so.5
#sudo strip --remove-section=.note.ABI-tag /usr/lib64/libQt5Core.so.5
```
b.如果显示 strip:command not found
解决方法（base环境下）：

```shell
conda install binutils
```

c.如果import notebook的时候出现下图错误
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210506162908595.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDYwMDQwMA==,size_16,color_FFFFFF,t_70)
解决方法（base环境下）：

```shell
conda install nbconvert
```

