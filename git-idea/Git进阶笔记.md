# Git笔记

>  —焦怡煖

## 学习背景

学会markdown

## 学习内容的目录

## 学习内容

### 第一章 Git概述
##### 1.1 何为版本控制系统
  版本控制系统是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统。
  版本系统其实最重要的是可以记录文件修改历史记录，从而让用户能够查看历史版本，方便切换版本。
##### 1.2 为什么需要版本系统
  个人开发过渡到团队协作
##### 1.3 版本控制工具
* 集中式版本控制系统
  集中式版本控制工具
  CVS、SVN(Subversion)、VSS……

集中化的版本控制系统诸如 CVS、SVN 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。多年以来，这已成为版本控制系统的标准做法。

这种做法带来了许多好处，每个人都可以在一定程度上看到项目中的其他人正在做些什么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个集中化的版本控制系统，要远比在各个客户端上维护本地数据库来得轻松容易。

事分两面，有好有坏。这么做显而易见的缺点是中央服务器的单点故障。如果服务器宕机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作。

* 分布式版本控制系统
  分布式版本控制工具
  Git、Mercurial、Bazaar、Darcs……

像 Git 这种分布式版本控制工具，客户端提取的不是最新版本的文件快照，而是把代码仓库完整地镜像下来（本地库）。这样任何一处协同工作用的文件发生故障，事后都可以用其他客户端的本地仓库进行恢复。因为每个客户端的每一次文件提取操作，实际上都是一次对整个文件仓库的完整备份。

分布式的版本控制系统出现之后，解决了集中式版本控制系统的缺陷：

1. 服务器断网的情况下也可以进行开发（因为版本控制是在本地进行的）
2. 每个客户端保存的也都是整个完整的项目（包含历史记录，更加安全）
##### 1.4 Git 发展历史
##### 1.5 Git 工作机制

![Git工作机制](C:\Users\lenovo\Desktop\Git工作机制.jpg)

工作区和暂存区文件都可以删掉

##### 1.6 Git和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般我们简称为远程库。

* 局域网
  * GitLab
* 互联网
  * GitHub（外网）
  * Gitee码云（国内网站）

### 第二章 Git安装
### 第三章 Git常用命令

| 命令名称                             | 作用         |
| :------------------------------------ | :------------ |
|git config --global user.name 用户名|设置用户签名
|git config --global user.email 邮箱|设置用户签名|
|git init|初始化本地仓库|
|git status|查看本地库状态|
|git add 文件名|添加到暂存区|
|git commit -m "日志信息" 文件名|提交到本地库|
|git reflog|查看历史记录|
|git reset --hard 版本号|版本穿梭|

##### 3.1 设置用户签名

```bash
$ git config --global user.name 用户名

$ git config --global user.email 邮箱
```

##### 3.2 初始化本地仓库

* 基本语法

  git init
  
  ```bash
  $mkdir  git-demo
  
  #创建一个git项目
  
  $cd   git-demo/
  
  #在git中打开并进入这个项目
  
  $ git init
  
  #初始化仓库
  ```

##### 3.3 查看本地库状态

###### 3.3.1 首次查看（工作区没有任何文件）

```bash
$ git status

#出现：

On branch master

#提示你当前本地库在哪个分支里,master为git的默认分支

No commits yet

#当前没有提交过任何东西

nothing to commit (create/copy files and use "git add" to track)

#没有任何东西需要提交
```

###### 3.3.2新增文件（test.txt）

```bash
$ code test.txt
```
>用vscode创建一个新的文件，文件名为test

在文件里写内容，如：
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!

* 查看当前目录下的文件
```bash
$ ll
#出现：

total 1
-rw-r--r-- 1 lenovo 197121 144 Dec  4 15:46 test.txt
```
* 查看文件内容
```bash
$ cat test.txt

#出现：

hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
```
* 查看文件最后一行

```bash
$ tail -n 1 test.txt
#出现：

hello git! hello Geek!

#注：查看文件最后x行
#tail -n x test.txt
```

