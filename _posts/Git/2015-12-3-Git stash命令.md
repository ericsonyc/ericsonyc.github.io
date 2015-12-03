---
layout: post
author: Ericson
date: 2015-12-3 17:04
title: Git stash命令
category: Git
tag: [linux,git]
---

问题场景：

1. 经常有这样的事发生，当你正在进行项目中某一部分工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行工作，又不想提交一半的工作；
2. 有多个用户修改同一个文件，当一个用户修改提交后，其他用户依然是在初始状态上进行更改，如果其中一个用户需要知道那个用户的更改，这时就需要获取git上的文件，但会报错，因为同一文件修改有冲突。

上述两个问题就可以用git stash来存储工作目录的中间状态。下面主要针对第一种情况进行使用：

1. 首先使用git stash存储当前工作状态
2. 用git status可以验证工作目录是否clean
3. 工作目录中的变更都保持在栈上，要查看现有的储藏，可以使用git stash list
4. 如果有多个储藏，你可以重新应用你刚刚实施的储藏，git stash apply，apply后面也可以加上list列出来的id，表示应用第一次储藏，也可以使用--index 添加索引表示第几次储藏；另一个相同的命令是：git stash pop，弹出最近的储藏应用，并移除栈。<font color="red">值得一提的是，apply命令可以应用储藏，但是不移除栈，可以使用git stash drop {id}来表示希望移除哪次储藏</font>
5. 可能你想取消应用的储藏，可以使用 git stash show -p [id] \| git apply -R，[id]为可选项，不加默认最近的储藏。（你可能想要新建一个别名，在你的git中增加一个stash-unapply命令，代码为：git config --global alias.stash-unapply '!git stash show -p \| git apply -R'）
6. 如果你储藏了一些工作，暂时不去理会，然后继续在你的分支上工作，你在重新应用工作时可能会碰到一些问题，如果尝试应用的变更是针对一个你那之后修改过的文件，你会碰到一个归并冲突并且必须去化解它。如果你想用更方便的方法来重新检验你储藏的变更，你可以运行git stash branch {branchname}，这会创建一个新的分支，检出你储藏工作时所处的提交，重新应用你的工作，如果成功，将会丢弃储藏。