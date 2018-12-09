---
title: docker-compose生成的容器立刻退出,exited with code 0
date: 2017-10-09 13:15:30
categories: Docker
---
### ** 问题 **

通过自己编写的`docker-compose.yml`管理项目。

但是生成的容器却立刻退出。

***************

### ** 解决 **

Docker镜像的缺省命令是` bash`，如果不加 `-it`,` bash `命令执行了自动会退出，加`-it `后docker命令会为容器分配一个伪终端，并接管其`stdin/stdout`支持交互操作，这时候`bash`命令不会自动退出

像不使用`docker-compose`,我们会执行类似如下的命令

`docker run -it --name node node`

但`docker-compose`需要额外配置下

需要在`docker-compose.yml`中包含以下行:

```
stdin_open: true
tty: true
```
第一个对应于` docker run `中的 -i ,第二个对应于 -t .

***************

### ** 参考 **

[Docker-Composer exited with code 0](https://stackoverflow.com/questions/37100358/docker-composer-exited-with-code-0)
[交互式shell使用Docker Compose](http://www.developerq.com/article/1497834743)
[Docker Compose—简化复杂应用的利器](http://debugo.com/docker-compose/)


