1. Erlang

```text
# 安装最新的erlang包源，不执行这一步，无法安装最新版本的erlang
wget https://packages.erlang-solutions.com/erlang-solutions_2.0_all.deb
sudo dpkg -i erlang-solutions_2.0_all.deb

# 安装
sudo apt update
sudo apt install erlang elixir

```
验证
```text
Erlang
# root@ip-127-0-0-1:/home/ubuntu# erl
Elixir 
# root@ip-172-31-16-35:/home/ubuntu# iex
```

2. NodeNPM

> https://github.com/yuhuajing/AllCommonTools/blob/main/NodeNpm/nvminstall.md

3. rust 

```test
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
# 安装提示，选择1（默认为1）
# 1) Proceed with installation (default)
# 2) Customize installation
# 3) Cancel installation
1 # 直接回车也可
#
# 更新环境变量
source $HOME/.cargo/env
source ~/.profile
```

4. Tools
```text
sudo apt install libtool inotify-tools gcc make automake g++
```

5. 
```text
wget https://gmplib.org/download/gmp/gmp-6.2.1.tar.bz2
# 解压
tar -xjvf gmp-6.2.1.tar.bz2
# 编译并安装
cd gmp-6.2.1 && ./configure
make && make check && make install
```

6. postgres 数据库

> https://github.com/yuhuajing/AllCommonTools/blob/main/postgresql/postsqlinstall.md

## Blockscout

1. 
```text
git clone https://github.com/blockscout/blockscout.git && cd blockscout
```
2. 
```text
mix do deps.get --force
mix do local.rebar --force
mix do deps.compile
mix do compile
```
3. 添加secret_key_base环境变量：

> export SECRET_KEY_BASE="VTIB3uHDNbvrY0+60ZWgUoUBKDn9ppLR8MI4CpRz4/qLyEFs54ktJfaNT6Z221No"

或者也可以先生成一个新的secret_key_base，生成过程中请耐心等待：

# mix 由elixir提供，请务必保证elixir成功安装
> mix phx.gen.secret

4. 环境变量

```text
export DB_HOST=127.0.0.1
export DB_PASSWORD=123456
export DB_PORT=5432
export DB_USERNAME=postgres
export ETHEREUM_JSONRPC_VARIANT=geth
export IPC_PATH=/opt/EthereumData/geth.ipc
export COIN=ETHER
export COIN_NAME=ETHER
export PORT=4000
export ETHEREUM_JSONRPC_HTTP_URL=http://127.0.0.1:8545
export ETHEREUM_JSONRPC_TRACE_URL=http://127.0.0.1:8545
export DATABASE_URL=postgresql://postgres:123456@localhost:5432/blockscout?ssl=false
export DISABLE_EXCHANGE_RATES=true
#export NETWORK_ICON=/home/ubuntu/ic_launcher_round.png
#export LOGO=/home/ubuntu/ic_launcher_round.png
```
5. 数据库迁移

> mix do ecto.drop, ecto.create, ecto.migrate
报错xxx not_found的错误的话
```text
find / -name postgis-3 // 先全局查找

psql -h localhost -p 5432 -U postgres

\c blockscout

create extension btree_gist; 在进入数据库进行测试
```

6. node 依赖
> cd apps/block_scout_web/assets && npm install && node_modules/webpack/bin/webpack.js --mode production

> cd ../explorer && npm install && cd ..

> cd ../ && mix phx.digest

7. 证书
> cd apps/block_scout_web; mix phx.gen.cert blockscout blockscout.local && cd ..
> vi /etc/hosts
```text
   127.0.0.1       localhost blockscout blockscout.local
   255.255.255.255 broadcasthost
   ::1             localhost blockscout blockscout.local
```
8. 
> mix phx.server


## 修改界面
### 首页
1. 修改表头数据
> vim /opt/blockscout/apps/block_scout_web/lib/block_scout_web/templates/layout/_topnav.html.eex
2. 修改foot数据
> vim /opt/blockscout/apps/block_scout_web/lib/block_scout_web/templates/layout/_footer.html.eex
### 账户界面

点击Tokens 
> http://xxx:4000/accounts

> vim /opt/blockscout/apps/block_scout_web/lib/block_scout_web/templates/address/index.html.eex


## 重启

> ps aux | grep phx.server | grep -v grep | awk '{print $2}'| xargs kill -15

> cd /opt/blockscout && nohup mix phx.server >> mix.log 2>&1 &

> tail -f mix.log