---
title: git 撤销操作
img: 
top: true
cover: false
coverImg: 
comment: false
tags:
  - git
  - commit
date: 2019-07-12 11:05:16
summary:
password:
categories: git
---

## git 撤销 commit

> 今天在合并分支时出错，想撤销 commit，发现 idea 自身对撤销 commit 的操作并不友好，于是翻了翻 git 手册，整理下撤销操作的命令！

1. 覆盖上次提交 

   如果本次提交漏了那个文件，可以使用`amend`来重复覆盖上次提交，最终会只有一个提交，第二次提交的结果会覆盖第一次提交的结果。

   ```shell
   git commit --amend
   ```

   更改提交信息   

   如果上次提交后未做任何修改，再次执行就会只覆盖原来的提交信息。

2. 取消提交的文件

   取消本次提交的文件   

   不删除工作空间改动，撤销 commit 和 add . 操作

   ```shell
   git reset --mixed HEAD^
   ```

   - 可以添加文件名字指定文件撤销。

   - `HEAD^` 等价于 `HEAD~1`

   - `HEAD^`的意思是上一个版本，也可以写成`HEAD~1`

   - 如果你进行了2次commit，想都撤回，可以使用`HEAD~2`

   - 参数： 

     - `--mixed  `   
       不删除工作空间改动代码，撤销 `commit`，并且撤销 `git add .` 操作
       这个为默认参数,`git reset --mixed HEAD^` 和 `git reset HEAD^` 效果是一样的。

     - `--soft`   
       不删除工作空间改动代码，撤销`commit`，不撤销`git add .` 。

     - `--hard `   
       删除工作空间改动代码，撤销`commit`，撤销`git add .` 

       注意完成这个操作后，就恢复到了上一次的 commit 状态。

## git 分支

清除本地有而远端没有的无用分支

```shell
git remote prune origin
```