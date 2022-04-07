# Git

## 关于版本控制和 Git

版本控制系统（VCS）用于跟踪人员和团队在项目上进行协作时的更改历史记录。 当开发人员对项目进行更改时，可以随时恢复项目的任何早期版本。

开发人员可以查看项目历史记录以找出：

- 进行了哪些更改？
- 谁进行了更改？
- 何时进行了更改？
- 为什么需要更改？

在分布式版本控制系统中，每个开发人员都有项目和项目历史记录的完整副本。 与曾经流行的集中式版本控制系统不同，DVCS 不需要与中央存储库的持续连接。 Git 是最流行的分布式版本控制系统。

## Git 中的三个区域

Git本地有三个工作区域：工作目录（Working Directory）、暂存区（Stage/Index）、资源库（Repository或Git Directory）。如果在加上远程的git仓库(Remote Directory)就可以分为四个工作区域；

- 工作区（working Directory）：简单理解就是你在电脑里能看到的目录；

- 暂存区（Stage/Index）：用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息,一般存放在 .git 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）;

- 资源库（Repository或Git Directory）：安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本；
- 远程的git仓库

**基本的 Git 工作流程如下：**

1. 在工作区中修改文件；
2. 将你想要下次提交的更改进行暂存；
3. 提交更新，找到暂存区的文件，将快照永久性存储到 Git 仓库；

## Git 安装

在开始使用 Git 管理项目的版本之前，需要将它安装到计算机上。可以使用浏览器访问如下的网址，根据自己的操作系统，选择下载对应的 Git 安装包：**https://git-scm.com/downloads**

