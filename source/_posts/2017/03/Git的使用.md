---
title: Git的使用
date: 2017-03-31 19:57:46
categories: 工具
tags: [git,工具]
---

- - -
<!--more-->
Git的使用
---


## git的使用
![](git基本使用流程.tiff)

## git文件状态流向
![](文件状态流动.tiff)
## diff使用
![](http://i2.muimg.com/567571/83672d403d19673c.png)

## 基本命令

```
# 配置个人信息	
  $ git config --global user.name "Your Name"
  $ git config --global user.email 
"email@example.com"

# git目录初始化
  $ git init

# 文件添加到仓库
  $ git add -p <file>
  $ git add .

# 把文件提交到仓库
  $ git commit -m "add LICENSE"

# 查看仓库当前状态
  $ git status

# 查看difference
  $ git diff

# 显示从最近到最远的提交日志
  $ git log --pretty=oneline # 格式化输出信息

# 版本退回
  $ git reset --hard HEAD^ # 当前版本HEAD,上一个版本HEAD^,上上个版本HEAD^^
  $ git reset --hard 130f10a # 或HEAD~100

# 查看命令记录
  $ git reflog

# 丢弃工作区的修改，回到最近一次git commit或git add时的状态：
  $ git checkout -- README.md

# 把暂存区的修改撤销掉（unstage）
  $ git reset HEAD READER.md

# 从版本库中删除该文件
  $ git rm README.md
  $ git commit -m "remove READER.md"

# 把误删的文件恢复到最新版本，checkout其实用版本库里的版本替换工作区的版本
  $ git checkout -- README.md

```

## 远程仓储

```
 $ ssh-keygen -t rsa -C "youremail@example.com"
# 测试是否成功
  $ ssh -T git@github.com

# 把一个已有的本地仓库与之关联
  $ cd existing-project 
  $ git init 
  $ git add --all 
  $ git commit -m "Initial Commit" 
  $ git remote add origin ssh://git@git.sankuai.com/~cuijianlong/autoated_scrip.git 
  $ git push origin master

# 把本地库的所有内容推送到远程库上（推送master分支的内容）
  $ git push -u origin master

# 向远程库推送更新
  $ git push origin master

# 从远程库克隆
  $ git clone git@github.com:xxxx/xxxxx

# 远程分支切换
  $ git clone                 # 克隆远程代码
  $ git branch -av            # 查看远程分支和本地分支列表
  $ git  checkout  remotes/origin/ceair    
  $ git  checkout  ceair 

```

## 分支管理
```
# 创建+切换dev分支
  $ git checkout -b dev

# 相当于
  $ git branch dev # 创建分支
  $ git checkout dev

# 查看当前分支，当前分支前面标有×号
  $ git branch

# 切换回master分支
  $ git checkout master

# 合并指定分支到当前分支
  $ git merge dev

# 删除dev分支
  $ git branch -d dev

# 查看分支合并情况
  $ git log --graph --pretty=oneline --abbrev-commit

# 修改readme.txt文件，并提交一个新的commit
  $ git add readme.txt
  $ git commit -m "add merge"

# 切换回master
  $ git checkout master

# 合并dev分支，请注意--no-ff参数，表示禁用Fast forward
  $ git merge --no-ff -m "merge with no-ff" dev

# 如果需要临时修复Bug，可以把当前工作现场“储藏”起来，等Bug修复后恢复现场后继续工作
  $ git stash list

# 此时查看工作区是干净
# 切换到需要修复Bug的分支，创建临时分支来修复
  $ git checkout master
  $ git checkout -b issue-101

# 修复完成后切换到master分支，完成合并，删除临时分支
  $ git checkout master
  $ git merge --no-ff -m "merged bug fix 101" issue-101
  $ git branch -d issue-101

# Bug修复后，切换回dev分支继续干活
  $ git checkout dev

# 查看工作现场列表
  $ git stash list

# 恢复工作现场
  $ git stash pop # 恢复的同时把stash内容也删了
  $ git stash apply # 恢复，不删除stash的内容，使用git stash drop

# 再次查看工作现场列表，干净
  $ git stash list

# 可以多次stash，恢复时指定恢复
  $ git stash apply stash@{0}

# 强行删除一个没有合并过的分支
  $ git branch -D <name>

# 要查看远程库的信息
  $ git remote
  $ git remote -v

# 推送其他分支
  $ git push origin dev

# 从远程库clone，默认情况只能看到master分支，需要在dev分支，必须创建远程origin的dev分支到本地
  $ git checkout -b dev origin/dev
  $ git checkout -b branch-name origin/branch-name
  $ git branch --set-upstream branch-name origin/branch-name # 关联

# 向远程库推送dev有冲突
  $ git pull # 抓取到本地合并解决冲突，再向远程推送
  $ git push origin dev

```

## 标签管理
```
# 列出所有tag 
  $ git tag   
# 新建一个tag在当前commit 
  $ git tag [tag] 
# 新建一个tag在指定commit 
  $ git tag [tag] [commit] 
# 删除本地tag $ git tag -d [tag] 
# 删除远程tag 
  $ git push origin :refs/tags/[tagName] 
# 查看tag信息 
  $ git show [tag] 
# 提交指定tag 
  $ git push [remote] [tag] 
# 提交所有tag 
  $ git push [remote] --tags 
# 新建一个分支，指向某个tag 
  $ git checkout -b [branch] [tag]
  
```

## 自定义 Git

```
# 显示颜色，会让命令输出看起来更醒目
  $ git config --global color.ui true

# 忽略某些文件时，需要编写.gitignore，然后将.gitignore放到版本库中
# st就表示status
  $ git config --global alias.st status

# 配置一个unstage别名
  $ git config --global alias.unstage 'reset HEAD'
  $ git unstage test.py # 等价于
  $ git reset HEAD test.py

# 显示最后一次提交信息
  $ git config --global alias.last 'log -1'

```
