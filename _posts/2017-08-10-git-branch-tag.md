---
layout: post
title:  "git 分支及标签操作"
date:   2017-08-10 00:00:00
categories: Git
description: git branch tag 操作
keywords: git
author: wxcsdb88
---

git 分支查看、创建、合并及重命名等操作， tag 的查看、创建和删除等操作。

# 分支 branch

## 查看

```bash
# 查看本地仓库分支信息
git branch -a

# 查看仓库分支详情
git branch -a -vv

# 查看包含特定提交的分支
git branch --contains 4547e8e

# 查看远程分支信息
git branch -r -vv
```

## 更新

```bash
git fetch origin

# 当前分支 master
git fetch
# 合并本地master与更新的代码
git merge origin/master

# 上述操作等同于 git pull 或者 git pull origin master
```

## 比较

```bash
#　本地与远程分支对比
git diff master origin/master
# 相同分支，不同分支的文件比较
git diff sha1:file sha2:file
```

## 切换

```bash
git checkout <branch_name>
# 如果当前分支有未加入版本库或者变动的代码，checkout后会将这些变化带入切换后的分支!
```

## 创建

```bash
# 创建分支
git branch branch_name

# 以当前分支为基准，创建并检出代码到新分支
git checkout -b <branch_name>

# 以当前分支为基准,reset，创建并检出代码到新分支
git checkout -B <branch_name>

# 基于远程跟踪分支创建本地分支
git checkout --track -b <branch_name> origin/<branch_name>

```

## 推送

```bash
# 推送本地分支到远程仓库
# 推送并同步远程分支信息到本地
git push -u origin <branch_name>

# 以覆盖方式提交分支,慎用
git push -f origin <branch_name>
```

## 分支删除

### 本地分支删除

```bash
git branch -d <branch_name>

# 存在未合并的提交也删除此分支，强制删除
git branch -D <branch_name>
```

### 远程分支删除

```bash
git push origin :<branch_name>
```

## 合并

```bash
# 如果你在其他分支进行开发或修改代码，需要提交修改到master分支，则需要进行以下操作:
git checkout master
git merge branch_name

# 合并其他分支部分文件到当前分支
git checkout <version-sha> file1 file2
git status -s
git add -A
git commit -m '...'

# 安全的做法是检出一个临时分支，在分支上进行文件检出，合并后再切换回当前分支，这样就
# 保留了合并后的文件！
git checkout -b temp_branch
git checkout other_branch <version> file1 file2
# 解决冲突之类的
git checkout branch
```

## 分支重命名

### 本地分支重命名

```bash
git branch -m <old_branch_name> <new_branch_name>
```

### 删除远程分支

```bash
git push origin :<old_branch_name>
```

### 推送本地分支

```bash
git push -u origin <new_branch_name>
```

# 标签 tag

## 查看tag

```bash
git tag -l
git tag --list
```

## 创建tag

```bash
# tag 分支创建, 以当前分支为基准
git tag <tagname>
git tag -a <annotated tag message > -m <tag message> [<commit sha>]
```

## 推送tag

```bash
# 标签推送
gut push origin <tagname>
# 推送本地所有未推送的标签到远程仓库
git push origin --tags
```

## 删除tag

```bash
# tag 删除
git tag -d <tagname>

# 远程标签删除
git push origin :refs/tags/<tagname>
```