###### 3.3.3 再次查看(检测到未追踪的文件)

```bash
$ git status

#出现：

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt

nothing added to commit but untracked files present (use "git add" to track)

#文件虽然有了，但是只是存在于工作区，git还从来没有追踪过这个文件

#如何追踪：git add
```

##### 3.4 添加暂存区

###### 3.4.1 将工作区文件添加到暂存区

```bash
$ git add test.txt
```

###### 3.4.2 查看状态（检测到暂存区有新文件）

```bash
$ git status

#出现：

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test.txt

#test.txt成功添加到暂存区
```

* 若我想在暂存区删除test.txt这个文件
  
  1. 根据提示：

  ```bash
   $ git rm --cached test.txt
  
  #出现：
  
  rm 'test.txt'
  ```
>表明该文件在暂存区被删除了，但工作区还有

> 拓展一下git rm命令

>以下实例从暂存区和工作区中删除 runoob.txt 文件：

>git rm runoob.txt 

>如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f。

>强行从暂存区和工作区中删除修改后的 runoob.txt 文件：

>git rm -f runoob.txt 
如果想把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单(暂存区)中删除，使用 --cached 选项即可：

>git rm --cached <file>
>以下实例从暂存区中删除 runoob.txt 文件：

>git rm --cached runoob.txt

2. 检查一下工作区还有

```bash
$ ll

#出现：

total 1
-rw-r--r-- 1 lenovo 197121 144 Dec  4 15:46 test.txt
```


3. 再查看状态

 ```bash
 
 $ git status

#出现：

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt

nothing added to commit but untracked files present (use "git add" to track)
 ```
>表明在暂存区删除成功

4. 重新添加并检查状态

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git add test.txt

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test.txt
```

##### 3.5 提交本地库

添加到暂存区，还没形成历史版本，所以要提交本地库

###### 3.5.1 将暂存区文件提交到本地库
```bash
$ git commit -m "日志信息" 文件名

$ git commit -m "first commit" test.txt

#出现：

[master (root-commit) 71a3fa7] first commit
 1 file changed, 6 insertions(+)
 create mode 100644 test.txt
```
> 说明在master这个分支下面，又一个第一次提交这么一个版本，一个文件被改变，6行内容被插入。说明文件提交成功了
>
> 其中，71a3fa7这七位数字就是版本号

###### 3.5.2查看状态（没有文件需要提交）

```bash
$ git status

#出现：

On branch master

#当前是主干分支

nothing to commit, working tree clean

#文件已经提交过了，并且这个文件既没有新增也没有修改，工作树是干净的，没有东西需要再次提交
```
* 查看日志信息：

```bash
$ git reflog

#出现：

71a3fa7 (HEAD -> master) HEAD@{0}: commit (initial): first commit
```
>指针指向了master分支

* 查看详细日志的命令：

```bash
  $ git log
  #出现：
  commit 71a3fa7df3ed00cf5961fe7b7c59acf3a5f53cae (HEAD -> master)
  Author: Jiao-Yixuan18 <jiao-yixuan18@users.noreply.github.com>
  Date:   Thu Dec 4 16:28:07 2025 +0800

    first commit

```
>不仅能看到版本，还能看到谁提交的这个版本
>71a3fa7df3ed00cf5961fe7b7c59acf3a5f53cae 为完整版本号

##### 3.6 修改文件（test.txt）

###### 3.6.1 查看状态（检测到工作区有文件被修改）

1. 修改文件：
```bash
  $ git log
  #出现：
  commit 71a3fa7df3ed00cf5961fe7b7c59acf3a5f53cae (HEAD -> master)
  Author: Jiao-Yixuan18 <jiao-yixuan18@users.noreply.github.com>
  Date:   Thu Dec 4 16:28:07 2025 +0800

    first commit

