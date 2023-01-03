---
title: Docker 容器的使用
date: 2022/12/06 16:00:12
cover: https://www.helloimg.com/images/2023/01/03/oCD5cE.png
categories:
  - Docker
tags:
  - Docker
  - 容器
  - container
---

# 获取容器
我们可以使用docker pull 命令来下载 centos镜像
```shell
$ docker pull centos8
```
# 启动容器
```shell
$ docker run -it centos8 /bin/bash
```
## 参数说明

- -i：交互式操作
- -t: 终端
- centos8：centos8镜像
- /bin/bash：这里我们希望有一个交互式的 Shell ，因此用的就是 /bin/bash

如果要退出终端那就使用
```shell
$ exit
```
# 查看所有容器
```shell
$ docker ps -a
```
# 启动一个已经停止的容器
```shell
$ docker start b750bbbcfd88(容器id)
```
# 停止一个已经启动的容器
```shell
$ docker stop b750bbbcfd88(容器id)
```
# 后台运行容器(不想进入容器的时候)
```shell
$ docker -itd --name content_8 centos8 /bin/bash
```
## 参数说明

- -i：交互式操作
- -t: 终端
- -d: 后台运行
- --name: 运行时指定容器的名称
- /bin/bash：这里我们希望有一个交互式的 Shell ，因此用的就是 /bin/bash
# 进入容器
在使用参数 `-d` 时, 容器会进入后台, 这个时候如果想要进入容器内部可以使用以下命令
```shell
$ docker exec -it [容器ID] /bin/bash
```
## 参数说明

- -i：交互式操作
- -t: 终端
- /bin/bash：这里我们希望有一个交互式的 Shell ，因此用的就是 /bin/bash
# 导入和导出容器
## 导出容器
如果要导出到本地的某个容器, 可以使用 `docker export` 命令
```shell
$ docker export [容器ID] > centos8.tar
```
> 导出容器ID到本地文件的 centos8.tar

## 导入容器
```shell
$ cat docker/ubuntu.tar | docker import - test/ubuntu:v1
```
此外, 还可以通过指定URL或某个目录来导入
```shell
$ docker import http://example.com/exampleimage.tgz example/imagerepo
```
## 删除容器
```shell
$ docker rm -f [容器ID]
```
清除所有处于终止状态下的容器
```shell
$ docker container prune
```

