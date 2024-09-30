老师: Ameya Agashe  </br>
时间: 2024/09/29 14:00  </br>
PPT: [查看](https://www.canva.com/design/DAFw1gCEzC0/UfdUiDehqNW0dPF_bcohJg/view?utm_content=DAFw1gCEzC0&utm_campaign=designshare&utm_medium=link&utm_source=editor#1)

```
学习目标:
    为什么要使用Git？
    如何设置Git？
    Git 的基本使用方法使用
    Git branch 进行日常协作
    使用merge和rebase 合并分支
    使用GitHub 讲行团队协作
```


- [Git相关概念](#git相关概念)
  - [什么是版本控制系统(Version Control System)？](#什么是版本控制系统version-control-system)
  - [软件发布生命周期(Software Development Life Cycle, SDLC)](#软件发布生命周期software-development-life-cycle-sdlc)
  - [为什么要使用version control？](#为什么要使用version-control)
  - [Version Control词汇表](#version-control词汇表)
  - [集中式(Centralized) \& 分布式(Distributed)](#集中式centralized--分布式distributed)
- [Git概念](#git概念)
  - [什么是 Git？](#什么是-git)
  - [Git branch (Git分支)](#git-branch-git分支)
  - [Git Workflow](#git-workflow)
  - [GitSCM Local](#gitscm-local)
  - [Git \& GitHub](#git--github)
- [Git实际应用](#git实际应用)
  - [Step 0：一个点的历史 - Git Setup](#step-0一个点的历史---git-setup)
  - [Step 1:一条线的历史- commit](#step-1一条线的历史--commit)
  - [Step 2: 两条线的历史 – branch \& merge](#step-2-两条线的历史--branch--merge)
    - [branch](#branch)
    - [Merge a branch (git merge)](#merge-a-branch-git-merge)
    - [Merge conflicts](#merge-conflicts)
  - [Step 3：多条线的历史- 远程协作](#step-3多条线的历史--远程协作)
- [Ask git to ignore files](#ask-git-to-ignore-files)
- [GitHub Pull Request (PR)](#github-pull-request-pr)
- [Takeaways](#takeaways)
- [Force push](#force-push)
- [Homework / Challenges](#homework--challenges)


## Git相关概念
### 什么是版本控制系统(Version Control System)？
版本控制的意思是复制每一个有变动的版本，记录版本变更。

想象一下你正在创建一个 Word 文档或一个简单的 Python 代码。现在你要确保每次你今天开始工作时，你完成了一些代码，写了一个文档。明天早上，你开始编辑工作文档，所以除了只拥有完成的代码之外，也许还需要追踪变化、追踪更改的历史记录(-在这里可以看作是不同的版本)来帮助你回忆工作流程。

它可以让你轻松地回溯、撤销、重写、合并、分享、复制、跟踪、修复错误。


### 软件发布生命周期(Software Development Life Cycle, SDLC)
- SDLC是什么，有什么阶段？
包含了软件从开始到发布的不同阶段。它定义了一种用于提高待开发软件质量和效率的过程。因此，SDLC旨在通过最少的资源，交付出高质量的软件。为了避免产生严重项目失败后果，软件开发的生命周期通常可以被划分为如下六个阶段：
需求收集->设计->软件开发->测试和质量保证->部署->维护
这些阶段并非是静态的，它们可以进一步地被分解成多个子类别，以适应独特的开发需求与流程。

- SDLC方法
虽然SDLC通常都会遵从上述步骤，但是它们在实现方式上略有不同。常见的6种SDLC方法：
瀑布方法：顺序开发过程
敏捷方法(Agile)：以沟通和灵活性为中心，适用于目的不明确的开发
精益方法：与敏捷开发类似，但是侧重于效率、快速交付、以及迭代式开发
迭代方法(iterative)：瀑布模型的替代方案
![iterative.png](https://pics4.baidu.com/feed/6a63f6246b600c33e954d58d5b8a0d05d8f9a192.jpeg@f_auto?token=93ffe6b8340949465f0ecd5508b67c4e)
螺旋：侧重于降低软件开发过程中的各项风险
DevOps方法

[查看更多SLDC信息](https://baijiahao.baidu.com/s?id=1733313528126384989&wfr=spider&for=pc)


### 为什么要使用version control？
- 撤销改动或者回滚版本(snapshot) 文档产生修改之后，修改的内容希望被记录下来，因为删除的内容可能会希望找回，或者修改的内容经过若干版本后可能想要将文本改回到之前的某个状态。它会为每个版本提供一个snapshot，即记录每一次发生变化的部分，并形成修改的timeline，成线性可回溯。

- 回溯历史(A complete long-term history of every file that provides traceability) 在团队中，修改文档会有很多人，当发现文件有变化时，想要查看历史记录搞清楚为什么文件会变成今天的样子的时候，可以用版本控制回溯历史的任意一个snapshot，也可查找到版本修改的 who,when,why，以及修改的具体内容。

- 协同合作(via branching strategies) 协助团队共同修改文件，当两个人同时修改一个文件中的不同段落后，git可以帮助将不同的修改内容merge到一起。

- 备份（Backup） git会记录下最新的版本，当本地的内容不小心被删除，可以使用git拉取最新的内容。

### Version Control词汇表
    Repository: 项目仓库，存放所有文件的地方。
    Diff：项目的两个状态之间的差异（添加和删除）。
    Commit：项目在历史某一时刻的状态快照。使用差异记录历史上两点之间的差异。
    Branch：对项目（主分支 = 主分支）的修改与主分支并行进行，但不影响主分支。
    Merge：将变更从一个分支引入另一个分支。
    Clone：下载项目的本地副本。
    Fork：你自己的别人项目版本，你可以使用原始代码库进行修改。可能包括许多更改或仅修复一些错误。有时你最终会将这些更改合并回上游

### 集中式(Centralized) & 分布式(Distributed)
**集中式版本控制**：过去的遗迹集中式版本控制系统依赖于开发人员提交更改的中央服务器。用户喜欢集中式系统，因为它们易于设置并为管理员提供工作流程控制。集中式版本控制器，例如Subversion、CVS和Perforce，解决了在硬盘上手动存储多个副本的古老问题，但少数好处并不能超过依赖单一服务器所面临的风险。

如果项目的唯一副本损坏或停机，开发人员将无法访问代码或检索以前的版本。此外，远程提交非常慢，因为用户必须通过网络提交到中央存储库，这可能会降低系统的速度。用户还必须进入网络才能推动更改，这限制了开发人员可以在何时何地进行提交。合并和分支也很困难且令人困惑，因为贡献者必须将合并和分支作为一次签入进行跟踪。

**分布式版本控制**：快速软件开发的关键与集中式版本控制系统不同，分布式版本控制没有单点故障，因为开发人员在分布式版本控制工作站上克隆存储库，创建多个备份副本。如果源代码损坏，团队可以使用任何开发人员的克隆作为备份，从而提高安全性，因为丢失项目的全部历史记录的风险很小。

此外，由于有本地副本，开发人员可以离线提交，这为他们的个人工作流程提供了灵活性，并且不必作为一个巨大的变更集进行提交。分布式版本控制，例如 Git、Bazaar 和 Mercurial，提供了快速分支，因为与远程服务器之间没有通信，一切都是在本地驱动器上完成的。

## Git概念

### 什么是 Git？
Git 是一个分布式版本控制系统，用于跟踪软件开发期间源代码的变化。
它旨在协调程序员之间的工作，但它可用于跟踪任何文件集中的更改。其目标包括速度、数据完整性以及对分布式非线性工作流程的支持。

### Git branch (Git分支)
简单来说，Git 的分支，就是开发过程中，要选择的一条路，你可以选择和其他小伙伴一起走同一条路，也可以自己走一条路，路与路之间相互没有影响，作为路的主人，你也随时可以让两条路合并。

### Git Workflow
正常来说一个文件从本地到远程仓库的提交所需要的步骤：
![Git-01.img](https://i-blog.csdnimg.cn/blog_migrate/97933580c5a375e244077f90870ce234.png)

### GitSCM Local
Git 带有用于提交（git-gui）和浏览（gitk） 的内置 GUI 工具，但对于寻求特定平台体验的用户，还有几个第三方工具。[官网](https://git-scm.com/downloads/guis)

### Git & GitHub
- Git是一款免费、开源的**分布式版本控制系统**，用于敏捷高效地处理任何或小或大的项目。
- GitHub 是一个面向开源及私有软件项目的**托管平台**，因为只支持Git 作为唯一的版本库格式进行托管，故名GitHub。


## Git实际应用
- 用命令确认Git是否已经安装，打开任意一个command line工具
  ```bash
  git --version
  ```

### Step 0：一个点的历史 - Git Setup
- Git Global Setup
  ```bash
  git config --global user.name "your name"
  git config --global user.email "your email add"
  git config --global core.editor "code --wait"
  ```
  注意：我们使用 VSCode 作为我们的编辑器，全局它会影响你的整个计算机设置，如果没有全局设置，它只影响当前的存储库

- Git local – hands on
不加--global就可以设置local config，local config的优先级高于global config

- Setting up a repository 代码仓库
  ```bash
  git init
    OR
  git clone (remote repository only 用于拉取远端仓库)
  ```
  只有文本文件才能被Git管理，word不可以，word是复杂文件。
- git init 初始化一个全新的 Git 存储库并开始跟踪
它在现有目录中添加了一个隐藏的子文件夹`learngit`，用于存放版本控制所需的内部数据结构。
  ```bash
  mkdir learngit
  cd learngit
  pwd
  /Users/jonny/learngit
  git init
    OR 
  git clone 
  ```
- Ignoring Files
    通常，你会有一类不希望 Git 自动添加甚至显示为未跟踪的文件。这些文件通常是自动生成的文件，例如日志文件或 编译系统生成的文件。在这种情况下，你可以创建一个名为 .gitignore 的文件列表模式来匹配它们 
    
    A collection of .gitignore [templates](https://github.com/github/gitignore)

- Git Cloud Repository
  在Git 远端动手 “创建” 存储库 https://github.com/new 
  *注意：你必须有一个 github 账户*
### Step 1:一条线的历史- commit
- Git工作原理：
    git 需要两步 commit working directory 有些修改只是为了帮助手头工作，不需要track，需要被track的文件需要放在stage里面
    ```bash
    git add <file>...
    git add . （. 表示该目录下的所有文件，提交所有文件到stage）
    ```
    当所有的修改任务都完成了，double check后需要将修改作为新的版本提交
    ```bash
    git commit
    ```
    修改的内容会形成一个snapshot进入 git的repo里面(.git)

    用vscode编辑新的文件后，文件后面的 'U' 是untracked, 'A' 是Add to stage(点击加号或用git add + <文件名>) 点击commit之前要添加message信息记录版本和修改，点击commit后文件将tracked
  ```bash
  git restore <file>...  (to discard changes in working directory)
  git rm <file>... (将文件删掉，git将不再track该文件)
  git stash  (把当时的变更暂存，给一个新的stash名字保存，修改的内容放在了stash中，文件恢复到原来的状态，在vscode中你可以运用apply stash恢复刚刚修改的内容)
  ```

- Commit changes
Commit message 要有意义 回顾commit history的时候只能通过message判断commit的用处和意义,格式是有convention的（ticekt_id+description）

- Git undo changes
    ```bash
    git commit --amend (Undoing the last commit/comment)

    git rm test.txt
    git clean Remove untracked files from the working tree 
    git stash Stash the changes in a dirty working directory away git stash
    git stash list
    git stash apply
    git stash pop stash@{0}
    ```
    checkout 删除的东西想找回了，可以用checkout找回来 
    clean 建立的很多测试文件可以用clean命令批量清理掉，由于是删除命令，需要强制(-f)执行 
    revert 当需要版本回滚到之前某个版本。（git log 拿到 版本的SHA）用一个新的commit对历史记录进行回滚 revert可能会有冲突（之后的commit可能会对本次的修改有依赖，需要专门处理冲突） 
    reset 回滚到某一个之前的版本，该版本之后的所有commit都会被删掉。分soft（时间点后的所有变更都放入working folder里面）和 hard（直接删除时间点后的所有变更）

    ```bash
    git checkout .
    git clean -f
    git revert <SHA>
    git reset <SHA>
    ```

- Git status and history
  ```bash
  git status
  git diff
  git log (--all --decorate --oneline --graph)
  ```

### Step 2: 两条线的历史 – branch & merge

#### branch 
main or master branch 是主分支 

production environment your branch  ---> dev environment

合并代码到主分支是your branch合并到main or master branch

- 创建新的分支feat1
  ```bash
  git checkout -b feat1
  ```bash

- 选取分支
  ```
  git checkout <分支名>
  ```

- branching commands:
  ```bash
  git branch     (查看分支情况）
  git branch -d （删除branch）
  git checkout -b（建立branch）
  ```

- Git with branching
  >Create a branch (git branch)
  >Checkout a branch (git checkout)

  >Merge a branch (git merge)
  >Rebase a branch (git rebase)

  >Create a branch (git branch)
  >Checkout a branch (git checkout)


git branch crazy-experiment 请注意，这只会创建新分支。
要开始向其添加提交，你需要选择它使用 git checkout，然后使用标准的 git add 和 git commit 命令。
git checkout –b crazy-experiment

#### Merge a branch (git merge)
Git merge 允许你采用 git 分支创建的独立开发线路并将它们集成到一个分支中。Git merge 会将多个提交序列合并为一个统一的历史记录。在最常见的用例中，使用 git merge 来合并两个分支。
- Start a new feature
  ```bash
  git checkout -b feat1
  ```
- Edit some files
  ```bash
  git add <file>
  git commit -m "Start a feature"
  ```
- Edit some files
  ```bash
  git add <file>
  git commit -m "Finish a feature"
  ```
- Merge in the feat1 branch
  ```bash
  git checkout main
  git merge new-feature
  git branch -d new-feature
  ```

#### Merge conflicts

- 如果不想解决冲突：
  ```bash
  git merge <branch name> --abort
  git merge <branch name> --overwrite-ignore
  git merge <branch name> --no-overwrite-ignore
  ```

- 两种workflow: merge 和 rebase (无区别)
branch多了之后历史记录会非常复杂，所以需要用rebase，
rebase - A clean, linear history free of unnecessary merge commits

Merging vs. Rebasing
Rebase a branch (git rebase)

- graph---在 VSCode 中使用 git 历史插件----你可以获得更好的可视化
    [useful visualazaiton link](http://git-school.github.io/visualizing-git/#free)


### Step 3：多条线的历史- 远程协作

- Connect to remote repo
用于手动建立或去除两个repo的联系（一般情况用不到）
```bash
git clone
git remote add <name> <url>
git remote rm <name>
git remote rename <old-name> <new-name>
```

- Set up tracking branch
也可以在push的时候建立这种联系
  ```bash
  git branch -u <name>/<branch>
  ```

- Update local from remote
当 remote repo发生变化，本地会提示有更新，fetch命令用于比对本地和remote的repo是否有差异，发生了多少变更。
  ```bash
  git fetch   (check if codes in both ends are the same)
  git pull
  ```

- Update remote from local
  ```bash
  git push <name> <branch>
  git push <name> <local_branch>:<remote_branch>
  ```

- Sync (VS Code)
pull+push

- Delete a remote branch
  ```bash
  git push -d <name> <branch>
  git push <name> :<branch>
  ```


## Ask git to ignore files

- 各种文件 不属于 CODE， 如 MP3，MP4，JPEG，.exe 音频视频文件等
- 二进制文件（BINARY FILES）
- 路径 path and directory
- 需要添加 COMMIT进去 .gitignore 这个文件进去 （hidden file）
- GIT 只处理 文本格式 和 SOURCE CODE 文件


## GitHub Pull Request (PR)
如果想给别人的开源仓库贡献代码，通常是先 fork 别人的项目，然后本地修改完成提交到自己的个人 fork 仓库，最后提交 PR 等待别人合入你的代码。

拉取请求允许您向其他人介绍您已推送到 GitHub 存储库的更改。发送拉取请求后，利益相关方可以审查该组更改，讨论潜在的修改，甚至在必要时推送后续提交

Note: PR--->加入一个人工的REVIEW， 一般实际生产环境 MAIN是受到保护的，需要权限。  in github ---> click "compare & pull request" button

Benefits:
• Peer Review
• Sufficient testing and better stability
• Reducing conflicts Continuous Delivery
• Clearer responsibility

When you push your branch, got the github repo

Before you create Pull Request, please check:
• Follow coding standard (code style, naming convention, etc. )
• Have tests
• No conflict
• DO NOT leave comment blank – add summary of this PR

Code Review：
• Two ways to show diff
• Single comment vs.multiple

Comments for Code
Review:
• LGTM – look good to me
• :+1
• Markdown

The reviewer should identify errors that will cause an issue in production.
• The reviewer should verify that the stated goal of the code change aligns with the changes
being made.
• The reviewer should verify that any changes align with the team’s coding standards.
• The reviewer should look for anything they personally disagree with


Pull Request (PR) merge strategy – github flow:

> create a branch--> ADD commits -->open a pull request--> discuss & review--> Merge and Deploy


## Takeaways
• Never forget .gitignore
• Fix conflicts before PR
• Try to put all code for one function/subfunction/one bug fix in one git
commit, which also means the commit should be small enough
• Try to make sure every commit will not break the build pipeline, which means it should pass code style check and unit tests

## Force push
(偶尔遇到的情况 用本地的时间线强行rewrite remote的时间线)
```
git push -f
git push <name> + <branch_name>
git push --force-with-lease
```

## Homework / Challenges

<https://github.com/australiaitgroup/DevOpsNotes/blob/main/WK2_Git/git_exercise_1.md>

<https://github.com/australiaitgroup/DevOpsNotes/blob/main/WK2_Git/git_exercise_2.md>

<https://learngitbranching.js.org/>
