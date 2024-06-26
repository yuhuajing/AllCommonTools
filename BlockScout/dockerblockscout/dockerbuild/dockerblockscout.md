# Docker 容器

## 创建镜像 
docker build -t imageName:Version

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
每个指令都会在镜像上创建一个新的层，所以尽量合并语句（将多行的下载、解压等放到一个命令中执行），每个指令的前缀都必须是大写

1. FROM 指定用到的镜像源--安装好预置工具的镜像包,后续所有的操作都是基于这个包
2. RUN 在构建过程中在镜像中执行的命令，对镜像进行修改和配置
3. CMD 用于指定容器启动时默认要执行的命令，为容器提供默认行为（被最后一条CMD指令覆盖）
4. ENTRYPOINT 容器创建时的主要命令
5. EXPOSE 容器运行时监听的特定网络端口（8545 8546 5432）
6. ENV 容器内部的环境变量
7. ADD 除了文件复制，还支持解压和 URL 复制等附加功能
8. COPY 更简单和直接，用于纯粹的文件复制
9. ARG 定义在构造过程中传递给构建器的变量，这些参数可以在构建过程中通过 --build-arg 选项传递给 docker build 命令，并在 Dockerfile 中使用
```text
FROM alpine
# 定义一个参数，用于指定应用的版本号
ARG APP_VERSION=1.0
# 在容器中创建一个文件，并将应用版本号写入文件
RUN echo "Version: ${APP_VERSION}" > /app_version.txt
```
```text
docker build --build-arg APP_VERSION=2.0 -t my_app:latest .
```
> 在这个例子中，构建过程中的参数 APP_VERSION 被设置为 2.0，并在容器中创建一个文件 /app_version.txt，其中写入的内容是 Version: 2.0。

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
## 声明环境变量
```text
export MIX_ENV=prod
export ETHEREUM_JSONRPC_HTTP_URL=http://123.60.164.200:8545
export ETHEREUM_JSONRPC_TRACE_URL=http://123.60.164.200:8545
export ETHEREUM_JSONRPC_WS_URL="ws://123.60.164.200:8546"
export SECRET_KEY_BASE="l4Z2o45D9Cvz7lezp30vxu4mCXqeKzXozjJjioYzWBlXM/NHEAu9/2OyWTIM0+1Y"
export CHAIN_ID=12345
export SUBNETWORK="Orbites"
export COIN="ORB"
export COIN_NAME="ORB"
export BLOCKSCOUT_PROTOCOL="http"
export PORT=4000
export DISABLE_EXCHANGE_RATES="true"
export POOL_SIZE=40
export POOL_SIZE_API=40
export ACCOUNT_POOL_SIZE=10
export ECTO_USE_SSL="false"
export HEART_BEAT_TIMEOUT=600
export INDEXER_MEMORY_LIMIT="10GB"
export FETCH_REWARDS_WAY="manual"
```
## 构建镜像

1. 在 本地blockscout文件的docker目录下```https://github.com/blockscout/blockscout/tree/master/docker```执行```make build```构建容器。
2. ```make build```通过同路径下的DockFile文件执行容器的封装工作，将```../```的所有文件拷贝的容器内
3. 容器构建完成后，可以通过docker push推送到Docker hub
```text
docker login

docker tag blockscout xxx/blockscout:latest

docker push xxx/blockscout:latest
```

## MakeFile构建镜像
1. 拉取/build blockscout镜像
> make build

2. 启动数据库容器并建表迁移数据
> make postgres

3. 启动sc verify 容器
> make scverifier

4. 启动blockscout容器
> make start

关闭blockscout服务：
> make stop 
```

## docker-compose 构建容器
```bash
docker compose -f docker-compose.yml up --build
```

This command uses by-default `docker-compose.yml`, which builds the explorer into the Docker image and runs 6 Docker containers:

- Postgres database, which will be available at port 5432 on localhost.
- smart contract verification, which will be available at port 6379 on localhost.
- Blockscout explorer at http://localhost:4000.

## Building Docker containers from source with native smart contract verification (deprecated)

```bash
docker-compose -f docker-compose-no-rust-verification.yml up --build
```