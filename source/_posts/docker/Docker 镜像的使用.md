---
title: Docker 镜像的使用
date: 2023/1/3 15:15:43
cover: https://www.helloimg.com/images/2023/01/03/oCD5cE.png
categories:
  - Docker
tags:
  - Docker
  - 镜像
  - images
---

# 列出镜像列表
我们可以使用 `docker images` 来列出本地主机上的镜像
```shell
$ docker images
```
![image.png](https://s2.loli.net/2023/01/03/jYuRFcMDSm1Orlx.png)
## 选项说明

- REPOSITORY: 表示镜像的仓库源
- TAG:　镜像的标签
- IMAGE ID: 镜像ID
- CREATED: 镜像的创建时间
- SIZE: 镜像大小
> 同一仓库源可以有多个 TAG，代表这个仓库源的不同个版本，如 ubuntu 仓库源里，有 15.10、14.04 等多个不同的版本，我们使用 REPOSITORY:TAG 来定义不同的镜像。

# 获取一个新的镜像
当我们在本地主机上使用一个不存在的镜像时 Docker 就会自动下载这个镜像。如果我们想预先下载这个镜像，我们可以使用 docker pull 命令来下载它。
```shell
docker pull centos:8
```
当我们在本地主机上使用一个不存在的镜像时 Docker 就会自动下载这个镜像。如果我们想预先下载这个镜像，我们可以使用 docker pull 命令来下载它。
# 查找镜像
我们可以从 Docker Hub 网站来搜索镜像，Docker Hub 网址为： [https://hub.docker.com/](https://hub.docker.com/)
我们也可以使用 docker search 命令来搜索镜像。比如我们需要一个 httpd 的镜像来作为我们的 web 服务。我们可以通过 docker search 命令搜索 httpd 来寻找适合我们的镜像。
```shell
$ docker search httpd
```
![image.png](https://s2.loli.net/2023/01/03/zlKVAxekZowgcYq.png)
## 选项说明

- NAME: 镜像仓库源名称
- DESCRIPTION: 镜像的描述
- OFFICIAL: 是否 docker 官方发布
- STARS: 类似 Github 里面的 star，表示点赞、喜欢的意思。
- AUTOMATED: 自动构建。
# 拖取镜像
```shell
$ docker pull httpd
```
下载完后我们就可以使用这个镜像了
```shell
$ docker run httpd
```
# 删除镜像
```shell
$ docker rmi httpd
```
