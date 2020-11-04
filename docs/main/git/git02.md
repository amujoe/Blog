# git 命名规则、分支管理、提交流程





写给此时凌乱的你

git 现时代做前端必备的技能了。只会简单 add  commit  是可以临时应付一下工作，如果进行稍微有点规模的项目，多项功能并行开发，多个bug 都必须同时修复上线，你会发现你的工作流越来越乱。

俗话说：无规矩不成方圆。所以在做开发时候有一套团队的 git flow 还是比较重要的！ 近期我就在做这样的事，如果你也在做，不妨一起聊聊，不同的角度会碰撞出更漂酿的火花。

让我们进入主题：

![一路向前](https://img-crs.vchangyi.com/2020/10/28/2637bbd1afb64bd84a307b791395aa1c.jpeg)



今天重点要解决的是两个问题： **1. 代码分支管理      2. 提交流程**

**简单目录：**

**[一： 命名规范](#命名规范)**

**[二： 分支由来](#分支由来)**

**[三： 代码推送-feature](#代码推送-feature)**

**[四： 代码推送-hotfix](#代码推送-hotfix)**

**[五：开发 Vs 修bug](#开发vs修bug)**





### # 命名规范

先说说我们分支命名规范：（如下图）。 是在每个成员心中埋下一个伏笔， 以后就可以根据命名，来判断一个分支是用来开发新功能的，还是在修改 bug。

![](https://img-crs.vchangyi.com/2020/10/28/57b0c182a5ab6b18d9ad7e7303043d53.jpeg)



#### # 分支由来

命名规范有了，接下来聊聊每一分支的由来：

​        master                                    是石头缝里蹦出来的

​        develop                                  是 master 的长子

​        feature / coding01                 每次新功能开发都是从由 develop 切出来的新分支

​        hotfix / coding01                     每次修改线上 bug  都直接从 master 切一个新分支

![](https://img-crs.vchangyi.com/2020/10/28/bfb2b91dc590e87bd88cda509dba42bb.jpeg)

#### # 代码推送-feature

功能开发分支 （ feature / coding01 ）代码推送流程：

本地多人开发，必须都把 topic 分支代码合并到 feature 分支

 然后推送 test / dev 进行发布测试，

 测试 ok 之后，合并到 develop 分支等待上线。 

 上线之时，负责人合并 develop 代码到 master 上线

![](https://img-crs.vchangyi.com/2020/10/28/feaf77147d592f3a3df6af2da30ea2f3.jpeg)



#### # 代码推送-hotfix

修复完 Bug ，合并到 test / dev 测试

测试完成后直接推送到 master 发布

并同步给 develop ，（为了在开发新功能到时候，不用在出现老 Bug）

![](https://img-crs.vchangyi.com/2020/10/28/e332e0a9f240667ea27eef0038776d39.jpeg)



#### # 开发vs修bug

对比 feature 和 hotfix 分支的推送流程

![](https://img-crs.vchangyi.com/2020/10/28/76271fd12ea1c39d9480a119061dc8f9.jpeg)



#### # 写在最后

对于命名规则、分支管理、提交流程, 你了解了吗?  还有什么疑问吗?  欢迎一起讨论[请移步我的博客](https://www.jianshu.com/p/d408811c8bc0)