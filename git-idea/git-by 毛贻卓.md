## Git的学习感想
> **毛贻卓**
***
### 学习的背景
- 需要接触先进工具，对vscode，github，git之间的深度联动感到便捷和惊讶。
***
### 学习内容目录
- 关于分支的用途：比如修复bug，新功能开发，多人协作等等
- 关于远程和本地的连接
- 不使用vscode的情况下使用相关git指令管理仓库
***
### 学习内容
>**关于分支**
  -  查看分支：git branch
  - 创建分支：git branch "name" 
  - 切换分支：git checkout "name" 或者git switch "name" 
  - 创建+切换分支：git checkout -b "name" 或者git switch -c "name" 
  - 合并某分支到当前分支：git merge "name" 
  - 删除分支：git branch -d "name" 
  - 分支合并图：git log --graph
  - 切换分支放下当前工作：git stash
  - 回到工作现场：git stash pop
  - 把bug提交的修改“复制”到当前分支，避免重复劳动：git cherry-pick "commit"
  - 如果要丢弃一个没有被合并过的分支：git branch -D "name"强行删除
  - 本地分支和远程分支的链接：git branch --set-upstream-to "branch-name" origin/"branch-name"
  
  >**感想**
  - 没有VSCode方便，但兼容性更高不限于VSCode编译器。
***
  >**关于连接**
  - vscode内置功能可自动克隆并连接到远程
  - 使用git指令：
    - **git remote add origin git@server-name:path/repo-name.git**关联一个远程仓库
    - **git push origin master**推送本地修改到远程

>**感想**
- 这个功能十分便捷    
***
>**不使用vscode管理仓库**
- 通过**git init**将当前目录设为git可以管理的仓库，在git所管理的目录使用**git add (file),git commit -m message**来添加文件.
- 使用**git status**命令来查看当前仓库的状态
- 使用**git diff**来查看修改的内容
- **git reset --hard commit_id**可以回退到之前某一个已经提交了的版本.
- **git log**查看提价历史
- **git reflog**查看命令历史,回到未来
- **git checkout -- file**可丢掉工作区的修改
- **git reset HEAD file**把文件从暂存区回退到工作区
- **git rm**把版本库文件删掉
***
### 关于个人使用VSCode的历程
>1.使用过程中遇到以上语法只适用于删除本地分支，github上的远程分支依旧存在，在远程main分支上使用：git push origin --delete 分支名。可以删除远程分支。

>2.我和我的伙伴对git，github与VSCode的联动非常感兴趣。于是我创建了一个测试仓库模拟多人协作时的情况，来看看有哪些问题是我们学理论时没遇到的，于是我们发现了：
  - 1.其中一人删除远程分支后，另一人的VSCode中仍然显示已被删除的分支，只是打不开该分支。经过deepseek的指导，我们使用**git fetch -p**来临时解决这个问题，打开vscode设置并开启 Git: Fetch On Pull和Git: Prune On Fetch来提前更新远程分支状态。
  - 2.每次克隆仓库十分的繁琐，经过探索，我发现VSCode上有一个叫连接的功能，可以直接连接github远程仓库并进行修改无需到本地。
  
  >### 参考资料
1.廖雪峰的Git教程

2.deepseek~~的大力支持~~
