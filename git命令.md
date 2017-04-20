# 1.创建版本库:

`git init`

# 2.把文件添加到版本库:

`git add <文件名>`

`git commit -m "注释"`

# 3.查看文件差异

```
    git diff
    git diff HEAD -- 文件名 # 查看工作区和版本库里面最新版本的区别
```

# 4.查看状态

```
git status
```

# 5.显示最近到最远的提交日志

```
git log
```

## 5.1 让日志在一行显示

```
git log --pretty=oneline
```

# 6.版本回退

```
git reset --hard HEAD^
git reset --hard 版本id(git log 查出的id的前6位就行)
# HAED表示当前版本
# HEAD^ 就表示上一个版本
```

# 7. 回到未来

```
git reflog # 查看每一次命令的id
git reset --hard 版本id
```

# 8.撤销修改

```
# 1. 没有add到暂存区
# 2. 添加到暂存区后，没有提交前又修改了文件
git checkout -- 文件名 #注意； 没有--，就变成了“切换到另一个分支”的命令 其实是用版本库里的版本替换工作区的版本
# 3.add到暂存区，commit前想撤销更改
git reset HEAD 文件名
git checkout -- 文件名

#4.已经提交到版本库，利用"版本回退"的相关内容
git reset -- hard 版本号
```

# 9.删除文件

```
# 如果是提交到版本库的文件被删除
# 1. 如果确实要删除
git rm 文件名
git commit -m "注释"
# 2. 如果是误删
git checkout -- 文件名 # 用版本库里的版本替换工作区的版本
```

# 10.添加远程库

```
git remote add origin 远程库的git地址 # 远程库的名字就是origin，这是Git默认的叫法
```

# 11.把本地库推送到远程库

```
git push -u origin master # 推送到远程master分支
# 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
# 还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。由于远程库是空的，
# 我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
# 还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
# 以后再次推送时就可以省去-u 参数

# 推送到远程dev分支
git push origin dev
# 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并
```

# 12. 从远程库克隆

```
git clone git仓库地址
```

# 13. 查看远程库的信息

```
 git remote
```

# 14.查看更详细的信息

```
$ git remote -v
origin  git@github.com:xinyi1091/learngit.git (fetch)
origin  git@github.com:xinyi1091/learngit.git (push)
# 上面显示了可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址。
```

# 15.创建本地关联origin/dev的分支

```
git checkout -b dev origin/dev
# 创建本地分支dev，并且和远程origin/dev分支关联，本地dev分支的初始代码和远程的dev分支代码一样
```

# 16.创建与切换分支

```
git checkout -b 新分支名
# git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
git branch dev # 创建
git checkout dev # 切换
```

## 16.1 查看分支

```
git branch # git branch命令会列出所有分支，当前分支前面会标一个*号。
```

## 16.2 合并分支

```
git merge 待合并的分支名
```

## 16.3 查看分支的合并情况

```
git log --graph --pretty=oneline --abbrev-commit
```

## 16.4 删除分支

```
git branch -d 要删除的分支名
```

## 16.5 丢弃没有被合并过的分支

```
git branch -D <name>
```

## 16.6 禁用fast forward模式，会在merge时生成新的commitid

```
git merge --no-ff -m "注释" 要被合并的分支
# 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，
# 而fast forward合并就看不出来曾经做过合并
```

# 17. 储藏工作现场

> 经常有这样的事情发生，当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。问题是，**你不想提交**进行了一半的工作，否则以后你无法回到这个工作点。解决这个问题的办法就是`git stash`命令

```
git stash
```

## 17.1 查看现有的储藏

```
git stash list
结果:
stash@{0}: WIP on master: 049d078 added the index file
stash@{1}: WIP on master: c264051 Revert "added file_size"
stash@{2}: WIP on master: 21d80a5 added number to log
```

## 17.2 恢复现场

```
# 方法1
git stash apply  
# 如果你想应用更早的储藏，你可以通过名字指定它，像这样：git stash apply stash@{2}。
# 如果你不指明，Git 默认使用最近的储藏并尝试应用它：

git stash drop  [希望移除的分支的名字]# 上一步恢复后，stash内容并不删除，所以用这个命令删除
# 方法2
git stash pop #恢复的同时把stash内容也删了
```

# 18.多人协作的工作模式

> 1. 首先，可以试图用`git push origin branch-name`推送自己的修改；
> 2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
> 3. 如果合并有冲突，则解决冲突，并在本地提交；
> 4. 没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！

如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令

`git branch --set-upstream branch-name origin/branch-name`。

# 19. 创建标签

```
git tag <name>
```

# 20.查看所有标签

```
git tag
# 默认标签是打在最新提交的commit上的
# 给指定commitId的打标签
git tag <name> <commitId>
# 查看标签信息  注意，标签不是按时间顺序列出，而是按字母排序的
git show <标签名>
# 创建带有说明的标签，用-a指定标签名，-m指定说明文字
git tag -a v0.1 -m "version 0.1 released" 3628164
# 通过-s用私钥签名一个标签
git tag -s v0.2 -m "signed version 0.2 released" fec145a # 签名采用PGP签名，因此，必须首先安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错
```

# 21.删除标签

```
git tag -d 标签名
```

# 22. 推送标签到远程

```
git push origin <tagname>
# 一次性推送全部尚未推送到远程的本地标签
 git push origin --tags

 # 如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
 $ git tag -d v0.9
Deleted tag 'v0.9' (was 6224937)
# 然后，从远程删除。删除命令也是push，但是格式如下：
$ git push origin :refs/tags/v0.9
To git@github.com:michaelliao/learngit.git
 - [deleted]         v0.9
```

# 23.配置别名

```
git config --global alias.st status
```



