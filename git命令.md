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
