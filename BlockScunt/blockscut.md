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