```
在vscode编辑器里，在第一行后面添加了2222222222

2. 查看状态：

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
>表明文件被修改了，且修改的文件还没有添加到暂存区

###### 3.6.2 将修改的文件在此添加到暂存区
```bash
$ git add test.txt
```
###### 3.6.3 查看状态（工作区的修改添加到了暂存区）

```bash
$ git status

#出现：

On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt
```
>说明文件添加到了暂存区里

* 再提交本地库：
```bash
$ git commit -m "second commit" test.txt

#出现：

[master ad9571b] second commit
 1 file changed, 1 insertion(+), 1 deletion(-)
```
> 表明一个文件被修改，一行新增，一行删除
>
> 为啥：git是按行来维护文件的，修改了一行它没法表达出来，所以它先把修改之前的那一行删掉，再把修改后的那一行新增进来

* 再次查看状态：

```bash

$ git status
On branch master
nothing to commit, working tree clean
```
* 查看版本信息：

```bash
$ git reflog
ad9571b (HEAD -> master) HEAD@{0}: commit: second commit
71a3fa7 HEAD@{1}: commit (initial): first commit
```
>指针指向第二版本

* 查看第二版本的内容（因为指针指向了第二版本哦）：
```bash
$ cat test.txt
hello git! hello Geek!2222222222
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
```
##### 3.7 历史版本

###### 3.7.1 查看历史版本

* 基本语法

```bash


$ git reflog #查看版本信息

$ git log #查看版本详细信息
```
示例：
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git reflog
ad9571b (HEAD -> master) HEAD@{0}: commit: second commit
71a3fa7 HEAD@{1}: commit (initial): first commit

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git log
commit ad9571b43c971b073002e63d8b2787f4e9caae0a (HEAD -> master)
Author: Jiao-Yixuan18 <jiao-yixuan18@users.noreply.github.com>
Date:   Thu Dec 4 16:51:44 2025 +0800

    second commit

commit 71a3fa7df3ed00cf5961fe7b7c59acf3a5f53cae
Author: Jiao-Yixuan18 <jiao-yixuan18@users.noreply.github.com>
Date:   Thu Dec 4 16:28:07 2025 +0800

    first commit
```
>可以看到提交作者、提交日期和详细版本号
###### 3.7.2 版本穿梭
如果对最新的代码不满意，可以使版本穿越回去

* 基本语法
```bash
  git reset --hard 版本号
```
* 示例：
我想把第二个版本穿越回第一个版本
如何操作：
1. 查看版本信息，复制我想回到的那个版本的版本号：

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git reflog
ad9571b (HEAD -> master) HEAD@{0}: commit: second commit
71a3fa7 HEAD@{1}: commit (initial): first commit
```
2. 版本穿梭

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git reset --hard 71a3fa7
HEAD is now at 71a3fa7 first commit
```
3. 再次查看版本信息：

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git reflog
71a3fa7 (HEAD -> master) HEAD@{0}: reset: moving to 71a3fa7
ad9571b HEAD@{1}: commit: second commit
71a3fa7 (HEAD -> master) HEAD@{2}: commit (initial): first commit
```
>发现指针指向了第一版本

4. 查看当前版本内容：

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ cat test.txt
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
```
>说明文件版本确实发生了变化

* 除此之外还可以去哪里看？
点开git-demo——.git——HEAD
内容为：ref: refs/heads/master
说明指针指向了master这个分支上
* 如何知道在master这个分支上的哪个版本呢？
打开git-demo——.git——refs——heads——master
内容为：71a3fa7df3ed00cf5961fe7b7c59acf3a5f53cae
出现了当前版本号（第一版本的版本号），说明指针指向了master分支，而master分支指向了第一版本

如果再从第一版本穿越到第二版本呢？
1. 查看版本信息，复制第二版本的版本号：

```bash
    lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
    $ git reflog
    71a3fa7 (HEAD -> master) HEAD@{0}: reset: moving to 71a3fa7
    ad9571b HEAD@{1}: commit: second commit
    71a3fa7 (HEAD -> master) HEAD@{2}: commit (initial): first commit
```
2. 版本穿梭：

