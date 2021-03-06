# Git

git remote add origin {url} 添加远程仓库地址

git仓库里出现要忽略的文件时，删除本地忽略的文件，并push到remote，还原本地忽略的文件。

git push origin --delete dev\_20180802 删除远程分支

git branch -d dev\_20180802 删除本地分支

yarn config set registry [https://registry.npm.taobao.org](https://registry.npm.taobao.org)

alt + enter 全屏

git checkout -- . 清除修改

git branch -a 查看所有分支

ssh-keygen -t rsa 生成密钥

git remote add origin git@github.com:Botue/repo.git

本地强制上传到远程仓库git push -u origin master -f

git log --oneline

git log -n 3

git log --stat -1

git dif xxx.xx

git config --global alias.st status  
git config --global alias.co checkout  
git config --global alias.ci commit  
git config --global alias.br branch  
git config --global alias.rs reset

git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C\(yellow\)%d%Creset %s %Cgreen\(%cr\) %C\(bold blue\)&lt;%an&gt;%Creset' --abbrev-commit --date=relative"

git diff 6f647f79a39 HEAD

git diff 6f647f79a39^!

git log --graph --oneline

git status --short

git reset HEAD 重置暂存区

git reset HEAD blash.txt 将blash移出暂存区

git branch xxx 6f647f79a39

git commit -am'xxxxxxx' 添加并提交

git reset --hard 6f647f79a39

git branch -d xxx 删除分支

git reflog

git merge --no-ff a-branch 强制其产生一次新的提交

git log --merges

## 储藏

git stash

git stash pop 恢复位于栈顶的被储藏修改

git stash list

git stash pop stash@{1}

## .gitignore

```text
#
#Simple file path
#
somehow/xxx.txt
#
#
#
generated/
#
#
#
*.bak
#
#
#
!demo.bak
```

## 创建裸仓库

裸仓库通常可被用来充当开发者们传递提交的汇聚点，以便其他人可以从中拉回他们所做的修改。

git clone --bare /program/first-steps 创建裸仓库

## 工作区与版本库

工作区是一个包含.git子目录（内含版本库）中的目录。用git init命令在当前目录中创建版本库。

git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C\(yellow\)%d%Creset %s %Cgreen\(%cr\) %C\(bold blue\)&lt;%an&gt;%Creset' --abbrev-commit --date=relative"

![](.gitbook/assets/360截图20180315095201098.jpg)

需要配置hosts

