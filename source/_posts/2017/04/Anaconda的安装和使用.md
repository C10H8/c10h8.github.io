---
title: Anaconda的安装和使用
date: 2017-04-10 14:47:52
categories: Python
tags: [Anaconda,Python]
---

- - -
<!--more-->
Anaconda的安装和使用
---


![](https://pic1.zhimg.com/v2-0658b34b4498516ba1014e6fe6490b88_r.jpg)
## 1. 什么是Anaconda
官方的解释：
>  Anaconda is the leading open data science platform powered by Python. The open source version of Anaconda is a high performance distribution of Python and R and includes over 100 of the most popular Python, R and Scala packages for data science.

>  Additionally, you'll have access to over 720 packages that can easily be installed with conda, our renowned package, dependency and environment manager, that is included in Anaconda. See the packages included with Anaconda and the Anaconda changelog

>  [Anaconda](https://www.continuum.io/why-anaconda) 是一个用于科学计算的Python发行版，支持 Linux, Mac, Windows系统，提供了包管理与环境管理的功能，可以很方便地解决多版本python并存、切换以及各种第三方包安装问题。Anaconda利用工具/命令conda来进行package和environment的管理，并且已经包含了Python和相关的配套工具。

## 2. Anaconda的安装

[官网下载](https://www.continuum.io/downloads)

安装时，会发现有两个不同版本的Anaconda，分别对应Python 2.7和Python 3.5，两个版本其实除了这点区别外其他都一样。后面我们会看到，安装哪个版本并不本质，因为通过环境管理，我们可以很方便地切换运行时的Python版本。

## 3. Anaconda的使用
```
# 创建一个名为python34的环境，指定Python版本是3.4（不用管是3.4.x，conda会为我们自动寻找3.4.x中的最新版本）
conda create --name python34 python=3.4

# 使用activate激活某个环境
activate python34 # for Windows
source activate python34 # for Linux & Mac
# 激活后，会发现terminal输入的地方多了python34的字样，实际上，此时系统做的事情就是把默认2.7环境从PATH中去除，再把3.4对应的命令加入PATH

# 此时，再次输入
python --version
# 可以得到`Python 3.4.5 :: Anaconda 4.1.1 (64-bit)`，即系统已经切换到了3.4的环境

# 退出当前的环境
deactivate python34 # for Windows
source deactivate python34 # for Linux & Mac

# 删除一个已有的环境
conda remove --name python34 --all

# 列举当前环境中的所有依赖包
conda list 
# 安装某个新的依赖
conda install nltk 
```

### 4. Jupyter Notebook
在Conda安装之后，Jupyter Notebook是默认安装好的，直接在工作目录下打开即可:

jupyter notebook
你可以参阅[Running the Notebook](http://jupyter.readthedocs.io/en/latest/running.html#running)获取更多命令细节,后面在写一篇文章介绍`jupyter`的使用。




## 参考
* [Anaconda使用总结](http://www.jianshu.com/p/2f3be7781451)
* [官网](https://www.continuum.io/downloads#osx)
* [Python语法速览与机器学习开发环境搭建](https://zhuanlan.zhihu.com/p/24536868)
