# 安装nvm node 版本管理工具

## git方式安装 nvm

1. 下载文件
> cd ~/ && git clone https://github.com/nvm-sh/nvm.git .nvm
2. 配置NVM参数
> cd ~/.nvm && chmod 777 nvm.sh &&  ./nvm.sh
3. 配置环境变量
> vim /etc/profile
```text
export NVM_DIR="$HOME/.nvm"
export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
> source /etc/profile
4. 验证
> nvm ls-remote
5. 安装node.js 安装npm
> nvm install xxx
6. 切换版本
> nvm use xxx
7. npm换源
> npm config set registry https://registry.npm.taobao.org

## Q
1. nvm ls-remote 为空 N/A时

进入 nvm.sh文件 调整下载顺序 将wget顺序前调

> vim ~/.nvm/nvm.sh
```test
nvm_download() {
  local CURL_COMPRESSED_FLAG
  if nvm_has "wget"; then
        # Emulate curl with wget
    ARGS=$(nvm_echo "$@" | command sed -e 's/--progress-bar /--progress=bar /' \
                            -e 's/--compressed //' \
                            -e 's/--fail //' \
                            -e 's/-L //' \
                            -e 's/-I /--server-response /' \
                            -e 's/-s /-q /' \
                            -e 's/-sS /-nv /' \
                            -e 's/-o /-O /' \
                            -e 's/-C - /-c /')
    # shellcheck disable=SC2086
    eval wget $ARGS
  elif nvm_has "curl"; then
    if nvm_curl_use_compression; then
      CURL_COMPRESSED_FLAG="--compressed"
    fi
    curl --fail ${CURL_COMPRESSED_FLAG:-} -q "$@"
  fi
}
```