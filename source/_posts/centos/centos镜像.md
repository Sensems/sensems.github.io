---
title: CentOS 镜像
cover: https://gitee.com/Sensems/image-bed/raw/master/image/centos-8-2023-1-915:48:33.jpg
categories:
  - Centos
tags:
  - Centos
  - 镜像
---



# CentOS 镜像

[在线体验基于CentOS快速搭建LAMP环境去体验本教程介绍如何搭建LAMP环境，其中LAMP分别代表Linux、Apache、MySQL和PHP。](https://developer.aliyun.com/adc/scenario/6869de098ad44fc8a1560a1836a7c5f2)

## 简介

CentOS，是基于Red Hat Linux提供的可自由使用源代码的企业级Linux发行版本；是一个稳定，可预测，可管理和可复制的免费企业级计算平台。

下载地址: https://mirrors.aliyun.com/centos/

#### 相关仓库：

- CentOS过期源（centos-vault）：https://developer.aliyun.com/mirror/centos-vault
- CentOS arm源（centos-altarch）：https://developer.aliyun.com/mirror/centos-altarch/
- CentOS Stream源（centos-stream）：https://developer.aliyun.com/mirror/centos-stream
- CentOS debuginfo源（centos-debuginfo）：https://developer.aliyun.com/mirror/centos-debuginfo/

## 配置方法

> **通知：CentOS 8操作系统版本结束了生命周期（EOL），Linux社区已不再维护该操作系统版本。建议您切换到Anolis或Alinux。如果您的业务过渡期仍需要使用CentOS 8系统中的一些安装包，请根据下文切换CentOS 8的源。**

### 1. 备份

```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

### 2. 下载新的 CentOS-Base.repo 到 /etc/yum.repos.d/

##### centos8（centos8官方源已下线，建议切换centos-vault源）

```shell
wget -O /etc/yum.repos.d/CentOS-Base.repo  https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
```

或者

```shell
curl -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
```

**centos6（centos6官方源已下线，建议切换centos-vault源）**

```shell
wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-6.10.repo
```

或者

```shell
curl -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-6.10.repo
```

**CentOS 7**

```shell
wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo
```

或者

```shell
curl -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo
```

### 3. 运行 yum makecache 生成缓存

### 4. 其他

非阿里云ECS用户会出现 Couldn't resolve host 'mirrors.cloud.aliyuncs.com' 信息，不影响使用。用户也可自行修改相关配置: eg:

```shell
sed -i -e '/mirrors.cloud.aliyuncs.com/d' -e '/mirrors.aliyuncs.com/d' /etc/yum.repos.d/CentOS-Base.repo
```



## CentOS 8 结束生命周期如何切换源

### 公网用户：

```shell
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
yum clean all && yum makecache
```

### 阿里云ecs用户：

```powershell
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.cloud.aliyuncs.com/repo/Centos-vault-8.5.2111.repo
sed -i 's/mirrors.cloud.aliyuncs.com/url_tmp/g' /etc/yum.repos.d/CentOS-Base.repo && sed -i 's/mirrors.aliyun.com/mirrors.cloud.aliyuncs.com/g' /etc/yum.repos.d/CentOS-Base.repo && sed -i 's/url_tmp/mirrors.aliyun.com/g' /etc/yum.repos.d/CentOS-Base.repo
yum clean all && yum makecache
```



## 相关链接

- 官方主页: http://www.centos.org/
- 邮件列表: https://wiki.centos.org/GettingHelp/ListInfo
- 论坛: https://forums.centos.org/
- 文档: http://www.centos.org/docs/
- Wiki: http://wiki.centos.org/