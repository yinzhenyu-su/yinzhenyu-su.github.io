---
title: Nginx 重定向到cdn服务器
date: 2022-05-06 19:16:00
tags:
  - [nginx]
category: 
  - [linux]
---

### Nginx redirect request to CDN Server

```nginx
http {

  # Split clients (approximately) equally based on
  # client ip address
  split_clients $remote_addr $cdn_host {
    33% cdn1;
    33% cdn2;
    - cdn3;
  }

  server {
    server_name example.com;

    # Use the variable defined by the split_clients block to determine
    # the rewritten hostname for requests beginning with /images/
    location /images/ {
      rewrite ^ http://$cdn_host.example.com$request_uri? permanent;
    }
    # 匹配 类似 /eg/a.png /eg/static/a.png 的路径
    # 向客户端发送一个301重定向响应
    # 客户端在接收到该响应后会到对应的Location获取资源
    location ~* ^/eg(.*).(css|js|jpg|jpeg|png)$ {
      rewrite ^ https://your.cdn.server$request_uri? permanent;
    }
  }
}
```

![image-20220506191308000](https://s3.bmp.ovh/imgs/2022/05/09/50f2ea4a19754597.gif)

![image-20220506191359992](https://s3.bmp.ovh/imgs/2022/05/09/ae66f89225270892.gif)