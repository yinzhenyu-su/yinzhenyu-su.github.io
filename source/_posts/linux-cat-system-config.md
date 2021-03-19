---
title: 查看linux系统属性常用命令
date: 2016-09-23
tags:
  - [linux]
category: 
  - [linux]
---

```bash
uname -a // 查看内核/操作系统/CPU 信息
cat /proc/cpuinfo //查看 CPU 信息
hostname //查看计算机名

df -h //查看各分区使用情况
du -sh folderName // 查看指定目录大小
mount -t cifs -o"username=username,password=password" //path/to/samba /mnt/localPath // 挂载samba到本地目录,需要先安装cifs-tools

screen -R screenName // 连接到screenName, 若不存在则创建
screen -ls // 展示所有屏幕

lsof -i :80 // 查看80端口绑定的程序
iptables -t nat -L // 展示所有nat路由规则
iptables -t nat -D PREROUTING 1 // 删除PREROUTING规则中第一条数据

systemctl enable serviceFilePath // 启用服务
service serviceName start / stop / restart // 开启、停止、重启 服务

crontab -e // 编辑当前用户的系统计划任务
crontab -l // 展示当前用户的系统计划任务
```

<!--more-->

`free -m`
查看内存使用量和交换区使用量


`grep MemTotal /proc/meminfo`
查看内存总量

`grep MemFree /proc/meminfo`
查看空闲内存量

`uptime`
查看系统运行时间、用户数、负载

`cat /proc/loadavg`
查看系统负载磁盘和分区

`mount | column -t`
查看挂接的分区状态

`fdisk -l`
查看所有分区

`swapon -s`
查看所有交换分区


`ifconfig`
查看所有网络接口的属性

`route -n`
查看路由表

`netstat -lntp`
查看所有监听端口

`netstat -antp`
查看所有已经建立的连接

`netstat -s`
查看网络统计信息进程

`ps -ef`
查看所有进程

`last`
查看用户登录日志

`cut -d: -f1 /etc/passwd`
查看系统所有用户

`cut -d: -f1 /etc/group`
查看系统所有组

`crontab -l`
查看当前用户的计划任务服务