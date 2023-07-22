1. Erlang
> https://github.com/yuhuajing/AllCommonTools/blob/main/Erlang/erlangInstall.md

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

> mix phx.gen.secret

添加环境变量

> export SECRET_KEY_BASE="l4Z2o45D9Cvz7lezp30vxu4mCXqeKzXozjJjioYzWBlXM/NHEAu9/2OyWTIM0+1Y"

4. 环境变量

```text
export ETHEREUM_JSONRPC_HTTP_URL=http://127.0.0.1:8545
export ETHEREUM_JSONRPC_TRACE_URL=http://127.0.0.1:8545
export DATABASE_URL=postgresql://postgres:postgres@localhost:5432/blockscout?ssl=false
export ETHEREUM_JSONRPC_WS_URL="ws://127.0.0.1:8545/ws"
export SECRET_KEY_BASE="l4Z2o45D9Cvz7lezp30vxu4mCXqeKzXozjJjioYzWBlXM/NHEAu9/2OyWTIM0+1Y"
export CHAIN_ID=1
export SUBNETWORK="GEN-X"
#export LOGO="/images/blockscout_logo.svg"
#export LOGO_FOOTER="/images/blockscout_logo.svg"
export COIN="ETH"
export COIN_NAME="ETHER"
export INDEXER_DISABLE_BLOCK_REWARD_FETCHER="true"
export INDEXER_DISABLE_PENDING_TRANSACTIONS_FETCHER="true"
export INDEXER_DISABLE_INTERNAL_TRANSACTIONS_FETCHER="true"
export MIX_ENV="dev"
export BLOCKSCOUT_PROTOCOL="http"
export PORT=4000
export DISABLE_EXCHANGE_RATES="true"
export POOL_SIZE=40
export POOL_SIZE_API=40
export ACCOUNT_POOL_SIZE=5
export ECTO_USE_SSL="false"
export HEART_BEAT_TIMEOUT=60
export INDEXER_MEMORY_LIMIT="3Gb"
export FETCH_REWARDS_WAY="manual"
export INDEXER_EMPTY_BLOCKS_SANITIZER_BATCH_SIZE=1000
export ETHEREUM_JSONRPC_VARIANT=geth
export IPC_PATH=/opt/EthereumData/geth.ipc
```
5. 数据库迁移

> mix do ecto.drop, ecto.create

> mix do ecto.migrate

手动安装postgrel可能会报错xxx not_found的错误的话
```text
find / -name postgis-3 // 先全局查找

psql -h localhost -p 5432 -U postgres

\c blockscout

create extension btree_gist; 在进入数据库进行测试
```

6. node 依赖
> cd apps/block_scout_web/assets && npm install && node_modules/webpack/bin/webpack.js --mode production

> cd ../../explorer && npm install

> cd ../../ && mix phx.digest

7. 证书
> cd apps/block_scout_web

> mix phx.gen.cert blockscout blockscout.local

> vi /etc/hosts

```text
   127.0.0.1       localhost blockscout blockscout.local
   255.255.255.255 broadcasthost
   ::1             localhost blockscout blockscout.local
```
8.
> cd ../../../

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