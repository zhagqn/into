# Into Git

## 创建提交

```bash
# 初始化仓库
git init

# 初始化裸库，通常用于创建共享库
git init --bare
```

### 提交文件到暂存区

```bash
git add [filename]

# 提交所有变化包括内容修改（modified）、新文件（new），但不包括被删除的文件
git add .

# 仅监控已经被add的文件（tracked file），不提交新文件（untracked file）
git add -u

# 包括以上 git add --all
git add -A
```

### 提交文件到仓库

```bash
git commit -m "tip message"

# 将已跟踪文件直接提交
git commit -am "add && commit"

# 追加提交，不产生 commit-id
git commit --amend
```

### rebase 操作

```bash
# 将当前分支变基为目标分支，取消当前所有 commit 并保存到临时补丁
git rebase [name]

# 将当前分支最近3个 commit 合并
git rebase -i HEAD~3
```

## 版本回溯

### 查看修改、状态

```bash
# 查看仓库状态
git status

# 缩略状态
git status --short

# 查看修改
git diff
```

### 查看历史记录

```bash
git log

# 记录每一条命令
git reflog

# 详细历史记录，着色
git log --no-merges --color --stat --graph --date=format:'%Y-%m-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Cblue %s %Cgreen(%cd) %C(bold blue)<%an>%Creset' --abbrev-commit -p

# 着色历史记录
git log --no-merges --color --graph --date=format:'%Y-%m-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Cblue %s %Cgreen(%cd) %C(bold blue)<%an>%Creset' --abbrev-commit

# 可以将以上命令配置写入 ~/.gitconfig
[alias]
s = status --short
st = status
l = log --graph --all --decorate --abbrev-commit
ld = log --no-merges --color --stat --graph --date=format:'%Y-%m-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Cblue %s %Cgreen(%cd) %C(bold blue)<%an>%Creset' --abbrev-commit -p
lda = log --no-merges --color --graph --date=format:'%Y-%m-%d %H:%M:%S' --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Cblue %s %Cgreen(%cd) %C(bold blue)<%an>%Creset' --abbrev-commit
```

### 版本回退

```bash
# 回退到上一个版本
git reset HEAD^

# 重置暂存区与工作区
git reset --hard

# 回退到上一个版本，并重置暂存区与工作区
git reset --hard HEAD^

# 会退到指定版本
git reset --hard [commit]
```

### 撤销修改

```bash
# 撤销还未添加到暂存区的修改
git checkout -- [filename]

# 撤销已经添加到暂存区的修改
git checkout -- [filename]
git reset HEAD [filename]
```

##  分支

### 创建删除分支

```bash
git branch [name]

# 创建并切换分支
git checkout -b [name]

# 删除分支
git branch -d [name]

# 强制删除一个未合并分支
git branch -D [name]
```

### 查看分支

```bash
git branch

# 查看所有分支
git branch -a
```

### 分支合并

```bash
# 合并某分支到当前分支
git merge [name]

# 禁用 Fast forward
git merge --no-ff [name]
```

### 进度保存

```bash
# 保存当前工作进度，将暂存区和工作区保存起来
git stash

# 保存进度的备注
git stash save 'message'

# 显示保存进度的
git stash list

# 恢复保存的进度，并删除内容
git stash pop

# 恢复指定进度
git stash pop [stash_id]

# 恢复保存的进度，不删除内容
git stash apply
```

### 远程分支

```bash
# 查看远程库信息
git remote -v

# 本地推送分支到远程库
git push origin [name]

# 本地创建和远程对应分支
git checkout -b [local_name] origin/[remote_name]

# 建立本地分支和远程分支的关联
git branch --set upstream [local_name] origin/[remote_name]

# 删除远程分支
git push origin -d [name]
```
