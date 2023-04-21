# git flow

### git-flow 的工作流程
*** 
可以定义一个完全适合你自己项目的工作流程，或者使用一个别人定义好的

### 什么是 git-flow
___
一旦安装安装 git-flow，你将会拥有一些扩展命令。这些命令会在一个预定义的顺序下自动执行多个操作。

git-flow 并不是要替代 Git，它仅仅是非常聪明有效地把标准的 Git 命令用脚本组合了起来。

严格来讲，你并不需要安装什么特别的东西就可以使用 git-flow 工作流程。你只需要了解，哪些工作流程是由哪些单独的任务所组成的，并且附带上正确的参数，以及在一个正确的顺序下简单执行那些对应的 Git 命令就可以了。当然，如果你使用 git-flow 脚本就会更加方便了，你就不需要把这些命令和顺序都记在脑子里。

### 安装 git-flow
___
参考 [official documentation](https://github.com/petervanderdoes/gitflow-avh/wiki#installing-git-flow)

### 使用git-flow
***
- 初始化
```
λ git flow init
Initialized empty Git repository in D:/gitflow/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
Hooks and filters directory? [D:/gitflow/.git/hooks]
```
- git-flow 模式会预设两个主分支在仓库中：
> master 只能用来包括产品代码。你不能直接工作在这个 master 分支上，而是在其他指定的，独立的特性分支中（这方面我们会马上谈到）。不直接提交改动到 master 分支上也是很多工作流程的一个共同的规则。

> develop 是你进行任何新的开发的基础分支。当你开始一个新的功能分支时，它将是_开发_的基础。另外，该分支也汇集所有已经完成的功能，并等待被整合到 master 分支中。
```
D:\gitflow (develop -> origin)
λ git branch
* develop
  master
```

### `git`命令与`git flow`命令
***
0. help
```
λ git flow help
usage: git flow <subcommand>

Available subcommands are:
   init      Initialize a new git repo with support for the branching model.
   feature   Manage your feature branches.
   bugfix    Manage your bugfix branches.
   release   Manage your release branches.
   hotfix    Manage your hotfix branches.
   support   Manage your support branches.
   version   Shows version information.
   config    Manage your git-flow configuration.
   log       Show log deviating from base branch.

Try 'git flow <subcommand> help' for details.
```
1. `git flow init`
```
D:\git-command\gitflow (develop -> origin)
λ git flow init
Initialized empty Git repository in D:/git-command/gitflow/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
Hooks and filters directory? [D:/git-command/gitflow/.git/hooks]

D:\git-command\gitflow (develop -> origin)
λ git branch
* develop
  master
```
等价于
```
git init
touch README.md
git add .
git commit -m "init"
git checkout -b develop master
git branch 
```

2. 创建 feature
```
git flow feature help
usage: git flow feature [list]
   or: git flow feature start
   or: git flow feature finish
   or: git flow feature publish
   or: git flow feature track
   or: git flow feature diff
   or: git flow feature rebase
   or: git flow feature checkout
   or: git flow feature pull
   or: git flow feature delete

    Manage your feature branches.

    For more specific help type the command followed by --help
```
```
git flow feature start abc
Switched to a new branch 'feature/abc'

Summary of actions:
- A new branch 'feature/abc' was created, based on 'develop'
- You are now on branch 'feature/abc'

Now, start committing on your feature. When done, use:

     git flow feature finish abc
     
git branch
  develop
* feature/abc
  master
```
等价于
```
git checkout -b feature/abc develop
Switched to a new branch 'feature/abc'

git branch
  develop
* feature/abc
  master
```
3. 删除feature
```
git flow feature delete abc
Switched to branch 'develop'
Deleted branch feature/abc (was 3a7a7cf).

Summary of actions:
- Feature branch 'feature/abc' has been deleted.
- You are now on branch 'develop'

```
等价于
```
git checkout develop
git branch -D feature/abc
```

4. 完成feature
```
git flow feature finish abc
Switched to branch 'develop'
Updating 3a7a7cf..315eccf
Fast-forward
 abc.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 abc.txt
Deleted branch feature/abc (was 315eccf).

Summary of actions:
- The feature branch 'feature/abc' was merged into 'develop'
- Feature branch 'feature/abc' has been locally deleted
- You are now on branch 'develop'

```
等价于
```
git checkout develop
git merge --no-ff feature/abc
git branch -d feature/abc
```

5. 创建 release
```
git flow release start 1.0.0
```
等价于
```
git checkout -b release/1.0.0 develop
```

6. 舍弃 release
```
git flow release abort 1.0.0
```
等价于
```
git branch -D release/1.0.0
```

7. 完成 release
```
git flow release finish 1.0.0
```
等价于
```
git checkout develop
git merge --no-ff release/1.0.0
git tag -a 1.0.0 -m "Release 1.0.0"
git checkout master
git merge --no-ff release/1.0.0
git branch -d release/1.0.0
```

8. 创建 Hotfixes
```
git flow hotfix start 1.0.1
```
等价于
```
git checkout -b hotfix/1.0.1 foo master
```
9. 完成 Hotfixes
```
git flow hotfix finish 1.0.1
```
等价于
```
git checkout master
git merge --no-ff hotfix/1.0.1
git tag 1.0.1
git checkout develop
git merge --no-ff hotfix/1.0.1
git branch -d hotfix/1.0.1
```