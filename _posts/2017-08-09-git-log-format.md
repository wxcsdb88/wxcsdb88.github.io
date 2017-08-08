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

## git log 配置
```
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'"
```
上述可以使用`git lg`查看git log
## pretty 使用
git log --pretty=format:'%h %ar %an'
把format后面单引号中的内容替换为你想要的格式，即可实现自定义的log输出格式。这里的%h, %ar等是一些git预定义的占位符，完整的列表如下：

<table><tr><th>格式</th><th>说明</th></tr><tr><td>%H</td><td>commit hash</td></tr><tr><td>%h</td><td>commit的短hash</td></tr><tr><td>%T</td><td>tree hash</td></tr><tr><td>%t</td><td>tree的短hash</td></tr><tr><td>%P</td><td>parent hashes</td></tr><tr><td>%p</td><td>parent的短hashes</td></tr><tr><td>%an</td><td>作者名字</td></tr><tr><td>%aN</td><td>mailmap中对应的作者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))</td></tr><tr><td>%ae</td><td>作者邮箱</td></tr><tr><td>%aE</td><td>作者邮箱 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))</td></tr><tr><td>%ad</td><td>日期 (–date= 制定的格式)</td></tr><tr><td>%aD</td><td>日期, RFC2822格式</td></tr><tr><td>%ar</td><td>日期, 相对格式(1 day ago)</td></tr><tr><td>%at</td><td>日期, UNIX timestamp</td></tr><tr><td>%ai</td><td>日期, ISO 8601 格式</td></tr><tr><td>%cn</td><td>提交者名字</td></tr><tr><td>%cN</td><td>提交者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))</td></tr><tr><td>%ce</td><td>提交者 email</td></tr><tr><td>%cE</td><td>提交者 email (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))</td></tr><tr><td>%cd</td><td>提交日期 (–date= 制定的格式)</td></tr><tr><td>%cD</td><td>提交日期, RFC2822格式</td></tr><tr><td>%cr</td><td>提交日期, 相对格式(1 day ago)</td></tr><tr><td>%ct</td><td>提交日期, UNIX timestamp</td></tr><tr><td>%ci</td><td>提交日期, ISO 8601 格式</td></tr><tr><td>%d</td><td>ref名称</td></tr><tr><td>%e</td><td>encoding</td></tr><tr><td>%s</td><td>commit信息标题</td></tr><tr><td>%f</td><td>过滤commit信息的标题使之可以作为文件名</td></tr><tr><td>%b</td><td>commit信息内容</td></tr><tr><td>%N</td><td>commit notes</td></tr><tr><td>%gD</td><td>reflog selector, e.g., refs/stash@{1}</td></tr><tr><td>%gd</td><td>shortened reflog selector, e.g., stash@{1}</td></tr><tr><td>%gs</td><td>reflog subject</td></tr><tr><td>%Cred</td><td>切换到红色</td></tr><tr><td>%Cgreen</td><td>切换到绿色</td></tr><tr><td>%Cblue</td><td>切换到蓝色</td></tr><tr><td>%Creset</td><td>重设颜色</td></tr><tr><td>%C(…)</td><td>制定颜色, as described in color.branch.* config option</td></tr><tr><td>%m</td><td>left, right or boundary mark</td></tr><tr><td>%n</td><td>换行</td></tr><tr><td>%%</td><td>a raw %</td></tr><tr><td>%x00</td><td>print a byte from a hex code</td></tr></table>
