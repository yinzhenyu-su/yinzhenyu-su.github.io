---
title: Git 常用命令
date: 2021-07-31 09:59:15
tags:
  - [css]
category:
  - [css]
---

### CSS 如何固定导航目录

> 在博客页面中有一个很常用的布局是文章主题居中，目录居左或居右固定，那么这个布局要如何用CSS渲染出来呢
> 不多说，直接上代码

1. html
```html
<div class="wrapper">
	<div class="main-page">
		内容
	</div>
	<div class="nav-block">
		<div class="nav-inner">
			目录
		</div>
	</div>
</div>
```

2. css
  ```css
  body {
      background-color: #EEEEEE;
  }
  
  .wrapper {
      width: 400px;
      margin: auto;
      max-width: 100%;
  }
  
  .main-page {
      display: inline-block;
      height: 9999px;
      width: 400px;
      background: white;
  }
  
  .nav-block {
      display: inline-block;
      margin-left: 20px;
      position: fixed;
      top: 30px;
      background-color: white;
  }
  
  .nav-inner {
      width: 120px
  }
  ```

### Online Demo
 [点我查看](http://jsrun.net/M38Kp)