```bash
    lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
    $ git reset --hard ad9571b
    HEAD is now at ad9571b second commit
```
3. 再次查看版本信息：

```bash
    lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
    $ git reflog
    ad9571b (HEAD -> master) HEAD@{0}: reset: moving to ad9571b
    71a3fa7 HEAD@{1}: reset: moving to 71a3fa7
    ad9571b (HEAD -> master) HEAD@{2}: commit: second commit
    71a3fa7 HEAD@{3}: commit (initial): first commit
```

*Git切换版本，底层其实是移动的HEAD指针*

### 第四章 Git分支操作
##### 4.1 什么是分支 

​       在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支。使用分支意味着程序员可以把自己的工作从开发主线上分离开来，开发自己分支的时候，不会影响主线分支的运行。对于初学者而言，分支可以简单理解为副本，一个分支就是一个单独的副本。（分支底层其实也是指针的引用）

##### 4.2 分支的好处

​       同时并行推进多个功能开发，提高开发效率。
各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。

##### 4.3 分支的操作

|   **命令名称**      | **作用**   |
| :--------   | :-----  | 
| git branch 分支名     | 创建分支 |  
| git branch -v        |   查看分支   | 
| git checkout 分支名        |    切换分支    |
| git merge | 把指定的分支合并到当前分支上|


###### 4.3.1 查看分支
```bash
$ git branch -v

#出现：

*master ad9571b second commit
```
> 表明当前只有一个master分支

###### 4.3.2 创建分支
```bash
$ git branch hot-fix
```
> 创建了一个名为hot-fix的分支
>
> 什么都没出现

再查看分支
```bash
$ git branch -v

#出现：

  hot-fix ad9571b second commit
*master  ad9571b second commit
```
> 发现有了这个分支，此时星号（提示当前所在分支作用）所在位置为master分支的前面

###### 4.3.3 切换分支
```bash
$ git checkout hot-fix

#出现：

Switched to branch 'hot-fix'

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$
```
> 看lenovo这句结尾，发现分支已经切换到hot-fix

再次查看分支
```bash
$ git branch -v

#出现：

*hot-fix ad9571b second commit
  master  ad9571b second commit
```
>发现星号已经到hot-fix分支前面了，证实了已经切换到hoot-fix分支

###### 4.3.4 修改分支

1. 修改文件
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)

$ code test.txt
```
2. 查看状态
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)

$ git status
On branch hot-fix
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
3. 提交到暂存区
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)

$ git add test.txt
```
4. 再次查看状态
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)

$ git status
On branch hot-fix
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt
```
5. 提交到本地库

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git commit -m "hot-fix first commit" test.txt
[hot-fix f027de0] hot-fix first commit
 1 file changed, 2 insertions(+), 2 deletions(-)
```
>表明一个文件被改变，两行删除，两行新增

6. 检查内容是否被修改
```bash
$ cat test.txt
hello git! hello Geek!22222
hello git! hello Geek!33333
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
```
7. 打开本地文件，点开test.txt发现内容已被修改
8. 打开HEAD，发现指针指向hot-fix
9. 打开.git——refs——hot-fix，发现hot-fix存储的就是“hot-fix first commit”这个版本的版本号
10. 查看提交版本
```bash
$ git reflog

#出现：
f027de0 (HEAD -> hot-fix) HEAD@{0}: commit: hot-fix first commit
ad9571b (master) HEAD@{1}: checkout: moving from master to hot-fix
ad9571b (master) HEAD@{2}: reset: moving to ad9571b
71a3fa7 HEAD@{3}: reset: moving to 71a3fa7
ad9571b (master) HEAD@{4}: commit: second commit
71a3fa7 HEAD@{5}: commit (initial): first commit
```
>指针指向hot-fix分支

###### 4.3.5 合并分支

若想把hot-fix分支合并到master分支上，必须切换回master分支，站在master分支上进行合并

1. 切换到master分支
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)

