# postgresql

> https://www.postgresql.org/ftp/source/

1. 下载安装包
> wget https://ftp.postgresql.org/pub/source/v15.3/postgresql-15.3.tar.gz
2. 安装工具包
> apt -y install gcc make libreadline-dev ruby zlib1g zlib1g.dev
3. 解压缩
>  tar -zxvf postgresql-15.3.tar.gz  -C /usr/local
4. 进入文件并执行验证脚本
> cd postgresql && ./configure
5. 编译二进制文件
> make && make install
6. 配置环境变量
> vim /etc/profile
> export PATH=/usr/local/pgsql/bin:$PATH
> source /etc/profile