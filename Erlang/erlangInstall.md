# Erlang 

> https://www.erlang-solutions.com/downloads/

1. 添加源

> https://github.com/yuhuajing/AllCommonTools/blob/main/UbuntuSource/sourceslist.md

根据Ubuntu Version (22.04) 配置Erlang的源

```shell
deb https://packages.erlang-solutions.com/ubuntu jammy contrib
```
```shell
wget https://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc
sudo apt-key add erlang_solutions.asc
```

2. 安装Erlang

```shell
sudo apt-get update
sudo apt-get install erlang
```

3. 验证

```shell
erl
```
4. 安装Elixir
```shell
sudo apt -y install elixir
```