$ git checkout master

#出现：

Switched to branch 'master'
```
2. 查看master分支当前的文件内容
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)

$ cat test.txt

#出现：

hello git! hello Geek!2222222222
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!

```

> 注意：此时当前分支为master分支，hot-fix为要合并的分支

3. 合并分支（把hot-fix合并到master上）

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)

$ git merge hot-fix
//出现：
Updating ad9571b..f027de0
Fast-forward
 test.txt | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
```
>表明合并成功：一个文件被修改，两行新增，两行删除

4. 再次查看master分支上的文件内容

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)

$ cat test.txt
//出现：
hello git! hello Geek!22222
hello git! hello Geek!33333
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
```
>发现此时master分支上test.txt的内容已经修改为了hot-fix里test.txt的内容

###### 4.3.6 产生冲突

冲突产生的原因：
   合并分支的时候，两个分支在同一个文件的同一个位置有两套完全不同的修改。Git无法替我们决定使用哪一个。必须人为决定新代码内容。
1. 修改master分支

```bash
    lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
    $ code test.txt
```
  在倒数第二行后面加master test
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git add test.txt

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git commit -m "master test" test.txt
[master d0a1080] master test
 1 file changed, 1 insertion(+), 1 deletion(-)

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ cat test.txt
hello git! hello Geek!22222
hello git! hello Geek!33333
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!master test
hello git! hello Geek!
```
2. 修改hot-fix分支
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ code test.txt
```
在最后一行加merge
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git add test.txt

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git commit -m "hot-fix test" test.txt
[hot-fix 28fc55e] hot-fix test
 1 file changed, 1 insertion(+), 1 deletion(-)
```
3. 合并分支
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git checkout master
Switched to branch 'master'

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git merge hot-fix
Auto-merging test.txt
CONFLICT (content): Merge conflict in test.txt
Automatic merge failed; fix conflicts and then commit the result.

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master|MERGING)
$
```
>发现报了一个冲突（CONFLICT）日志，在test.txt里产生了代码冲突
>lenovo句后面的小括号也发生了变化，MERGING意思是正在合并中，没有合并成功

4. 查看本地库状态
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master|MERGING)
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
>表明Git已经不敢帮我合并了，需要我手动合并代码

###### 4.3.7 解决冲突

1. 手动解决代码冲突

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master|MERGING)
$ code test.txt
```
*出现：*

![合并冲突](C:\Users\lenovo\Desktop\合并冲突.png)

*手动改为我想要的代码的最终版本：*

![手动解决冲突](C:\Users\lenovo\Desktop\手动解决冲突.png)

> 手动合并完分支，别忘了提交暂存库和本地库

2. 提交暂存区和本地库

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master|MERGING)
$ git add test.txt

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master|MERGING)
$ git commit -m "merge test"
[master b0d4ab8] merge test
```
>注：此时使用git commit 命令时不能带文件名
>因为两个分支都修改了这个文件，如果带文件名，Git不知道是哪个test.txt，会报错
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$
```
> 发现后面MERGING消失，变为正常，说明合并成功

3. 检查一下吧
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ cat test.txt
hello git! hello Geek!22222
hello git! hello Geek!33333
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!master test
hello git! hello Geek!merge
```
4. look look hot-fix分支的情况
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ cat test.txt
hello git! hello Geek!22222
hello git! hello Geek!33333
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!merge
```
>没变化，说明只是将hot-fix合并到master分支

##### 4.4 创建分支和切换分支图解

master、hot-fix 其实都是指向具体版本记录的指针。当前所在的分支，其实是由 HEAD决定的。所以创建分支的本质就是多创建一个指针。
HEAD 如果指向 master，那么我们现在就在 master 分支上。
HEAD 如果执行 hotfix，那么我们现在就在 hotfix 分支上。
所以切换分支的本质就是移动 HEAD 指针。

### 第五章 Git团队协作机制

##### 5.1 团队内协作

![Git团队内协作](C:\Users\lenovo\Desktop\Git团队内协作.png)

##### 5.2 跨团队协作

![Git团对外协作](C:\Users\lenovo\Desktop\Git团对外协作.png)

### 第六章 GitHub操作

|命令名称|作用|
|:-------------|:-----------|
|git remote -v|查看当前所有远程地址别名|
|git remote add 别名 远程地址 |起别名|
|git push 别名 分支 |推送本地分支上的内容到远程仓库|
|git clone 远程地址 |将远程仓库的内容克隆到本地|
|git pull 远程库地址别名 远程分支名|将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并|

##### 6.1 创建远程仓库

在GitHub新建一个仓库为远程库，远程库的名称一般和本地库是一样的

##### 6.2 远程仓库操作

###### 6.2.1 创建远程仓库别名

1. 查看当前所有远程地址别名
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git remote -v
```
2. 创建别名
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git remote add git-demo https://github.com/Jiao-Yixuan18/git-demo.git
```
> 复制远程库的链接
> 别名和库名最好保持一致

3. 再次查看别名
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git remote -v
git-demo        https://github.com/Jiao-Yixuan18/git-demo.git (fetch)
git-demo        https://github.com/Jiao-Yixuan18/git-demo.git (push)
```
###### 6.2.2 推送本地分支到远程仓库

