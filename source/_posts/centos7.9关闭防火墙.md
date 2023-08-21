---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: centos7.9关闭防火墙
categories:
  - linux
tags:
  - centos
date: 2023-03-28 17:53:30
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

- [查看防火墙状态](#查看防火墙状态)
- [关闭防火墙](#关闭防火墙)
- [禁用防火墙](#禁用防火墙)

<!-- /code_chunk_output -->


## 查看防火墙状态
```
systemctl status firewalld.service
```

## 关闭防火墙

```
systemctl stop firewalld.service
```

## 禁用防火墙

```
systemctl disable firewalld.service
```