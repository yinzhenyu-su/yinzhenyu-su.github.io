---
title: 如何使用Travis CI 自动构建hexo博客
date: 2020-10-13 00:24:27
tags:
  - [hexo]
  - [travis-ci]
---

## 闲来无事，又开始了自己搭建博客的计划，之前断断续续用过 WordPress，typecho 等博客系统，慢慢发现自己写的文章还没有系统代码多，有很多功能自己并不能用上。现在转行做了前端，于是决定从前端的生态搞起，用 hexo 重新搭建博客页面。本篇文章主要讲一下在博客生成完之后如何使用 Travis CI 自动生成博客并提交到 gh-page 分支上。

## title: 如何