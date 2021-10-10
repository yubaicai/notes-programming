# IDEA使用Maven创建Web项目

## 项目版本

-   jdk：1.8
-   mysql5.7
-   maven3.6.3
-   IntelliJ IDEA 2020.2 

## 使用maven的web框架支持构建Web项目

1.  使用maven的web框架支持构建Web项目![image-20201022205025706](https://gitee.com/tiamos/blogimage/raw/master/images/20201022205032.png)

2.  填写项目名，组名，项目存放路径![image-20201022205539548](https://gitee.com/tiamos/blogimage/raw/master/images/20201022205545.png)

3.  maven路径选择![image-20201022205743405](https://gitee.com/tiamos/blogimage/raw/master/images/20201022205743.png)

4.  项目构建完成

    ![image-20201022205843902](https://gitee.com/tiamos/blogimage/raw/master/images/20201022205844.png)

5.  导入jar包![image-20201022210109609](https://gitee.com/tiamos/blogimage/raw/master/images/20201022210109.png)

6.  创建Java项目所需文件夹

    ![image-20201022210530393](https://gitee.com/tiamos/blogimage/raw/master/images/20201022210608.png)

    ![](https://gitee.com/tiamos/blogimage/raw/master/images/20201022210608.png)

    ![image-20201022210620144](https://gitee.com/tiamos/blogimage/raw/master/images/20201022210620.png)

7.  添加Tomcat

    ![image-20201022210700211](https://gitee.com/tiamos/blogimage/raw/master/images/20201022210905.png)

    ![image-20201022211104509](https://gitee.com/tiamos/blogimage/raw/master/images/20201022211104.png)

    ![image-20201022211250763](https://gitee.com/tiamos/blogimage/raw/master/images/20201022211250.png)

    ![image-20201022211557586](https://gitee.com/tiamos/blogimage/raw/master/images/20201022211557.png)

8.  使用Maven的web框架创建的web项目不需要资源导入这一步

## 不使用maven的web框架创建项目

>    创建项目的步骤和上面是一样的只是在运行项目之前需要进行导入资源包的操作

下面进行操作

1.  添加web框架支持

    ![image-20201022212433574](https://gitee.com/tiamos/blogimage/raw/master/images/20201022212433.png)

    ![image-20201022212517675](https://gitee.com/tiamos/blogimage/raw/master/images/20201022212517.png)

2.  Module模块添加资源包![image-20201022211928175](https://gitee.com/tiamos/blogimage/raw/master/images/20201022211928.png)

3.  选择项目war包![image-20201022212649270](https://gitee.com/tiamos/blogimage/raw/master/images/20201022212649.png)

4.  新建lib文件夹![image-20201022213125293](https://gitee.com/tiamos/blogimage/raw/master/images/20201022213125.png)

5.  导入资源包

    ![image-20201022213155400](https://gitee.com/tiamos/blogimage/raw/master/images/20201022213155.png)

6.  应用即可

    ![image-20201022213211733](https://gitee.com/tiamos/blogimage/raw/master/images/20201022213211.png)