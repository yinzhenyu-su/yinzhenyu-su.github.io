---
title: Git 常用命令
date: 2020-10-13 00:24:27
tags:
  - [git]
  - [terminal]
category:
  - [git]
---

### Git 常用命令

```bash
git add . // 追踪文件变更
git mv oldFileName newFileName // 重命名文件
git rm fileName // 删除文件
git stash save "stash message" // 暂存本地修改
git stash list // 展示暂存列表
git stash apply stash@{0} // 应用最新暂存到仓库，<stash@{0}>可以不加
git stash pop stash@{0} // 同上，应用最新暂存到仓库并删除改暂存
git stash drop stash@{0} // 删除暂存
git commit -m "message" // 提交文件修改信息
git branch -a // 展示所有分支信息（包括远程）
git branch -d branchName // 删除本地分支
git push --set-upstream origin branchName // 创建远程分支并提交本地分支到远程
git push --delete origin branchName // 删除远程分支
git push // 提交当前分支的本地更改
git pull // 拉取远程分支并merge到本地
git merge branchName // 将<branchName> 合并到当前分支
```