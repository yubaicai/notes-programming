在前面的文章中已经介绍了如何在Centos下安装 Docker，本文就不多做介绍。直接开始说如何使用 Docker 安装 MySQL。

## 拉取镜像和运行

### 拉取MySQL最新镜像

```shell
docker pull mysql
```

![拉取MySQL最新镜像](https://gitee.com/rudecode/blog-image/raw/master/images/202112140018295.png)

注意：这里拉取的是`tag`为`latest`的镜像，如果我们想拉取指定版本的镜像，可以使用下面的指令。

```shell
docker pull mysql:5.7
```

这样就会拉取 5.7 版本的 MySQL了。

### 运行镜像

```shell
docker run -d --name mysql-dev -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
```

-   -p 端口映射，格式为：主机(宿主)端口:容器端口
-   –name 命名容器名称
-   -d 后台运行容器，并返回容器ID
-   -e 设置环境变量

这里我们启动了一个名为 `mysql-dev` 的 MySQL 镜像，暴露的端口为`3306`，默认账号密码为： `root:123456`

![运行MySQL镜像](https://gitee.com/rudecode/blog-image/raw/master/images/202112140018220.png)

### 进入MySQL 容器验证

```shell
docker exec -it mysql-dev /bin/bash
```

![进入MySQL容器并登录](https://gitee.com/rudecode/blog-image/raw/master/images/202112140018867.png)

上图中，我进入了镜像名为`mysql-dev`的MySQL容器。并通过启动容器的账号密码进行了登录。至此，MySQL 已经启动了，我们可以使用数据库工具（DataGrip、Navicat）来连接这个MySQL。

## 数据库工具连接不上问题解决

通过上面的步骤，MySQL已经启起来了，本地也可以正常连接。但是，当我通过数据库工具进行连接的时候，却发现怎么也无法连接上（这里只关心数据库的问题，默认服务器端口已经开启）,报错`1251 - Client does not support authentication protocol`

通过排查，发现是没有开启 数据库账号的远程登录权限。可以通过下面的几行指令进行解决。

```sql
-- 授权
grant all on *.* to 'root'@'%';
-- 刷新权限
flush privileges;
```

执行了上面的命令之后，还不能远程访问，因为Navicat只支持旧版本的加密，需要更改mysql的加密规则。

```sql
-- 更改加密规则
alter user root@'localhost' idenified by '123456' PASSWORD expire never;
-- 更新root用户密码
alter user 'root'@'%' idenified with mysql_native_password by '123456';
-- 刷新权限
flush privileges;
```

## 容器使用外挂目录

>   请注意使用外挂目录需要在创建容器的时候就指定。

如果说在刚使用 Docker 的时候，叫我给MySQL容器指定外挂目录，我肯定会问为什么。促使我使用 Docker 安装 MySQL 的主要原因就是安装简单，但我似乎忘记了*数据的重要性*。在经历了一次不小心删除MySQL容器的事故之后，我意识到了这个问题，于是我为新创建的 MySQL 容器外挂目录。

### 创建本地目录

既然要外挂目录，那么就需要在宿主机上面创建一个目录，作为外挂目录

```shell
mkdir /data/mysql/data   #创建存放数据目录
mkdir /data/mysql/conf     #创建存放配置目录
cd /data/mysql/conf
touch my.cnf  #创建mysql配置文件my.cnf
vim my.cnf
```

![image-20200623152222384](https://gitee.com/rudecode/blog-image/raw/master/images/202112140018460.png)

在 `my.cnf` 中写入下面的数据：

```shell
[mysql]

# 设置mysql客户端默认字符集
 
default-character-set=utf8
 
[mysqld]

# 设置3306端口
 
port = 3306
```

### 启动MySQL 容器

```shell
docker run 
    -p 3306:3306  
    --restart=always 
    --privileged=true 
    --name mysql-dev 
    -v /data/mysql/conf:/etc/mysql/conf.d 
    -v /data/mysql/data:/var/lib/mysql 
    -e MYSQL_ROOT_PASSWORD=123456 
    -d mysql
```

上面的命令为了方便各位阅读，如果要执行可以使用下面的指令。

```shell
docker run -p 3306:3306  --restart=always --privileged=true --name mysql-dev -v /data/mysql/conf:/etc/mysql/conf.d -v /data/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```

备注：

-   -p 端口映射，格式为：主机(宿主)端口:容器端口
-   –restart=always 设置随服务启动而启动容器
-   –name 命名容器名称
-   -v 设置挂载点，格式为：主机（宿主）目录：容器目录
-   -e 设置环境变量
-   -d 后台运行容器，并返回容器ID
-   –privileged=true 使用该参数，container内的root拥有真正的root权限
-   对于已经运行但没设置随docker服务的启动而启动容器的可以执行命令 docker update –restart=always 容器名

![启动容器](https://gitee.com/rudecode/blog-image/raw/master/images/202112140018847.png)

我们来看看 `/data/mysql/data`目录下面是否有文件：

![image-20200623153430659](https://gitee.com/rudecode/blog-image/raw/master/images/202112140018787.png)

可以看到，这么目录下面一句存在了指定文件且时间也正确，也就是说我们外挂成功了。