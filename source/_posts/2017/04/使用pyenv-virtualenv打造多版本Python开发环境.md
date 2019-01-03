---
title: 使用pyenv+virtualenv打造多版本Python开发环境
date: 2017-04-06 15:01:25
categories: Python
tags: pyenv virtualenv Python
---

- - -
<!--more-->
使用pyenv+virtualenv打造多版本Python开发环境
---

## 1.pyenv的安装
* `pyenv`的安装，非常简单，[请参考](https://github.com/pyenv/pyenv-installer)
* 需要注意使用的是zsh，还是bash

	
## 2.pyenv的使用
```
# 查看系统当前安装的python列表
$ pyenv versions

# 查看可安装的python包有哪些
$ pyenv install --list

# 安装python
$ pyenv install -v 3.5.1

# 卸载python
$ pyenv uninstall 2.7.3

```

## 3.python环境切换
python优先级: shell > local > global

```
# 设置全局的 Python 版本，通过将版本号写入 ~/.pyenv/version 文件的方式。
$ pyenv global 3.4.0

# 设置面向程序的本地版本
$ pyenv local 2.7.3

# 设置面向 shell 的 Python 版本
$ pyenv shell 3.2.1

```


## 4.使用 pyenv + virtualenv 打造多版本 Python 开发环境
* 创建虚拟环境: pyenv virtualenv 2.7.10 my-virtual-env-2.7.10
* 列出当前虚拟环境: pyenv virtualenvs
* 激活虚拟环境: pyenv activate
* 退出虚拟环境: pyenv deactivate
* 删除虚拟环境: pyenv uninstall my-virtual-env

## 参考
1. [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
2. [Linux 下的 Python 多版本管理](https://my.oschina.net/lionets/blog/267469)


