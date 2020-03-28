# Git

## 远程仓库

***

### 创建版本库

`git init` 命令，把当前目录变成Git可以管理的仓库

### 管理修改

`git add <file>` 命令，把工作区修改后的文件，添加到暂存区(stage)

`git commit -m <message>` 命令，把暂存区的文件，更新到版本库

### 版本回退

`git reset --hard commit_id` 命令：切换到指定版本，`commit_id` 可以是 `HEAD^` 或者 `HEAD^^` ，`HEAD` 表示当前版本，`HEAD^` 表示上一个版本。

### 历史版本，历史修改

穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

### 比较不同

`git diff filename`: 比较工作区和暂存区
`git diff HEAD — filename`: 比较工作区和版本库的最新版本

### 撤销修改

`git checkout -- file `可以丢弃工作区的修改，`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区。`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。

### 删除文件

命令`git rm`用于删除一个文件，理解为向暂存区添加一条删除指令。

### 关联远程库

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

### 克隆远程库

要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
比如：$ git clone git@github.com:michaelliao/gitskills.git
http地址为：https://github.com/michaelliao/gitskills.git

## 分支管理

***

### 创建与合并分支

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

### 解决冲突

切换到 `master` 分支后，使用 `git merge [name]` 命令无法合并成功，在 `master` 分支使用 vi 进行查看，可以看到 Git 用 `<<<<<<<，=======，>>>>>>>标记出不同分支的内容`，修改了冲突后，commit 提交，会形成一个新的节点。

### BUG 分支

正在 dev 分支上工作，这时候需要修改bug，直接不提交无法切换或生成新的分支，需要 `git stash` 暂存当前分支。
在 master 新建分支，修复 bug，然后合并到 master 分支上来。提交。然后切回 dev 分支。
使用 `git stash list` 查看暂存工作区，使用 `git stash pop` 或者 `git stash apply [id] +  git stash drop [id]` 来恢复。
p.s.这时候如果想，把 bug 修改应用到当前 dev 分支，使用 `git cherry-pick [bug branch id]` ，只合并 bug 分支进来。（此处如果有冲入，就需要解决冲突，再 commit）

### 不合并强行删除

开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除

### 基于 GitHub 的多人协作

多人协作的工作模式通常是这样：

首先，可以试图用git push origin <branch-name>推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

小结
查看远程库信息，使用git remote -v；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。