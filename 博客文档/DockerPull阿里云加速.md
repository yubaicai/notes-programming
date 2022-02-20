### 问题

在自己机器虚拟机里面安装Docker之后pull镜像奇慢无比，网上找的方法有称为DaoCloud开发者，会给你一个独立的镜像url，你配置进去就行了，但是这个方法需要注册，比较麻烦，阿里云也提供这种方法的加速。

### 方法1

-   打开https://cr.console.aliyun.com/?spm=5176.2020520001.0.0.7QuK43#/imageList ，第一次需要设置密码
-   点击https://cr.console.aliyun.com/?spm=5176.2020520001.0.0.7QuK43#/accelerator ，这里有一个镜像加速器网址，一种办法是照操作文档操作设置就行，另一种是下面的。
-   我使用的Portainer管理的Docker,在Registries添加刚刚的加速器网址
    ![image.png](https://gitee.com/yubaicai/blog-image/raw/master/images/202112140101618.png)
-   以后下载镜像可以在界面上pull，选择刚刚添加的镜像源即可。
    ![image.png](https://gitee.com/yubaicai/blog-image/raw/master/images/202112140101108.png)

### 方法2

-   打开下面的网址：
    https://dev.aliyun.com/search.html?spm=5176.1972343.0.1.9ivyey
-   搜索一个镜像，会找到阿里云仓库的加速，点击查看详情；
-   点击下面的复制，比如redis：`docker pull registry.cn-zhangjiakou.aliyuncs.com/cytong/redis`
-   再到docker里面pull 就可以了

## 注意

这些方法导致的缺点就是在 `docker images` 出来的镜像名包含了网址，所以操作的时候也要注意一下。

或者本来想试试Vmaware使用宿主机的代理进行访问镜像源，但是设置起来还是比较麻烦，这个方法玩玩也足够了。。。。