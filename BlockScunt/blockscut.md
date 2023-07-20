1. Erlang

```text
# 安装最新的erlang包源，不执行这一步，无法安装最新版本的erlang
wget https://packages.erlang-solutions.com/erlang-solutions_2.0_all.deb
sudo dpkg -i erlang-solutions_2.0_all.deb

# 安装
sudo apt update
sudo apt install erlang

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
cd gmp-6.2.1
./configure
make 
make check 
sudo make install
```

6. postgres 数据库

7. 