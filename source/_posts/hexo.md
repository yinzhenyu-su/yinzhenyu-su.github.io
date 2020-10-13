---
title: 如何使用Travis CI 自动构建hexo博客
date: 2020-10-13 00:24:27
tags:
  - [hexo]
  - [travis-ci]
---

闲来无事，又开始了自己搭建博客的计划，之前断断续续用过 WordPress，typecho 等博客系统，慢慢发现自己写的文章还没有系统代码多，有很多功能自己并不能用上。现在转行做了前端，于是决定从前端的生态搞起，用 hexo 重新搭建博客页面。本篇文章主要讲一下在博客生成完之后如何使用 Travis CI 自动生成博客并提交到 gh-page 分支上。

### 操作流程

1. 在项目根目录中新建`_config.yml`文件并添加如下配置

   ```yml
   sudo: false
   language: node_js
   node_js:
     - 10 # use nodejs v10 LTS
   cache: npm
   branches:
     only:
       - master # build master branch only
   script:
     - hexo generate # generate static files
   deploy:
     provider: pages
     skip-cleanup: true
     github-token: $GH_TOKEN
     keep-history: true
     on:
       branch: master
     local-dir: public
   ```

2.
