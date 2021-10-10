[TOC]

# 软件下载

> 打开 [git官网] https://git-scm.com/ 下载git对应操作系统的版本。

> 所有东西下载慢的话就可以去找镜像！

> 官网下载太慢，我们可以使用淘宝镜像下载：http://npm.taobao.org/mirrors/git-for-windows/

![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0IXktseBR7lpvVF4bibFwiaibnGxkDm0wYicPIiaZxcUe2KuibAHj83MiaWFSQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)


下载对应的版本即可安装！

安装：无脑下一步即可！安装完毕就可以使用了！

# 启动Git
安装成功后在开始菜单中会有Git项，菜单下有3个程序：任意文件夹下右键也可以看到对应的程序！
![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0jaiaAfr2pAfWtFX57kGYqR3SlNxDlAZDkCU6IOB1YAicKxHib5yGbv9zQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
Git Bash：Unix与Linux风格的命令行，使用最多，推荐最多

Git CMD：Windows风格的命令行

Git GUI：图形界面的Git，不建议初学者使用，尽量先熟悉常用命令
```

### 常用的Linux命令

平时一定要多使用这些基础的命令！

1. cd : 改变目录。
2. cd . . ：到上一个目录，直接cd进入默认目录
3. pwd : 显示当前所在的目录路径。
4. ls(ll):  都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。
5. touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。
6. rm:  删除一个文件, rm index.js 就会把index.js文件删除。
7. mkdir:  新建一个目录,就是新建一个文件夹。
8. rm -r :  删除一个文件夹, rm -r src 删除src目录
```java
rm -rf / 切勿在Linux中尝试！删除电脑中全部文件！
```
9.  mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下。
10. reset 重新初始化终端/清屏。
11. clear 清屏。
12. history 查看命令历史。
13. help 帮助。
14. exit 退出。
15. ‘#’表示注释

### Git配置
所有的配置文件，其实都保存在本地！

查看配置 git config -l

![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0GJANibs86DwYqoADdgZySGibmafR8p1XBq6ZG3t0J2wSg9icrIVVQo6dQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
#### ** 查看不同级别的配置文件：**
```sql
#查看系统config
git config --system --list
　　
#查看当前用户（global）配置
git config --global  --list
```
#### Git相关的配置文件：
1）、Git\etc\gitconfig  ：Git 安装目录下的 gitconfig     --system 系统级

2）、C:\Users\Administrator\ .gitconfig    只适用于当前登录用户的配置  --global 全局
![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0hcJS0rxj3qoCVvfDKh3WxwQJlSV3P15EIZuejraOwXLdic6NCB8X8oQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这里可以直接编辑配置文件，通过命令设置后会响应到这里。
### 设置用户名与邮箱（用户标识，必要）
当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：
```sql
git config --global user.name "kuangshen"  #名称
git config --global user.email 24736743@qq.com   #邮箱
```
只需要做一次这个设置，如果你传递了--global 选项，因为Git将总是会使用该信息来处理你在系统中所做的一切操作。如果你希望在一个特定的项目中使用不同的名称或e-mail地址，你可以在该项目中运行该命令而不要--global选项。总之--global为全局配置，不加为某个项目的特定配置。![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0zQZY37q1iaG0n7445X8YgPVvZH5AqyGvT4RgmoyIcZlJWiaLcxyDgSdQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)