---
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
title: vscode配置markdown
categories:
  - 开发工具
tags:
  - vscode
  - markdown
mp3: /music/点歌的人-海来阿木.mp3
cover: /img/000726-16587652463b70.jpg
date: 2022-12-05 09:37:57
---
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
<!-- code_chunk_output -->

1. [安装插件](#安装插件)
2. [插件配置](#插件配置)
3. [通过markdown-preview-enhanced导出左侧目录](#通过markdown-preview-enhanced导出左侧目录)

<!-- /code_chunk_output -->


# 安装插件
![](/img/20221205100328.png)
1. Markdown All in One
2. Markdown PDF
3. Markdown Preview Enhanced
4. Paste Image
# 插件配置
```
"markdown-pdf.displayHeaderFooter": false,
"markdown-pdf.highlightStyle": "github.css",
"markdown-pdf.styles": [
    "C:\\home\\tools\\vscodeMdStyle\\typora-vue-theme-master\\vue.css"
],
"markdown-preview-enhanced.codeBlockTheme": "github.css",
"markdown-preview-enhanced.automaticallyShowPreviewOfMarkdownBeingEdited": true,
"markdown-preview-enhanced.enableCriticMarkupSyntax": true,
"markdown-preview-enhanced.enableExtendedTableSyntax": true,
"markdown-preview-enhanced.enableHTML5Embed": true,
"markdown-preview-enhanced.enableTypographer": true,
"markdown-preview-enhanced.frontMatterRenderingOption": "table",
"markdown-preview-enhanced.HTML5EmbedUseLinkSyntax": true,
"markdown-preview-enhanced.enableScriptExecution": true,
"markdown-preview-enhanced.previewTheme": "github-light.css",
"pasteImage.path": "${projectRoot}/source/img",
"pasteImage.basePath": "${projectRoot}/source",
"pasteImage.forceUnixStyleSeparator": true,
"pasteImage.prefix": "/",
"pasteImage.defaultName": "YMMDDHHmmss"
```
# 通过markdown-preview-enhanced导出左侧目录
![](/img/20221205101434.png)
![](/img/20221205101507.png)
1. 增加如下代码生成左侧目录
```
--
html:
  toc: true
  print_background: true
toc:
  depth_from: 1
  depth_to: 6
  ordered: true
--
```
2. 增加如下代码生成顶部目录
```
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=true} -->
```