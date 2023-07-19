# 设置代理
通过 go get/download 命令下载各种依赖时，经常需要访问 github/google 等网站，如果使用默认的代理，下载速度很慢，甚至无法下载，此时就需要设置国内代理以实现高效下载

## 国内常用的代理
1. https://goproxy.io/zh/
2. https://goproxy.cn
3. https://mirrors.aliyun.com/goproxy/

## 设置代理
```shell
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

## 取消代理
```shell
go env -u GOPROXY
```