1. 切换回master分支
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (hot-fix)
$ git checkout master
Switched to branch 'master'
```
2. 确认一下内容
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ cat test.txt
hello git! hello Geek!22222
hello git! hello Geek!33333
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!master test
hello git! hello Geek!merge
```
3. 推送到本地库
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git push git-demo master
fatal: unable to access 'https://github.com/Jiao-Yixuan18/git-demo.git/': Recv failure: Connection was reset
```
> 可能失败的原因：GItHub本身在国内访问不稳定，多推送几次
```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git push git-demo master
remote: Permission to Jiao-Yixuan18/git-demo.git denied to Jasmine-163.
fatal: unable to access 'https://github.com/Jiao-Yixuan18/git-demo.git/': The requested URL returned error: 403
```
> 403 Permission denied(权限被拒绝)，核心原因是当前Git用的账号（Jasmmine-163
> ）没有操作权限Jiao-Yixuan18/git-demo.git这个仓库
> 原因：我本地Git保存的登录凭据（用户名、密码、Token）对应的是Jasmine-163这个账号，但这个账号不是仓库Jiao-Yixuan18/git-demo的作者

* 如何把Git使用的账号改为GitHub?
1. 改全局账号（所有仓库都用这个账号）

打开 Git Bash 执行：

```bash
#设置用户名（对应 GitHub 账号名 Jiao-Yixuan18）
git config --global user.name "Jiao-Yixuan18"
#设置对应的 GitHub 注册邮箱
git config --global user.email "你的GitHub注册邮箱@xxx.com"
```
验证修改是否生效

执行下面命令，能看到输出的用户名是  Jiao-Yixuan18  就对了：

```bash  
#查全局配置
git config --global user.name
#查当前仓库配置
git config user.name
```
2. 清理旧凭据，让新账号生效
Windows 系统会缓存 Git 登录凭据，即使改了配置，仍会用旧账号（Jasmine-163）登录，必须清理：

1) 按下  Win + R ，输入  control keymgr.dll  回车，打开「凭据管理器」；
2) 切换到「Windows 凭据」，找到所有和  github.com  相关的条目（比如「git:https://github.com」）；
3) 右键这些条目，选择「删除」；
4) 重新执行  git push git-demo master 




```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git push git-demo master
info: please complete authentication in your browser...
Enumerating objects: 18, done.
Counting objects: 100% (18/18), done.
Delta compression using up to 32 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (18/18), 1.36 KiB | 46.00 KiB/s, done.
Total 18 (delta 7), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (7/7), done.
To https://github.com/Jiao-Yixuan18/git-demo.git

 * [new branch]      master -> master
