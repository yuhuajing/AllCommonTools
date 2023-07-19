# 端口占用

## 查看端口占用情况
```shell
lsof -i:端口号
```
更多lsof的命令
```text
lsof -i:8080：查看8080端口占用
lsof abc.txt：显示开启文件abc.txt的进程
lsof -c abc：显示abc进程现在打开的文件
lsof -c -p 1234：列出进程号为1234的进程所打开的文件
lsof -g gid：显示归属gid的进程情况
lsof +d /usr/local/：显示目录下被进程开启的文件
lsof +D /usr/local/：同上，但是会搜索目录下的目录，时间较长
lsof -d 4：显示使用fd为4的进程
lsof -i -U：显示所有打开的端口和UNIX domain文件
```

## netstat
```shell
netstat -tunlp | grep 端口号
```
```text
-t (tcp) 仅显示tcp相关选项
-u (udp)仅显示udp相关选项
-n 拒绝显示别名，能显示数字的全部转化为数字
-l 仅列出在Listen(监听)的服务状态
-p 显示建立相关链接的程序名
```

## 终结进程

> kill -9 PID
> kill -15 PID

kill -9 PID 是操作系统从内核级别强制杀死一个进程.

kill -15 PID 可以理解为操作系统发送一个通知告诉应用主动关闭.

SIGNTERM(15) 的效果是正常退出进程，退出前可以被阻塞或回调处理。并且它是Linux缺省的程序中断信号。

> ps aux | grep fake | grep -v grep | awk '{print $2}'| xargs kill -9