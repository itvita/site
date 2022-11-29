---
title: git从版本库中移除文件
categories:
  - git
tags:
  - git
mp3: /music/后来.mp3
cover: /img/235303-16661947832ac9.jpg
date: 2022-11-24 14:22:58
---
> 如果你想把一个文件从版本控制中移除，并且保留本地的文件，首先需要把这个文件加入到gitignore文件中。然后执行以下命令就可以了

```
git rm file_path --cached
```

> 以上命令将file_path所代表的文件从版本控制中删除，并保留本地文件，此外还要进行commit操作才能将服务端的文件删掉。如果想把一个文件夹从版本控制中删除并保留本地的文件，只需在上述命令的基础上加上-r参数，即

```
git rm -r folder_path --cached
```

> 如果想把所有gitignore中的文件从版本控制中删除的话，需要执行以下两个命令，即先移除所有文件，再执行添加所有文件（这次会忽略gitignore中的文件）。

```
git rm -r . --cached
git add .
```