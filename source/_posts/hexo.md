---
title: 如何使用Travis CI 自动构建hexo博客
date: 2020-10-13 00:24:27
tags:
  - [hexo]
  - [travis-ci]
category:
  - [hexo]
---

闲来无事，又开始了自己搭建博客的计划，之前断断续续用过 WordPress，typecho 等博客系统，慢慢发现自己写的文章还没有系统代码多，有很多功能自己并不能用上。现在转行做了前端，于是决定从前端的生态搞起，用 hexo 重新搭建博客页面。本篇文章主要讲一下在博客生成完之后如何使用 Travis CI 自动生成博客并提交到 gh-page 分支上。

### 操作流程

1. 在项目根目录中新建`_config.yml`文件并添加如下配置a

   ```yml
   language: node_js
   node_js:
     - 12
   cache: npm
   os: linux # linux of windows
   dist: bionic # bionic for 18.04, focal for 20.04 ,default is xenial 16.04
   branches:
     only:
       - master # build master branch only
   before_install:
     - export TZ='Asia/Shanghai'
   install:
     - npm install
   script:
     - hexo generate # generate static files
   deploy:
     provider: pages
     skip_cleanup: true
     keep_history: true
     token: $GH_TOKEN
     on:
       branch: master
     local_dir: public
   ```
<!--more-->

2. 打开 [github token](https://github.com/settings/tokens 'github Token 配置') 设置页面生成新 token，只勾选 repo 权限即可，然后点击复制按钮将 token 复制到剪贴板上，要注意的是 token 只能查看一次，如果没有复制保存，需要重新生成 token。
   ![token列表](/images/hexo/githubTokenList.png 'token列表')
   ![生成新token](/images/hexo/newRepoToken.png '生成新token')
   ![复制新生成的token](/images/hexo/copyNewToken.png '复制新生成的token')

3. 打开 [travis-ci 官网](https://travis-ci.org) 进入仓库设置页面，添加环境变量`GH_TOKEN`值为上一步复制的 token。
   <!-- ![](/images/hexo/travis-auth.png 'travis 授权') -->

   ![travis 仓库设置](/images/hexo/travis-setting.png 'travis 仓库设置')

4. 在以上步骤完成后就可以提交本地代码到 github 了。

   ```bash
   git add .
   git commit -m 'Your Commit Message'
   get push
   ```

5. 等待 2 分钟左右就可以在 github 上看到 travis 提交的合并请求,确认后进入仓库设置页面，把 GitHub Pages 页面分支切换为`gh-page`分支。
   ![GitHub Page 设置](/images/hexo/github-gh-page.png 'GitHub Page 设置')

### 后记

> 操作完成后，每次提交代码就会自动构建并生成博客页面了。后面对于 hexo 的配置会新开一个帖子进行记录，happy coding！。
> 由于 github 国内访问速度较慢所以本网站使用了 `nginx` 反向代理。
