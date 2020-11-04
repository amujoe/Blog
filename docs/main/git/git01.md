# git - 属于我自己的指北手册



##### 现在 git 一个工程师必备的技能



以前的工作中用的基本都是 SVN 版本管理工具，但随着潮流的趋势发展越多的人加入 Git 之流。最近待业在家，也追一追热潮。

SVN 和 Git 有什么区别呢？前者事集中式的版本管理工具，后者是分布式版本控制系统，这应该也是最核心的区别吧。最大的优点呢，我用最简单的方式来形容：如果公司用的是前者，那你每次工作都必须跑到公司去，后者你就可以在家或者找个环境优雅的咖啡厅办公。

当然本篇不是来探讨 SVN 和 Git 的区别，以上也仅代表我个人的一些见解。下面是我的学习笔记：



#### 工作流

你的本地仓库, 其实有三个“区域”组成:

第一个是你的**工作区**, 就是你的工作目录, 是持有实际的文件

第二个是 git 的**暂存区**, 是你 git add 以后, 就会存在暂存区

第三个是 **HEAD** 区,  它指向你最后一次提交的commit

![git](http://rogerdudler.github.io/git-guide/img/trees.png)



#### 分支的意义

分支是将不同特性的代码分开来的. 在你创建仓库的时候, 有一个默认的分支 **master**, 在你开发的时候, 会有其他的分支(关于不同分支的命名规范, 可以点[这里](./git02.md)) , 开发完成以后, 再把它合并到 master 分支.

![](http://rogerdudler.github.io/git-guide/img/branches.png) 





##### 以下是一些常用的命令, 你必须熟记于心



#### 创建仓库

创建新文件夹，打开，然后执行以下命令,  以创建新的 git 仓库

```
git init
```

#### 

#### 检出仓库

执行如下命令以创建一个本地仓库的克隆版本

```
git clone /path/to/repository
```

如果是远端服务器上的仓库，你的命令会是这个样子

```
git clone https://github.com/amujoe/management-frame.git
```



#### 创建一个新的分支, 并切换过去

```
// 创建新的分支
git checkout -b feature/v1.0.0

// 切换到分支
git checkout feature/v1.0.0
```



#### 添加、提交

完成一部分代码功能后, 你需要及时的提交更改. 可以用以下命令:

```
git add <filename>
```

或者直接

```
git add .  / git add *
```

以上操作是提交代码到**暂存区**, 使用如下命令以实际提交改动:

```
git commit -m "改动代码的备注"
```

也可以添加、提交一起操作

```
git commit -am "改动代码的备注"
```

现在，你的改动已经提交到了 **HEAD**，但是还没到你的远端仓库.



#### 合并

假如要把代码合并到 master.  先切换到 master 分支. 执行以下代码

```
git merge feature/v1.0.0
```

也可以执行

```
git rebase feature/v1.0.0
```

要问 merge 和 rebase 的区别.  前者会把差异的 commit 节点按照时间顺序穿插合并.  后者会把 feature/v1.0.0 分支差异的节点, 都排到 master 分支的最后进行合并.



#### 推送改动

执行如下命令以将这些改动提交到远端仓库:

```
git push origin 分支名
```



#### 更新

第二天来开发时, 首先要更新远程代码到本地, 可以执行以下命令:

```
git pull origin feature/v1.0.0
```

或者

```
git fetch origin feature/v1.0.0
```

区别:

如果你在A分支, 想更新A分支, 你需要用 `git pull ` 

如果你在A分支, 想更新B分支, 你需要用 `git fetch`

`git pull` 相等于先 `git fetch` 然后 `git merge`
