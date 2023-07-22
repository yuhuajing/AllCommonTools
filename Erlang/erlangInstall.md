# Erlang 

> https://www.erlang-solutions.com/downloads/

1. 安装asdf

> git clone https://github.com/asdf-vm/asdf.git ~/.asdf

> vim ~/.bashrc
```text
. $HOME/.asdf/asdf.sh

. $HOME/.asdf/completions/asdf.bash
```
> source ~/.bashrc

2. 增加源

```text
asdf plugin add erlang https://github.com/asdf-vm/asdf-erlang.git
asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir.git
```

3. tools
```shell
sudo apt install libssl-dev automake autoconf libncurses5-dev
```

4. install Erlang

```shell
export KERL_CONFIGURE_OPTIONS="--disable-debug --without-javac"
asdf install erlang 25.3.2.3
```

4. 安装Elixir
```shell
asdf install elixir 1.14.5-otp-25 
```

5. set global

```shell
asdf global elixir 1.14.5-otp-25
asdf global erlang 25.3.2.3
```