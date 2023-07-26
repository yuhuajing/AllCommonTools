# Docker-compose configuration

通过```docker compose -f xxx up -d```启动并运行容器

## Prerequisites

- Docker v20.10+
- Running Ethereum JSON RPC client

## Building Docker containers from source

```bash
docker compose -f docker-compose.yml up -d
```

This command uses by-default `docker-compose.yml`, which builds the explorer into the Docker image and runs 6 Docker containers:

- Postgres database, which will be available at port 5432 on localhost.
- smart contract verification, which will be available at port 8050 on localhost.
- Blockscout explorer at http://localhost:4000.

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

You can adjust BlockScout environment variables from `./envs/common-blockscout.env`. 
