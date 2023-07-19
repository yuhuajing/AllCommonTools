# 安装golang

## 安装
```shell
https://go.dev/dl/
```
下载适配的安装包
```shell
wget https://go.dev/dl/go1.20.6.linux-amd64.tar.gz
```
解压到指定路径
```shell
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.20.6.linux-amd64.tar.gz
```
配置环境变量-Linux
```shell
vim /etc/profile 
```
配置环境变量-MAC
```shell
vim ~/.bashrc
```
```shell
export GOROOT=/usr/local/go
export GOPATH=/opt/gopath
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
执行环境变量Linux
```shell
source /etc/profile 
```
执行环境变量-MAC
```shell
source ~/.bashrc
```
验证安装
```shell
go version
```
## 设置代理
通过 go get/download 命令下载各种依赖时，经常需要访问 github/google 等网站，如果使用默认的代理，下载速度很慢，甚至无法下载，此时就需要设置国内代理以实现高效下载

### 国内常用的代理
1. https://goproxy.io/zh/
2. https://goproxy.cn
3. https://mirrors.aliyun.com/goproxy/

### 设置代理
```shell
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

### 取消代理
```shell
go env -u GOPROXY
```

