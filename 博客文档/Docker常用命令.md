# Docker 目录

## 资源汇总

| 类型     | 名称                | 地址                                                         |
| -------- | ------------------- | ------------------------------------------------------------ |
| 官方网站 | docker 官网         | [http://www.docker.com](http://www.docker.com/)              |
| 官方教程 | Docker windows 入门 | https://docs.docker.com/windows                              |
| 官方教程 | Docker Linux 入门   | https://docs.docker.com/linux                                |
| 官方教程 | Docker mac 入门     | https://docs.docker.com/mac                                  |
| 官方教程 | Docker 用户指引     | https://docs.docker.com/engine/userguide                     |
| 官方博客 | Docker 官方博客     | [http://blog.docker.com](http://blog.docker.com/)            |
| 官方镜像 | Docker Hub          | [https://hub.docker.com](https://hub.docker.com/)            |
| 官方开源 | Docker 开源         | https://www.docker.com/open-source                           |
| 中文资源 | Docker 中文网站     | [https://www.docker-cn.com](https://www.docker-cn.com/)      |
| 中文资源 | Docker 安装手册     | https://docs.docker-cn.com/engine/installation               |
| 国内镜像 | 网易加速器          | [http://hub-mirror.c.163.com](http://hub-mirror.c.163.com/)  |
| 国内镜像 | 官方中国加速器      | [https://registry.docker-cn.com](https://registry.docker-cn.com/) |
| 国内镜像 | ustc 的镜像         | [https://docker.mirrors.ustc.edu.cn](https://docker.mirrors.ustc.edu.cn/) |
| 国内镜像 | daocloud            | https://www.daocloud.io/mirror                               |

## Docker 常用命令

### 基础命令

#### info

显示 Docker 系统信息，包括镜像和容器数

```shell
BASH
docker info
```

#### version

显示 Docker 版本信息

```shell
BASH
docker version
```

#### search

从 Docker Hub 查找镜像

```shell
BASH
docker search [OPTIONS] TERM
```

>   OPTIONS 说明

| 参数          | 解释                              |
| ------------- | --------------------------------- |
| `--automated` | 只列出 automated build 类型的镜像 |
| `--no-trunc`  | 显示完整的镜像描述                |
| `-s`          | 列出收藏数不小于指定值的镜像      |

**样例**

```shell
BASH
docker search mssql
```

#### login

登陆到一个 Docker 镜像仓库

```shell
BASH
docker login
```

**样例**

```shell
BASH
docker login -u 用户名 -p 密码
```

#### logout

登出一个 Docker 镜像仓库

```shell
BASH
docker logout
```

#### pull

从镜像仓库中拉取或者更新指定镜像

```shell
BASH
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

>   OPTIONS 说明

| 参数                      | 解释                     |
| ------------------------- | ------------------------ |
| `-a`                      | 拉取所有 tagged 镜像     |
| `--disable-content-trust` | 忽略镜像的校验，默认开启 |

**样例**

```shell
BASH
docker pull hub.c.163.com/library/mysql:latest
```

#### push

将本地的镜像上传到镜像仓库，要先登陆到镜像仓库

```shell
BASH
docker pull NAME[:TAG|@DIGEST]
```

**样例**

```shell
BASH
docker push myapache:v1
```

### 本地镜像管理

#### images

列出本地镜像

```shell
BASH
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

>   OPTIONS 说明

| 参数         | 解释                                                         |
| ------------ | ------------------------------------------------------------ |
| `-a`         | 列出本地所有的镜像（含中间映像层，默认情况下，过滤掉中间映像层） |
| `--digests`  | 显示镜像的摘要信息                                           |
| `-f`         | 显示满足条件的镜像                                           |
| `--format`   | 指定返回值的模板文件                                         |
| `--no-trunc` | 显示完整的镜像信息                                           |
| `-q`         | 只显示镜像 ID                                                |

**样例**

```shell
BASH
docker images -a
```

| REPOSITORY                  | TAG    | IMAGE ID     | CREATED      | SIZE   |
| --------------------------- | ------ | ------------ | ------------ | ------ |
| hub.c.163.com/library/mysql | latest | 9e64176cd8a2 | 9 months ago | 407 MB |

>   各个项目说明：

| 项目         | 解释             |
| ------------ | ---------------- |
| `REPOSITORY` | 表示镜像的仓库源 |
| `TAG`        | 镜像的标签       |
| `IMAGE ID`   | 镜像 ID          |
| `CREATED`    | 镜像创建时间     |
| `SIZE`       | 镜像大小         |

同一仓库源可以有多个 TAG，代表这个仓库源的不同个版本，如 ubuntu 仓库源里，有 15.10、14.04 等多个不同的版本，我们使用 REPOSITORY:TAG 来定义不同的镜像
所以，我们如果要使用版本为 15.10 的 ubuntu 系统镜像来运行容器时，命令如下：`docker run -it ubuntu:15.10 /bin/bash`
如果要使用版本为 14.04 的 ubuntu 系统镜像来运行容器时，命令如下：`docker run -it ubuntu:14.04 /bin/bash`

#### rmi

删除本地一个或多少镜像

```shell
BASH
docker rmi [OPTIONS] IMAGE
```

>   OPTIONS 说明

| 参数         | 解释                             |
| ------------ | -------------------------------- |
| `-f`         | 强制删除                         |
| `--no-prune` | 不移除该镜像的过程镜像，默认移除 |

删除单个镜像

```shell
BASH
docker rmi 9e6
```

删除 id 为 none 的镜像

```shell
BASH
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```

强制删除 id 为 none 的镜像

```shell
BASH
docker rmi -f $(docker images | grep "^<none>" | awk "{print $3}")
```

删除全部镜像

```shell
BASH
docker rmi $(docker images -q)
```

强制删除全部镜像

```shell
BASH
docker rmi -f $(docker images -q)
```

#### build

使用 Dockerfile 创建镜像

```shell
BASH
docker build [OPTIONS] PATH | URL | -
```

>   OPTIONS 说明

| 参数                      | 解释                                               |
| ------------------------- | -------------------------------------------------- |
| `--build-arg=[]`          | 设置镜像创建时的变量                               |
| `--cpu-shares`            | 设置 CPU 使用权重                                  |
| `--cpu-period`            | 限制 CPU CFS 周期                                  |
| `--cpu-quota`             | 限制 CPU CFS 配额                                  |
| `--cpuset-cpus`           | 指定使用的 CPU id                                  |
| `--cpuset-mems`           | 指定使用的内存 id                                  |
| `--disable-content-trust` | 忽略校验，默认开启                                 |
| `-f`                      | 指定要使用的 Dockerfile 路径                       |
| `--force-rm`              | 设置镜像过程中删除中间容器                         |
| `--isolation`             | 使用容器隔离技术                                   |
| `--label=[]`              | 设置镜像使用的元数据                               |
| `-m`                      | 设置内存最大值                                     |
| `--memory-swap`           | 设置 Swap 的最大值为内存 +swap，”-1” 表示不限 swap |
| `--no-cache`              | 创建镜像的过程不使用缓存                           |
| `--pull`                  | 尝试去更新镜像的新版本                             |
| `-q`                      | 安静模式，成功后只输出镜像 ID                      |
| `--rm`                    | 设置镜像成功后删除中间容器                         |
| `--shm-size`              | 设置 /dev/shm 的大小，默认值是 64M                 |
| `--ulimit`                | Ulimit 配置                                        |

**样例**

从已经创建的容器中更新镜像，并且提交这个镜像

```shell
BASH
docker commit -m="has update" -a="shitao" ede0be5f1842 mysql:v2
```

>   OPTIONS 说明

| 参数           | 解释                                   |
| -------------- | -------------------------------------- |
| `-m`           | 提交的描述信息                         |
| `-a`           | 指定镜像作者                           |
| `ede0be5f1842` | 容器 ID (通过 `docker ps -a` 查看)     |
| `mysql:v2`     | `mysql` 镜像的仓库源名 `v2` 镜像的标签 |

**样例**

使用 Dockerfile 指令来创建一个新的镜像

我们使用命令 `docker build`，从零开始来创建一个新的镜像。为此，我们需要创建一个 Dockerfile 文件，其中包含一组指令来告诉 Docker 如何构建我们的镜像。

```shell
BASH
docker build -t imagesname:2.0 /home/shitao/file/
```

>   OPTIONS 说明

| 参数                 | 解释                                         |
| -------------------- | -------------------------------------------- |
| `-t`                 | 指定要创建的目标镜像名                       |
| `imagesname:2.0`     | `imagesname` 镜像的仓库源名 `2.0` 镜像的标签 |
| `/home/shitao/file/` | dockerfile 路径                              |

#### tag

标记本地镜像，将其归入某一仓库

```shell
BASH
docker tag 9e64176cd8a2 mysql163:2.0.1
```

>   OPTIONS 说明

| 参数             | 解释                                         |
| ---------------- | -------------------------------------------- |
| `9e64176cd8a2`   | 镜像 id (镜像名)                             |
| `mysql163:2.0.1` | `mysql163` 镜像的仓库源名 `2.0.1` 镜像的标签 |

使用 `docker images` 命令可以看到，ID 为 `9e64176cd8a2` 的镜像多个标签

#### save

将指定镜像保存成 tar 归档文件

```shell
BASH
docker save -o /home/shitao/Downloads/mysql.tar 9e64176cd8a2
```

将镜像 runoob/ubuntu:v3 生成 my_ubuntu_v3.tar 文档

>   OPTIONS 说明

| 参数                               | 解释             |
| ---------------------------------- | ---------------- |
| `9e64176cd8a2`                     | 镜像 id (镜像名) |
| `/home/shitao/Downloads/mysql.tar` | 保存的地址       |

#### import

从归档文件中创建镜像

```shell
BASH
docker import /home/shitao/Downloads/mysql.tar mysql:0.2
```

>   OPTIONS 说明

| 参数                               | 解释                                    |
| ---------------------------------- | --------------------------------------- |
| `mysql:0.2`                        | `mysql` 镜像的仓库源名 `0.2` 镜像的标签 |
| `/home/shitao/Downloads/mysql.tar` | 归档文件地址                            |

#### inspect

获取容器 / 镜像的元数据

```shell
BASH
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

>   OPTIONS 说明

| 参数     | 解释                 |
| -------- | -------------------- |
| `-f`     | 指定返回值的模板文件 |
| `-s`     | 显示总的文件大小     |
| `--type` | 为指定类型返回 JSON  |

**样例**

```shell
docker inspect 9e6
```

### 容器生命周期管理

#### run

```shell
docker run -it hub.c.163.com/library/mysql /bin/bash
```

>   OPTIONS 说明

| 参数                          | 解释                                               |
| ----------------------------- | -------------------------------------------------- |
| `-i`                          | 以交互模式运行容器，通常与 `-t` 同时使用           |
| `-t`                          | 为容器重新分配一个伪输入终端，通常与 `-i` 同时使用 |
| `hub.c.163.com/library/mysql` | 镜像名                                             |
| `-P`                          | 将容器内部使用的网络端口映射到我们使用的主机上     |
| `-d`                          | 后台运行容器，并返回容器 ID                        |

#### start

启动一个或多少已经被停止的容器

```shell
BASH
docker start {容器ID|容器名称}
```

#### stop

停止一个运行中的容器

```shell
BASH
docker stop {容器ID|容器名称}
```

#### restart

重启容器

```shell
BASH
docker restart {容器ID|容器名称}
```

#### kill

杀掉一个运行中的容器

```shell
BASH
docker kill {容器ID|容器名称}
```

#### rm

删除一个或多少容器

```shell
BASH
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

>   OPTIONS 说明

| 参数 | 解释                                      |
| ---- | ----------------------------------------- |
| `-f` | 通过 SIGKILL 信号强制删除一个运行中的容器 |
| `-l` | 移除容器间的网络连接，而非容器本身        |
| `-v` | 删除与容器关联的卷                        |

删除指定容器

```shell
BASH
docker rm {容器ID|容器名称}
```

删除所有容器

```shell
BASH
docker rm $(docker ps -a -q)
```

#### exec

在运行的容器中执行命令

```shell
BASH
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

>   OPTIONS 说明

| 参数 | 解释                          |
| ---- | ----------------------------- |
| `-d` | 分离模式：在后台运行          |
| `-i` | 即使没有附加也保持 STDIN 打开 |
| `-t` | 分配一个伪终端                |

**样例**

```shell
BASH
docker exec -it {容器ID|容器名称} /bin/bash
```

### 容器操作

#### ps

查看正在运行的容器

```shell
BASH
docker ps [OPTIONS]
```

>   OPTIONS 说明

| 参数         | 解释                         |
| ------------ | ---------------------------- |
| `-a`         | 显示所有的容器，包括未运行的 |
| `-f`         | 根据条件过滤显示的内容       |
| `--format`   | 指定返回值的模板文件         |
| `-l`         | 显示最近创建的容器           |
| `-n`         | 列出最近创建的 n 个容器      |
| `--no-trunc` | 不截断输出                   |
| `-q`         | 静默模式，只显示容器编号     |
| `-s`         | 显示总的文件大小             |

**样例**

```shell
docker ps
```

| CONTAINER ID | IMAGE                       | COMMAND              | CREATED        | STATUS       | PORTS    | NAMES               |
| ------------ | --------------------------- | -------------------- | -------------- | ------------ | -------- | ------------------- |
| 5a0ec27520c6 | hub.c.163.com/library/mysql | “docker-entrypoint…” | 12 seconds ago | Up 9 seconds | 3306/tcp | amazing_ardinghelli |

>   各个项目说明：

| 项目           | 解释         |
| -------------- | ------------ |
| `CONTAINER ID` | 容器 ID      |
| `IMAGE`        | 镜像名称     |
| `COMMAND`      | 命令         |
| `CREATED`      | 容器创建时间 |
| `PORTS`        | 端口         |
| `NAMES`        | 容器名称     |

#### inspect

获取容器 / 镜像的元数据

```shell
BASH
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

>   OPTIONS 说明

| 参数     | 解释                 |
| -------- | -------------------- |
| `-f`     | 指定返回值的模板文件 |
| `-s`     | 显示总的文件大小     |
| `--type` | 为指定类型返回 JSON  |

**样例**

```shell
docker inspect 9e6
```

#### top

查看容器中运行的进程信息，支持 ps 命令参数

```shell
BASH
docker top CONTAINER
```

#### logs

获取容器的日志

```shell
BASH
docker logs [OPTIONS] CONTAINER
```

>   OPTIONS 说明

| 参数      | 解释                       |
| --------- | -------------------------- |
| `-f`      | 跟踪日志输出               |
| `--since` | 显示某个开始时间的所有日志 |
| `-t`      | 显示时间戳                 |
| `--tail`  | 仅列出最新 N 条容器日志    |

**样例**

```shell
BASH
docker logs -f 9e6
```

[![Docker 命令](http://img.readcode.top/blog/img202112150936704.png)](https://cdn.jsdelivr.net/gh/Sitoi/cdn/img/docker_cmd_logic.png)



