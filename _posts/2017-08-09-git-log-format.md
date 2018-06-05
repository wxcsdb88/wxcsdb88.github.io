---
layout: post
title:  "git log 格式配置"
date:   2017-08-09 00:00:00
categories: Git
description: git log 格式配置
keywords: git
author: wxcsdb88
---

git log 格式配置

# git log 配置

```bash
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'"
```

> 上述可以使用`git lg`查看git log

# pretty 使用

git log --pretty=format:'%h %ar %an'
把format后面单引号中的内容替换为你想要的格式，即可实现自定义的log输出格式。这里的%h, %ar等是一些git预定义的占位符，完整的列表如下：

|格式|说明|
|:--|:--|
| %H | commit hash |
| %h | commit的短hash |
| %T | tree hash |
| %t | tree的短hash |
| %P | parent hashes |
| %p | parent的短hashes |
| %an | 作者名字 |
| %aN | mailmap中对应的作者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1)) |
| %ae | 作者邮箱 |
| %aE | 作者邮箱 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1)) |
| %ad | 日期 (–date= 制定的格式) |
| %aD | 日期, RFC2822格式 |
| %ar | 日期, 相对格式(1 day ago) |
| %at | 日期, UNIX timestamp |
| %ai | 日期, ISO 8601 格式 |
| %cn | 提交者名字 |
| %cN | 提交者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1)) |
| %ce | 提交者 email |
| %cE | 提交者 email (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1)) |
| %cd | 提交日期 (–date= 制定的格式) |
| %cD | 提交日期, RFC2822格式 |
| %cr | 提交日期, 相对格式(1 day ago) |
| %ct | 提交日期, UNIX timestamp |
| %ci | 提交日期, ISO 8601 格式 |
| %d | ref名称 |
| %e | encoding |
| %s | commit信息标题 |
| %f | 过滤commit信息的标题使之可以作为文件名 |
| %b | commit信息内容 |
| %N | commit notes |
| %gD | reflog selector, e.g., refs/stash@{1} |
| %gd | shortened reflog selector, e.g., stash@{1} |
| %gs | reflog subject |
| %Cred | 切换到红色 |
| %Cgreen | 切换到绿色 |
| %Cblue | 切换到蓝色 |
| %Creset | 重设颜色 |
| %C(…) | 制定颜色, as described in color.branch.* config option |
| %m | left, right or boundary mark |
| %n | 换行 |
| %% | a raw % |
| %x00 | print a byte from a hex code |
