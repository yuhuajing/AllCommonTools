# postgresql
## Docker
> docker pull postgres

> docker run --name postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres

> export DATABASE_URL="postgresql://postgres:mysecretpassword@127.0.0.1:5432/blockscout"

## 手动安装
> https://www.postgresql.org/ftp/source/

1. 下载安装包
> wget https://ftp.postgresql.org/pub/source/v14.8/postgresql-14.8.tar.gz
2. 解压缩
>  tar -zxvf postgresql-14.8.tar.gz  -C /usr/local/postgresql
3. 安装工具包
> apt -y install gcc make libreadline-dev ruby zlib1g jq
4. 进入文件并执行验证脚本
> cd /usr/local/postgresql && ./configure
在检查时出现问题按照提示进行--移除检查条件即可
5. 编译二进制文件
> make && make install
6. 配置环境变量
> vim /etc/profile

> export PATH=/usr/local/pgsql/bin:$PATH

> source /etc/profile

## 使用postgresql
1. 添加用户 创建数据库 配置数据存储位置
> groupadd postgres
2. 建立用户帐号和创建用户的起始目录
> useradd -g postgres postgres
3. 初始化用户postgres密码 默认密码 postgres
> passwd postgres
4. 建立数据存储文件夹
> mkdir /usr/local/pgsql/data
5. 改变data文件所属用户
> chown postgres /usr/local/pgsql/data  
6. 赋予文件可读权限
> chmod 700 /usr/local/pgsql/data

### 初始化数据库
1. 进入postgres用户
> su postgres
2. 初始化数据库 
> cd /usr/local/pgsql/bin && ./initdb -D /usr/local/pgsql/data
3. 启动pgsql服务
> cd /usr/local/pgsql/bin && ./pg_ctl start  -D /usr/local/pgsql/data/
4. 查看服务状态
> cd /usr/local/pgsql/bin && ./pg_ctl status  -D /usr/local/pgsql/data/
5. 修改配置文件 开启远程连接
> vim /usr/local/pgsql/data/pg_hba.conf
```shell
# IPv4 local connections:
host    all             all            all           trust
```
> vim /usr/local/pgsql/data/postgresql.conf

进入文件后，输入```/```查找```listen_addresses```,点击 ```enter```后 按键```n```向后查找， 按键```N```向前查找，找到后再次按键```enter ```定位光标。

```shell
listen_addresses = '*'
```
6. 重启数据库
> cd /usr/local/pgsql/bin && ./pg_ctl restart  -D /usr/local/pgsql/data/
7. 查看服务状态
> cd /usr/local/pgsql/bin && ./pg_ctl status  -D /usr/local/pgsql/data/

### 连接
> cd /usr/local/pgsql/bin && ./psql
 
创建数据库
> create database blockscout;

在root用户下连接数据库
>cd /usr/local/pgsql/bin && ./psql -h localhost -p 5432 -U postgres -d blockscout
