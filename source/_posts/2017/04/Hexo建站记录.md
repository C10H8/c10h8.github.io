---
title: Hexo建站记录
date: 2017-04-01 16:39:36
categories: 工具
tags: [hexo]
---

- - -
<!--more-->
Hexo建站记录
---


##  1.建站
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
## 2.配置站点的_config.yml

上传代码需要注意的配置

```
deploy:
  type: git
  repository: https://github.com/stegosauruscui/stegosauruscui.github.io.git
  branch: master
```

## 3. package.json
``` 
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": "3.2.2"
  },
  "dependencies": {
    "hexo": "^3.2.0",
    "hexo-deployer-git": "^0.2.0",
    "hexo-generator-archive": "^0.1.4",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.0",
    "hexo-generator-searchdb": "^1.0.3",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.2.0",
    "hexo-renderer-marked": "^0.2.10",
    "hexo-renderer-stylus": "^0.3.1",
    "hexo-server": "^0.2.0"
  }
}
```
`注意`： 

* hexo 更新到3.0之后，deploy的type 的github需要改成git
* 如出现`在执行 hexo deploy 后,出现 error deployer not found:github 的错误`，执行：npm install hexo-deployer-git --save  

## 4.主题
### 1. 安装next

```
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
### 2. 参考
[快速使用](http://theme-next.iissnan.com/getting-started.html)

[主题配置](http://theme-next.iissnan.com/theme-settings.html)


## 5.常用命令
* `hexo -d`          上传到githup
* `hexo -g`          生成静态页面
* `hexo clean`       清理
* `hexo new file`     新建文件（写作页面）
* `hexo s`            启动服务
* `hexo new page tags`   新建一个页面（首页，分类，about……）

## 6. 如何写文章


![](http://i4.buimg.com/567571/38f47fd15b6a3169.png)

`如图所示，只需要把需要分类的文章写在 categories： 后面,自然就会分类`

## 7. 备份自己博客的源文件
当你执行`hexo d`命令后，hexo-deployer-git仅仅把博客的静态文件上传到gitHup的master分支。如果后期需要更换电脑什么的该怎么找到自己的源文件编辑，所以备份博客的源文件变得很重要的一个步骤。

```
# git初始化自己的博客文件
$ git init --bare <your_repo>.git
$ git add README.md
$ git commit -m "first commit"
# 创建一个hexoOrigin ，保存源文件分支， 在远程分支创建一个hexoOrigin，githup博客默认使用master分支
$ git checkout -b hexoOrigin
$ git push -u origin hexoOrigin  # 把源文件push到需要保存的分支 
```
## 8.更换新的电脑或者文件路径，拉取源文件操作

```aidl
# 拉取远程分支
$ git git clone git@github.com:stegosauruscui/stegosauruscui.github.io.git
# 顺序执行下面三个步骤即可
$ npm install hexo 
$ npm install
$ npm install hexo-deployer-git
$ hexo g # 生成静态文件
$ hexo s # 启动服务，测试是否正常
```


## 注意
> 1. 注意push的时候确保自己的主题目录文件，比如我用的主题是next，是直接拉取github上的，里面有别人的git文件，导致我push的时候并没有把主题文件push到远程



