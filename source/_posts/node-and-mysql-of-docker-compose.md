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
***************

<div width="100%" align="center"><img src="/img/wx.png" alt="微信赞助二维码"></div></div>
<p style="margin-top: 0.4em; text-align: center">
      <b style="font-size: 1em;">讨论请发邮件到 lichanghangcumt@gmail.com</b>
      <b style="font-size: 1em;">未经授权，禁止转载</b>
      <b style="font-size: 1em;">通过支付宝 15262042918 赞助此文</b>
 </p>
