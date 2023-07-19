1 安装nvm node 版本管理工具
2 git方式安装 nvm

cd ~/
1
git clone https://github.com/nvm-sh/nvm.git .nvm
1
cd ~/.nvm
1
git checkout v0.37.2
1
. ./nvm.sh
1
vim ~/.bashrc
1
export NVM_DIR="$HOME/.nvm"
export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
1
2
3
4
source ~/.bashrc
1
nvm验证

nvm ls
1
如果执行 nvm ls-remote 为空 N/A时，解决方案
进入 nvm.sh文件 调整下载顺序 将wget顺序前调

gedit nvm.sh
. ./nvm.sh
1
source ~/.bashrc
1
5.安装node.js 安装npm

使用nvm安装node
github 项目的配置要求为node版本 6.2.0-6.10.0，但是经过博主的无数个日日夜夜的试坑，还是决定安装node 8.9.0 版本 npm 6.14.2

nvm install v8.9.0
1
如果安装了多个node版本 可以使用 nvm ls 查看自己所有的安装的node版本 使用nvm use 选择版本
安装完node 后，执行 npm install npm@latest -g npm升级到最新版本
npm 切换成国内的下载源 要不太卡

npm config set registry https://registry.npm.taobao.org
华为云镜像

https://registry.npmjs.org
1
npm install npm@latest -g npm
1
npm info underscore
1
执行npm config set strict-ssl false
然后在执行更新命令