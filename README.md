# AllCommonTools
Install some common tools

以下网址提供所有的Ubuntu/Centos/Fedora/Kali/Debian 各个版本上的package的安装方式

> https://installati.one/ubuntu/


export DB_HOST=127.0.0.1
export DB_PASSWORD=123456
export DB_PORT=5432
export DB_USERNAME=postgres
export ETHEREUM_JSONRPC_VARIANT=geth
export COIN=ETHER
export COIN_NAME=ETHER
export PORT=14000
export ETHEREUM_JSONRPC_HTTP_URL=http://127.0.0.1:8545
export ETHEREUM_JSONRPC_TRACE_URL=http://127.0.0.1:8545
export DATABASE_URL=postgresql://postgres:123456@localhost:5432/blockscout?ssl=false
export DISABLE_EXCHANGE_RATES=true


export SECRET_KEY_BASE="VTIB3uHDNbvrY0+60ZWgUoUBKDn9ppLR8MI4CpRz4/qLyEFs54ktJfaNT6Z221No"

find / -name postgis-3

psql -h localhost -p 5432 -U postgres

create extension postgis;
create extension postgis_topology;
create extension fuzzystrmatch;
create extension address_standardizer;
create extension address_standardizer_data_us;
create extension postgis_tiger_geocoder;
create extension btree_gist;

SELECT PostGIS_full_version();


systemctl restart postgresql