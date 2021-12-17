>由于自己的各种需求，会频繁的使用到Docker，这就引出这篇Docker安装指南。至于为什么要写在Centos环境中的安装指南，主要是对于Windows和macOS，都有图形化安装界面。而对于Linux 和 Centos 却都需要指令安装，自己的购买的也是Centos服务器，所以这里就单说 Centos 中的 Docker 安装。

## 安装环境

-   Centos 7
-   2核 2 GiB 服务器配置

### 安装说明

其实安装 Docker 也是按照官网的步骤一步一步操作，就能安装成功，我的服务器环境是能够安装成功的。

这里先附上 Centos 安装 Docker 的官方地址：

https://docs.docker.com/install/linux/docker-ce/centos

为了节省再打开一次网页的时间，下面我就讲所有的步骤贴出来

## 详细安装步骤

### SET UP THE REPOSITORY

1.  安装必要的包

```shell
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

1.  设置稳定的仓库

```shell
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### INSTALL DOCKER ENGINE - COMMUNITY

```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```

### Start Docker

```shell
sudo systemctl start docker
```

### Stop Docker

```shell
sudo systemctl stop docker
```

## 使用国内镜像

众所周知，如果要使用 Docker 的官方镜像源，那么下载一个 `image` 不知道要等到猴年马月，反正我是等不了的。为了节省我的时间，也为了节省在座各位的时间，还是聪明的使用一个国内镜像源吧。注意：本文使用的163的Docke镜像源。

1.  打开或创建配置文件

    ```shell
    sudo vim /etc/docker/daemon.json
    ```

1.  在配置文件中新增配置

    ```shell
    "registry-mirrors": [
        "https://hub-mirror.c.163.com"
      ]
    # 如果有了 registry-mirrors 这个key，直接新增https://hub-mirror.c.163.com 这个源就可以了
    ```

1.  重启 Docker

    ```shell
    systemctl restart docker
    ```

后面使用Docker安装镜像就非常快了，敬请享用吧。