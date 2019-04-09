# git使用手册

## 是什么
一个源码版本管理系统,可以高效处理项目的版本管理

## 基本使用规范流程
1. 新建分支，每次开发新功能，都应该新建一个单独的分支
```
    #获取主干最新代码(每次提交前，都应该先做一次获取最新代码的操作)
    git checkout master
    git pull
    #新建一个开发分支
    git checkout -b myfeature
```
2. 提交分支commit  
分支修改后，就可以commit了
```
    git add --all
    git status
    git commit -m "描述提交信息"
```
3. 与主干同步  
分支开发过程中，经常与主干保持同步
```
    git fetch origin
    git rebase origin/master
```
4. 合并commit  
分支开发完毕后，很可能有一堆commit,但是合并到主干的时候，只希望有一个commit,这样不但清晰，也易于管理  
使用git rebase命令
git rebase -i origin/master

5. 推送到远程仓库
```
    git push --force origin myfeature
```
## 命令清单
我每天使用 Git ，但是很多命令记不住  
一般来说，日常使用只要记住下图6个命令就可以了，但是熟练使用，恐怕要记住60~100个命令。
![git常用命令](../assert/git常用命令.png)  
几个专用名词如下
+ WorkSpace : 工作区
+ Index / Stage : 暂存区
+ Repository : 仓库区(或本地仓库)
+ Remote : 远程仓库 
