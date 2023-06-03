---
title: "Docker Compose"
date: 2023-03-03T17:19:28+08:00
tags: [""]
categories: [""]
toc:
  enable: true
description: 
draft: true

---

<!--more-->

#安装docker

```
curl -sSL https://get.docker.com/ | sh

sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose

docker-compose --version
```

# 配置腾讯云镜像
```
vim /etc/docker/daemon.json
```
```
{
   "registry-mirrors": [
   "https://mirror.ccs.tencentyun.com"
  ]
}
```