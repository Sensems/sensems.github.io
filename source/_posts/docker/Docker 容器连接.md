---
title: Docker 容器的使用
date: 2023/1/3 15:13:50
cover: https://www.helloimg.com/images/2023/01/03/oCD5cE.png
categories:
  - Docker
tags:
  - Docker
  - 容器
  - container
---

# 网络端口映射
有以下两种端口映射方式
```shell
docker run -itd -P --name centos8 dokken/centos-8 /bin/bash
```
```shell
docker run -itd -p 1000:22 --name centos8 dokken/centos-8 /bin/bash
```
## 参数说明

- -i：交互式操作
- -t: 终端
- -d: 后台运行
- -p 1000:22 :以指定的1000端口映射容器的22端口
- -P: 容器内部端口随机映射到主机端口
- --name: 容器别名
- dokken/centos-8: 容器源名称
- /bin/bash：这里我们希望有一个交互式的 Shell ，因此用的就是 /bin/bash
## 区别

- -P :是容器内部端口随机映射到主机的端口。
- -p : 是容器内部端口绑定到指定的主机端口。

另外, 我们可以指定容器绑定的网络地址, 比如绑定 127.0.0.1
```shell
docker run -itd -p 127.0.0.1:1000:22 --name centos8 dokken/centos-8 /bin/bash
```
这样我们就可以通过` 127.0.0.1:1000 `来访问容器的22端口了