![image-20220407203932796](https://raw.githubusercontent.com/ximingx/Figurebed/master/img/202204072039892.png)

安装完 Git 之后，要做的第一件事就是设置自己的用户名和邮件地址。因为通过 Git 对项目进行版本管理的时候，Git 需要使用这些基本信息，来记录是谁对项目进行了操作：

```bash
# 设置你的用户名
git config --global user.name "username"              
# 设置你的邮箱
git config --global user.email "email@example.com"    
```

使用了 `--global` 选项，那么该命令只需要运行一次，即可永久生效， 全局使用；

通过 git config --global user.name 和 git config --global user.email 配置的用户名和邮箱地址，会被写入到 C:/Users/用户名文件夹/.gitconfig 文件中。这个文件是 Git 的全局配置文件，配置一次即可永久生效。
```bash
# 查看现有的配置
git config --list --global
```

## 基本 Git 命令

为使用 Git，开发人员使用特定命令来复制、创建、更改和合并代码。 这些命令可以直接从命令行执行，也可以使用 GitHub Desktop 等应用程序执行。 以下是使用 Git 的一些常用命令：

- `git init`初始化一个全新的 Git 存储库并开始跟踪现有目录。 它在现有目录中添加一个隐藏的子文件夹，该子文件夹包含版本控制所需的内部数据结构。
- `git clone`创建远程已存在的项目的本地副本。 克隆包括项目的所有文件、历史记录和分支。
- `git add`暂存更改。 Git 跟踪对开发人员代码库的更改，但有必要暂存更改并拍摄更改的快照，以将其包含在项目的历史记录中。 此命令执行暂存，即该两步过程的第一部分。 暂存的任何更改都将成为下一个快照的一部分，并成为项目历史记录的一部分。 通过单独暂存和提交，开发人员可以完全控制其项目的历史记录，而无需更改其编码和工作方式。
- `git commit` 将快照保存到项目历史记录中并完成更改跟踪过程。 简言之，提交就像拍照一样。 任何使用 `git add` 暂存的内容都将成为使用 `git commit` 的快照的一部分。
- **Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤**
- `git status`将更改的状态显示为未跟踪、已修改或已暂存。
- `git branch`显示正在本地处理的分支。
- `git merge`将开发线合并在一起。 此命令通常用于合并在两个不同分支上所做的更改。 例如，当开发人员想要将功能分支中的更改合并到主分支以进行部署时，他们会合并。
- `git pull`使用远程对应项的更新来更新本地开发线。 如果队友已向远程上的分支进行了提交，并且他们希望将这些更改反映到其本地环境中，则开发人员将使用此命令。
- `git push`使用本地对分支所做的任何提交来更新远程存储库。

### 示例：参与现有存储库

```bash
# download a repository on GitHub to our machine
# Replace `owner/repo` with the owner and name of the repository to clone
git clone https://github.com/owner/repo.git

# change into the `repo` directory
cd repo

# create a new branch to store any new changes
git branch my-branch

# switch to that branch (line of development)
git checkout my-branch

# make changes, for example, edit `file1.md` and `file2.md` using the text editor

# stage the changed files
git add file1.md file2.md

# take a snapshot of the staging area (anything that's been added)
git commit -m "my snapshot"

# push changes to github
git push --set-upstream origin my-branch
```

### 示例：启动新存储库并将其发布到 GitHub

首先，您需要在 GitHub 上创建一个新存储库。 更多信息请参阅“[Hello World](https://docs.github.com/cn/get-started/quickstart/hello-world)”。 **不要**使用 README、.gitignore 或许可文件初始化存储库。 这个空存储库将等待您的代码。

```bash
# create a new directory, and initialize it with git-specific functions
git init my-repo

# change into the `my-repo` directory
cd my-repo

# create the first file in the project
touch README.md

# git isn't aware of the file, stage it
git add README.md

# take a snapshot of the staging area
git commit -m "add README to initial commit"

# provide the path for the repository you created on github
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git

# push changes to github
git push --set-upstream origin main
```

### 示例：为 GitHub 的现有分支做出贡献

此示例假定您的计算机上已有一个名为 `repo` 的项目，并且自上次在本地进行更改以来，已将新分支推送到 GitHub。

```bash
# change into the `repo` directory
cd repo

# update all remote tracking branches, and the currently checked out branch
git pull

# change into the existing branch called `feature-a`
git checkout feature-a

# make changes, for example, edit `file1.md` using the text editor

# stage the changed file
git add file1.md

# take a snapshot of the staging area
git commit -m "edit file1"

# push changes to github
git push
```

## Git 分支

 **在初始化本地 Git 仓库的时候，Git 默认已经帮我们创建了一个名字叫做 master 的分支。**通常我们把这个 master 分支叫做主分支；

 在实际工作中，master 主分支的作用是：用来保存和记录整个项目已完成的功能代码；

 因此，不允许程序员直接在 master 分支上修改代码，因为这样做的风险太高，容易导致整个项目崩溃；由于程序员不能直接在 master 分支上进行功能的开发，所以就有了功能分支的概念。**功能分支指的是专门用来开发新功能的分支，它是临时从 master 主分支上分叉出来的，当新功能开发且测试完毕后，最终需要合并到 master 主分支上；**

使用如下的命令，可以查看当前 Git 仓库中所有的分支列表：

```bash
# 列出所有本地分支
# 分支名字前面的 * 号表示当前所处的分支；
git branch
```

使用如下的命令，可以基于当前分支，创建一个新的分支，**此时，新分支中的代码和当前分支完全一样**

```bash
# 新建一个分支，但依然停留在当前分支
git branch [branchname]
```

使用如下的命令，可以切换到指定的分支上进行开发：

```bash
git checkout [branchname]
```

功能分支的代码开发测试完毕之后，可以使用如下的命令，将完成后的代码合并到 master 主分支上：

```bash
# 切换到主分支
git checkout master

# 合并指定分支到当前分支
# 假设要把 C 分支的代码合并到 A 分支，则必须先切换到 A 分支上，再运行 git merge 命令，来合并 C 分支；
git merge [branchname]
```

当把功能分支的代码合并到 master 主分支上以后，就可以使用如下的命令，删除对应的功能分支：

```bash
# 删除分支
git branch -d [branchname]
```