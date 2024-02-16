# PKUAutoElective-Docker

Adapted from [PKUAutoElective](https://github.com/zhongxinghong/PKUAutoElective)

## Build
```dockerfile
FROM python:3.8.18-slim

LABEL maintainer="https://github.com/tim4431"

ADD . /PKUAutoElective
WORKDIR /PKUAutoElective

RUN pip install --no-cache-dir \
    -i https://pypi.tuna.tsinghua.edu.cn/simple \
    -r requirements.txt

ENTRYPOINT ["/PKUAutoElective/pkuautoelective.sh"]
```

## Installation
Docker hub: [tim44/pkuautoelective](https://hub.docker.com/repository/docker/tim44/pkuautoelective-docker)
Entrypoint: pkuautoelective.sh
`chmod +x pkuautoelective.sh`

## Configuration
```
.
├── config
│   ├── config.p1.ini (copied from config.sample.ini)
│   ├── config.sample.ini
│   ├── overallconfig.ini (copied from overallconfig.sample.ini)
│   └── overallconfig.sample.ini
├── docker-compose.yml
├── keys
│   ├── apikey.json (copied from apikey.sample.json)
│   ├── apikey.sample.json
│   ├── wechatkey.json (copied from wechatkey.sample.json)
│   └── wechatkey.sample.json
├── logs
│   └── p1.log
├── pkuautoelective.sh
└── README.md
```

`config.ini`: 刷课机配置文件

`overallconfig.ini`: 全局配置文件

`apikey.json`: TT 识图 API

`wechatkey.json`: 企业微信通知

## Running
```bash
docker compose up -d
```

注意修改`docker-compose.yml`中挂载的文件夹路径
``` yaml
version: '3.8'

services:
  pixivutil2:
    image: tim44/pkuautoelective-docker
    container_name: pkuautoelective
    volumes:
      - ~/Container/pkuautoelective-docker/config:/PKUAutoElective/config
      - ~/Container/pkuautoelective-docker/logs:/PKUAutoElective/logs
      - ~/Container/pkuautoelective-docker/keys:/PKUAutoElective/keys
      - ~/Container/pkuautoelective-docker/pkuautoelective.sh:/PKUAutoElective/pkuautoelective.sh
    network_mode: host
```

## Configuration
modify `pkuautoelective.sh` to configure the behavior of the container