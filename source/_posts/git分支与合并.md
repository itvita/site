---
title: git分支与合并
categories:
  - git
tags:
  - git
mp3: /music/突然的自我.mp3
cover: /img/233628-1657208188e67f.jpg
date: 2022-11-25 14:23:39
---
# 通过本地分支创建远程分支

> 创建并切换到本地分支

```
git checkout -b 分支名称
```
> 查看分支

```
git branch
```

> 同步并创建远程分支

```
git push --set-upstream origin 分支名称
```
> 切换分支

```
git checkout 分支名称（默认主分支：master）
```

# 如果本地没有分支，同步远程分支

> 更新远程主机origin 整理分支

```
git remote update origin --prune
```

> 列出远程分支

```
git branch -r
```

> 可以利用 git checkout --track origin/branch_name ，这时本地会新建一个分支名叫 branch_name ，会自动跟踪远程的同名分支 branch_name

```
git checkout --track origin/分支名称
```

> 或者新建本地分支gpf与远程gpf分支相关联

```
git checkout -b gpf origin/分支名称
```

# 合并分支到master上

> 首先切换到master分支上

```
git checkout master
```

> 如果是多人开发的话 需要把远程master上的代码pull下来

```
git pull origin master
```

> 然后我们把dev分支的代码合并到master上

```
git  merge dev
```

> 然后查看状态

```
git status
```

