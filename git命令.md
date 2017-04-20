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
# 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
# 还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
# 以后再次推送时就可以省去-u 参数
```

# 12. 从远程库克隆

```
git clone git仓库地址
```

# 13. 创建与切换分支

```
git checkout -b 新分支名
# git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
git branch dev # 创建
git checkout dev # 切换
```

## 13.1 查看分支

```
git branch # git branch命令会列出所有分支，当前分支前面会标一个*号。
```



