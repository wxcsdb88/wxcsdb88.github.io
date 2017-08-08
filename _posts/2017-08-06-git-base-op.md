---
layout: post
title:  "git 基本操作"
date:   2017-08-06 00:00:00
categories: Git
description: git 基本操作
keywords: git
author: wxcsdb88
---

git 基本操作命令

## 更新本地代码
### 暂存本地代码
```
git status -s
git stash
```
### 更新代码
```
git pull origin
git status -s
```
### 取出暂存代码
```
git stash pop
git status -s
```

>合并代码或解决冲突

### 重新添加代码到本地版本
```
git add -A
```

### 提交变动到本地代码仓库
```
git commit -m 'description for the commit'
git status -s
git log -p
```

### 提交本地代码到远程仓库
```
git push origin
```
