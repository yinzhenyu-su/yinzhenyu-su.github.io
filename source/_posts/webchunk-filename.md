---
title: 解决设置 webpackChunkName 后打包异常的问题
date: 2020-11-5 19:58:54
tags:
  - [webpack]
  - [js]
  - [vue]
---

### 如何解决设置 webpackChunkName 后，打包文件异常的问题

   在配置 vue-route 时，设置了 webpackChunkName 后发现打包完成后的部分 ChunkFile 文件夹异常，经过排查后发现 `/* ChunkFileName: "anyChunkName" */` 后面没有加空格就会导致webpack解析 ChunkName 时会出错，生成了奇怪的文件夹。从而导致打出来的包有关这个ChunkName的功能都不能正常使用。

   示例代码：（注意路径前要有空格）

   ```js
   {
     name: 'About',
     path: '/About',
     component: () => import(/* webpackChunkName: "About" */ '../views/About.vue')
   }
   ```
