[TOC]

***分支在GIT中相对较难，分支就是科幻电影里面的平行宇宙，如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，我们就需要处理一些问题了！***

![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0BOGzaG4QTc4JXO0hSlwcNtujNzAvxeibSrajLYLCT6otNnHDV9xYWwA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0Ayn87woxfepOhSlUj4FQTFUsia4ic0j6aQy4Tz32PRuJ0HSVeGeUzURA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### git分支中常用指令：
```
1. # 列出所有本地分支
2. git branch

4. # 列出所有远程分支
5. git branch -r

7. # 新建一个分支，但依然停留在当前分支
8. git branch [branch-name]

10. # 新建一个分支，并切换到该分支
11. git checkout -b [branch]

13. # 合并指定分支到当前分支
14. $ git merge [branch]

16. # 删除分支
17. $ git branch -d [branch-name]

19. # 删除远程分支
20. $ git push origin --delete [branch-name]
21. $ git branch -dr [remote/branch]
```
### IDEA中操作

![](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7Ksu8UlITwMlbX3kMGtZ9p0wHNIYeTHC8aHGASoDyZO64QicslqiaMb1OJ1Z1LPoic3LBGyDIYBa7XXw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

如果同一个文件在合并分支时都被修改了则会引起冲突：解决的办法是我们可以修改冲突文件后重新提交！选择要保留他的代码还是你的代码！

master主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。