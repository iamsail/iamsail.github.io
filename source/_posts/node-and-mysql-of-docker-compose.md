---
title: docker-compose搭建node与mysql
date: 2017-10-15 22:27:30
categories: Docker
---
# ** preface **

本文仅仅是对我管理node与mysql的`docker-compose.yml`文件记录,作为备忘。


***************

# ** docker-compose.yml **

```
version: "2"
services:
  node:
    image: sail97/node
    ports:
      - "8888:8888"
    volumes:
      - ./app:/app
    stdin_open: true
    tty: true

  mysql:
    image: mysql:5.6
    ports:
      - "3306:3306"
    volumes:
      - ./mysql:/var/lib/mysql/
    environment:
        MYSQL_ROOT_PASSWORD : sail
    restart: always
    stdin_open: true
    tty: true
```
*******************
# ** 目录结构 **


```bash
➜  try tree -L 1
.
├── app
├── docker-compose.yml
└── mysql
```

*****************
# ** 使用 **

在项目目录下执行

`docker-compose up -d`

即可
