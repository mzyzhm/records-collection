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

# show workspace
$ git rev-parse --show-toplevel

$ git rev-parse --show-prefix
$ git rev-parse --show-cdup

# edit different level config
$ git config -e # open demo/.git/config to edit
$ git config -e --global # open C:/Users/username/.gitconfig
$ git config -e --system # open C:/Program Files(x86)/Git/Git/mingw64/etc/gitconfig to edit

$ git commit --amend 



```