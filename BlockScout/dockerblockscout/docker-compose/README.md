# Docker-compose configuration

## 硬件
- Docker v20.10+
- Running Ethereum JSON RPC client （0.0.0.0:8545 0.0.0.0:8546）

## 启动并运行容器
1.
> docker pull yuhuajing/blockscout:latest
2. 
> docker pull postgres:latest
3. 
> docker pull ghcr.io/blockscout/smart-contract-verifier
4. 更改环境变量
```text
https://github.com/yuhuajing/AllCommonTools/blob/main/BlockScout/dockerblockscout/docker-compose/envs/common-blockscout.env/#L3
https://github.com/yuhuajing/AllCommonTools/blob/main/BlockScout/dockerblockscout/docker-compose/envs/common-blockscout.env/#L4
https://github.com/yuhuajing/AllCommonTools/blob/main/BlockScout/dockerblockscout/docker-compose/envs/common-blockscout.env/#L5
https://github.com/yuhuajing/AllCommonTools/blob/main/BlockScout/dockerblockscout/docker-compose/envs/common-blockscout.env/#L7
```
5. 启动镜像
> docker compose -f docker-compose.yml up -d
```text
23602cc7ff09   yuhuajing/blockscout:latest                            "bash -c 'bin/blocks…"   49 minutes ago   Up 49 minutes   0.0.0.0:4000->4000/tcp, :::4000->4000/tcp   blockscout
f589c9379e8d   postgres:latest                                        "docker-entrypoint.s…"   49 minutes ago   Up 49 minutes   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   postgres
dfbb4de52233   ghcr.io/blockscout/smart-contract-verifier:latest      "./smart-contract-ve…"   49 minutes ago   Up 49 minutes   0.0.0.0:8050->8050/tcp, :::8050->8050/tcp   smart-contract-verifier
```
6. 
> http://localhost:4000

## Configs for different Ethereum clients

The repo contains built-in configs for different clients without needing to build the image.

- Erigon: `docker-compose -f docker-compose-no-build-erigon.yml up -d`
- Geth: `docker-compose -f docker-compose-no-build-geth.yml up -d`
- Nethermind, OpenEthereum: `docker-compose -f docker-compose-no-build-nethermind up -d`
- Ganache: `docker-compose -f docker-compose-no-build-ganache.yml up -d`
- HardHat network: `docker-compose -f docker-compose-no-build-hardhat-network.yml up -d`
- Running only explorer without DB: `docker-compose -f docker-compose-no-build-no-db-container.yml up -d`. In this case, one container is created - for the explorer itself. And it assumes that the DB credentials are provided through `DATABASE_URL` environment variable.

All of the configs assume the Ethereum JSON RPC is running at http://localhost:8545.

In order to stop launched containers, run `docker-compose -d -f config_file.yml down`, replacing `config_file.yml` with the file name of the config which was previously launched.

You can adjust BlockScout environment variables from `./envs/common-blockscout.env`. Descriptions of the ENVs are available in [the docs](https://docs.blockscout.com/for-developers/information-and-settings/env-variables).
