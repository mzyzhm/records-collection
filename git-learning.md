---
title: Git commands
date: 2020-05-07 08:55:00
tags:
---

1. git config

```
$ git config --global user.name ""
$ git config --global user.email ""
```

2. git command alias

```
# all users in system
$ sudo git config --system alias.br branch
$ sudo git config --system alias.ci "commit -s"
$ sudo git config --system alias.co checkout
$ sudo git config --system alias.st "-p status"

# current user
$ git config --global alias.st status
...
```

3. Commands

```
$ git init
$ git init <project_name>
$ git add <file_name>
$ git commit -m "<commends>"

# show where is .git git repository
$ git rev-parse --git-dir

# 显示工作区根目录
$ git rev-parse --show-toplevel

$ git rev-parse --show-prefix
$ git rev-parse --show-cdup

# 编辑git config
# open demo/.git/config to edit
$ git config -e 
# open C:/Users/username/.gitconfig
$ git config -e --global 
# open C:/Program Files(x86)/Git/Git/mingw64/etc/gitconfig to edit
$ git config -e --system 

# 修改提交说明
$ git commit --amend 

# 修改历史提交说明
$ git rebase -i <commit-id>^

# 不小心包含了不该提交的文件
$ git rm --cached <file-name>
$ git commit --amed
# 历史版本
$ git rebase -i <commit-id>^

# 工作进度保存：当前分支还没完成，另外一个新的bug需要在一个干净工作区解决
$ git stash
$ git checkout <new-branch>
# 切回原来分支，恢复进度
$ git checkout <original-branch>
$ git stash pop

4. git 暂存区

# 查看工作区和暂存区的差异
$ git diff

# 查看工作区和HEAD（当前工作分支）的差异
$ git diff HEAD

# 提交暂存区和版本库中的差异
$ git diff --cached
$ git diff --cached HEAD

# git status扫描工作区改动的时候，先根据`.git/index`文件中记录的时间戳，长度等信息判断工作区文件是否改动。
# 如果改变，说明文件可能被改变，需要打开文件读取内容和更改前的原始文件相比较，判断文件内容是否被更改。高效。
# 精简输出状态
$ git status -s
# 同时显示当前所在的分支
$ git status -s -b

# 暂存区的目录树会被master或者Head指向的目录树所替换，工作区不受影响
$ git reset HEAD 

# 直接从暂存区删除文件
$ git rm --cached <file>

# 会用暂存区的文件替换工作区文件
$ git checkout . or git checkout -- <file>

# 会用HEAD指向的master分支中的全部或部分文件替换暂存区以及工作区中的文件。
$ git checkout HEAD


# 查看HEAD指向的目录树
$ git ls-tree -l HEAD

# 查看暂存区的目录树
$ git ls-files -s

5. git 对象


6. git 重置
# master分支在版本库的引用目录（.git/ref）中体现为一个引用文件`.git/refs/heads/master`，其内容就是分支中最新提交的提交ID

# 当有新的提交内容时，文件内容也会改变，指向新的提交。

# 认为改变master的指向
$ git reset --hard HEAD^

# 可以重置到任何一次提交，会彻底丢弃历史，很危险!!
$ git reset --hard <commit-id>

# 如何找回被丢弃的那些提交
$ tail -5 .git/logs/refs/heads/master
$ git reflog show master | head -5
# 重置master为两次变更之前
$ git reset --hard master@{2}


# 用指定提交状态下文件替换暂存区文件，暂存区中其他文件不改变，工作区也不会改变
$ git reset -- filename
$ git reset HEAD filename


# HEAD指向的目录树重置暂存区，工作区不会受到影响
$ git reset
$ git reset HEAD

# 彻底撤销最近的提交，引用，暂存区和工作区都会回退到上一次提交的状态。
$ git reset --hard HEAD^

# 工作区不改变，暂存区会回退到上一次提交之前，引用也会回退一次
$ git reset HEAD^
$ git reset --mixed HEAD^

# 工作区和暂存区不改变，引用向前回退一次
$ git reset --soft HEAD^

# git commit --amend相当于下面两条命令
$ git reset --soft HEAD^
$ git commit -e -F .git/COMMIT_EDITMSG


7. 恢复进度
# 保存进度
$ git stash

# 保存进度时使用指定的说明
$ git stash save "message..."

# 查看保存的进度
$ git stash list

# 恢复最近保存的进度
$ git stash pop

# 恢复进度，但是不删除stash的进度
$ git stash apply

# 删除一个存储的进度，缺省删除最新的进度
$ git stash drop <stash>

# 删除所有存储的进度
$ git stash clear

# 基于进度创建分支
$ git stash branch <branchname> <stash>

# 删除本地多余的目录和文件，dryrun一下
$ git clean -nd
# 删除本地多余目录和文件
$ git clean -fd



8. 删除文件

# 删除文件 git rm

# 从历史提交中提取文件
$ git cat-file -p HEAD~1:filename > filename

# 移动文件 git mv

# 打tag
$ git tag -m "message..." tag_name 

# .gitignore 只对未跟踪的文件起作用


# git rev-parse 底层命令


# log 命令
$ git log --graph
$ git log -3

# -p 在显示日志时同时显示改动
$ git log -p -l

# 不需要知道具体的改动，只想知道改动在哪些文件上用--stat
$ git log --stat --oneline I..C


$ git show
$ git cat-file


# git diff

# git diff 提供逐行比较，显示改动前的行和改动后的行，
# 另一种逐词比较的输出，使用--word-diff
$ git diff --word-diff


# 显示改行最早是在什么版本引入的
$ git blame <filename>

$ git blame -L 6,+5 <filename>

# 比较正确版本和有问题版本之前的差异，以及问题可能引入的位置
$ git bisect


8. 改变历史
# 修补提交命令
git commit --amend 

# 多步悔棋，把多提commit合并为一个完整的提交

# 把最近三次提交压缩为一个
$ git reset --soft HEAD^^
$ git commit -m "merge 3 commit"

9. 回到未来


```