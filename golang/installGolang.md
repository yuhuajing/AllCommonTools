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