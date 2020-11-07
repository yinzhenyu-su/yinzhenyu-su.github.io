---
title: iptables 用法简介
date: 2018-11-19 16:16:00
tags:
  - [linux iptables]
---

### 清除规则

```bash
iptables -F
iptables -X
iptables -Z
```

### 设置政策

```bash
iptables -P INPUT DROP
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
```
<!--more-->
### 允许正常包,开放 0:1024 端口

```bash
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -i eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A INPUT -i eth0 -p tcp --dport 0:1024 -j ACCEPT
```

### 开放特殊端口

```bash
ex_port="3306 6379 5000 8000 8080"
for t in $ex_port
do
 iptables -A INPUT -i eth0 -p tcp --dport $t -j ACCEPT
 iptables -A INPUT -i eth0 -p udp --dport $t -j ACCEPT
done
```

### icmp 设置

```bash
icmp_type="0 3 4 11 12 14 16 18"
for t in $icmp_type
do
 iptables -A INPUT -i eth0 -p icmp --icmp-type $t -j ACCEPT
done

iptables -A INPUT -i eth0 -p icmp --icmp-type 8 -j DROP
```