```
###### 6.2.3 克隆远程仓库到本地

1. 拉取代码

```bash
$ git clone 远程仓库地址

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-balabala (master)
$ git clone https://github.com/Jiao-Yixuan18/git-demo.git
Cloning into 'git-demo'...
remote: Enumerating objects: 18, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 18 (delta 7), reused 18 (delta 7), pack-reused 0 (from 0)
Receiving objects: 100% (18/18), done.
Resolving deltas: 100% (7/7), done.

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-balabala (master)
$ ll
total 0
drwxr-xr-x 1 lenovo 197121 0 Dec  6 17:26 Hello-World/
drwxr-xr-x 1 lenovo 197121 0 Dec  6 17:35 git-demo/


```
>clone代码不需要登录账号
2. 初始化本地仓库
3. 创建别名

进入git-balabala——git-demo这个文件夹里查看别名

```bash
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-balabala/git-demo (master)
$ git remote -v
origin  https://github.com/Jiao-Yixuan18/git-demo.git (fetch)
origin  https://github.com/Jiao-Yixuan18/git-demo.git (push)
```
>自动起的别名为origin
>

* 团队内协作

A把本地库推到（push）远程仓库

B把远程仓库克隆（clone）到自己的本地库

B修改代码

B推送（push）自己的本地库到远程仓库

A拉取（pull）远程仓库

> 实现了A和B的团队内协作
> 
```bash
#B修改代码并提交到本地库
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-balabala/git-demo (master)
$ code test.txt

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-balabala/git-demo (master)

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-balabala/git-demo (master)
$ git commit -m "balabala commit" test.txt
[master b4d2e55] balabala commit
 1 file changed, 2 insertions(+)

#B push 自己的本地库到远程仓库

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-balabala/git-demo (master)
$ git push https://github.com/Jiao-Yixuan18/git-demo.git master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 32 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 288 bytes | 288.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Jiao-Yixuan18/git-demo.git
   b0d4ab8..b4d2e55  master -> master
#这里push时的别名直接复制远程仓库地址就行


#进入A
#A拉取pull远程仓库

lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ git pull git-demo master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 268 bytes | 38.00 KiB/s, done.
From https://github.com/Jiao-Yixuan18/git-demo
 * branch            master     -> FETCH_HEAD
   b0d4ab8..b4d2e55  master     -> git-demo/master
Updating b0d4ab8..b4d2e55
Fast-forward
 test.txt | 2 ++
 1 file changed, 2 insertions(+)

#检查一下吧
lenovo@LAPTOP-FUAMVST6 MINGW64 /d/Git Space/git-demo (master)
$ cat test.txt
hello git! hello Geek!22222
hello git! hello Geek!33333
hello git! hello Geek!
hello git! hello Geek!
hello git! hello Geek!master test
hello git! hello Geek!merge
1111111111111111111111111111
2222222222222222222222222222 by balabala


```

###### 6.2.4 邀请加入团队

###### 6.2.5 拉取远程库内容

##### 6.3 跨团队协作

1. C打开参与项目所在的库（在D的账号里），点左上角fork，叉到自己的账号里来

2. C回到自己的账号，发现自己账号下新增了一个库（从D那里被fork过来的那个库）

3. C点开这个库，发现大标题底下标明了来历（从D那里fork来的）

4. C修改代码：

   1）在git bash里先把这个库克隆，在进行修改，推送

   2）直接在github里面改，提交

   > 此时修改过后的代码还只有修改者能看到，如果想让被修改者看到，需要进行pull request 操作

5. C进行pull request（拉取请求）

C（修改者）在自己fork来的库的页面点击pull request ,再点击New pull request ,再点击Create pull request，可以写一些备注

6. 打开D（被修改者）账号

刷新，发现新增了拉取请求，点开，有评论交流功能

7. D合并申请

审核代码后，没问题，点击Merge pull request (合并申请)，点击Confirm merge(确定合并)

##### 6.4 SSH免密登录


## 参考资料

