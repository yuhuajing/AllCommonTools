# Docker 容器

## 创建镜像
1. docker build 
需要准备Dockerfile文件，内部定义如何构建Docker容器
```text
runoob@runoob:~$ cat Dockerfile 
FROM    centos:6.7
MAINTAINER      Fisher "fisher@sudops.com"

RUN     /bin/echo 'root:123456' |chpasswd
RUN     useradd runoob
RUN     /bin/echo 'runoob:123456' |chpasswd
RUN     /bin/echo -e "LANG=\"en_US.UTF-8\"" >/etc/default/local
EXPOSE  22
EXPOSE  80
CMD     /usr/sbin/sshd -D
```
每个指令都会在镜像上创建一个新的层，每个指令的前缀都必须是大写

1. FROM 指定用到的镜像源--安装好预置工具的镜像包
2. RUN 

## 加入同个dockers网络
通过```--network```指定当前容器所处的网络

> docker run -itd --name test1 --network test-net ubuntu /bin/bash

## Docker push
登录自己的Docker hub 账号
> docker login

给要推送的镜像打标签--username换成自己的Dockers hub用户名
>docker tag ubuntu:18.04 username/ubuntu:18.04

查看是否成功打标签
>docker image ls

将打标签的镜像推送上去
>docker push username/ubuntu:18.04

检索查询该镜像
>docker search username/ubuntu