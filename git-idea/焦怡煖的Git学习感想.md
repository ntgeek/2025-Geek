# Git学习笔记

> —焦怡煖

## 学习背景

初步掌握了markdown语法，学习了GitHub

## 学习内容的目录

学会使用 Git 推送项目

Git命令

学习如何与他人在Github 上协作完成项目

## 学习内容

#### 学会使用 Git 推送项目
* 1.注册GitHub账号（阶段一已完成）
* 2.安装配置好Git
[安装配置教程](https://liaoxuefeng.com/books/git/install-git/index.html)
* 3.创建远程仓库
在GitHub上创建远程仓库
* 4.创建本地仓库
[创建版本库](https://liaoxuefeng.com/books/git/create-repo/index.html)
* 5.初始化本地仓库
打开文件管理器，进入创建的本地仓库对应的文件夹的目录，然后在空白处右击鼠标右键，选择 Git Bash Here
（1）配置用户信息，输入以下两条命令
  git config user.name "your name" --global
  git config user.email "your email" --global
（2）初始化仓库
   确定自己已经在命令行进入该项目目录，输入初始化命令，初始化该目录为一个 Git 仓库
   git init
（3）添加远程仓库
打开之前在 Github 上创建的仓库，单击 SSH按钮，然后点击 ssh 链接右方的复制图标复制该链接；切换回命令行，使用 git remote add 添加该链接
git remote add  "链接地址"
* 6.使用SSH密钥
（1）生成密钥对
在Git Bash的命令行，输入生成 SSH 密钥对的命令
ssh-keygen -C "comment"
（2）获取生成的公钥
接下来打开系统的文件管理器，进入用户家目录的 .ssh 文件夹，找到刚才建立的 id_rsa.pub 文件，以文本方式打开，复制其中的内容
（3）将公钥配置到 Github
在 Github 网站右上角找到个人头像的位置，点击头像，在弹出的菜单中点击 Settings，在左边的菜单中点击 SSH and GPG Keys，点击 New SSH Keys，将复制的公钥内容粘贴到 Key 输入框，并给该 SSH Key 定义一个 Title；然后点击下方的 Add SSH key 添加该 Key
* 7.提交推送
（1）添加文件
切回命令行，使用 git add 命令添加文件进入 git 管理
（2）查看状态
git status
（3）提交文件更改
git commit -m "input yours message"
（4）推送
使用 push 命令 将本地仓库推送到远程仓库（Github）中
git push -u origin master
可能会出现提示是否继续连接的输入项，输入 yes 即可


### Git命令
[Git命令](https://blog.csdn.net/u011709538/article/details/132618844?ops_request_misc=%257B%2522request%255Fid%2522%253A%25224c1c6fb175393b1458408a10f0dc6a50%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=4c1c6fb175393b1458408a10f0dc6a50&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-132618844-null-null.142^v102^pc_search_result_base5&utm_term=git%E5%91%BD%E4%BB%A4&spm=1018.2226.3001.4187)

#### 学习如何与他人在Github 上协作完成项目

* **感想**

  ​     阶段一学GitHub的时候，感觉GitHub是很好的提交工具，页面也简洁条理，遇到的问题基本也能自己解决。初学Git，感觉就不如GitHub那么友好了，各种命令，专有名词，让我有点不知所措，遇到不懂得词，AI、浏览器来回切换搜索这到底是啥意思。

  ​     直到学到廖雪峰的教程中，Git是什么，Git的诞生，集中式vs分布式，我感觉自己隐隐约约猜到了为什么学习Git会成为考核中的任务之一，它作为前世界上最先进的分布式版本控制系统，在往后的学习和实践中必然是非常好用高效的工具，团队中的成员可以很方便的修改项目。现在的考核也是为今后的学习和实践打下基础。一想到这，我突然就意识到攻克这一部分的难关也只是刚刚开始，但也是我成长的必经之路，因此对学习Git这件就有了更大的动力和兴趣。

  ​     在学习Git的过程中我遇到了很多问题，比如SSH连接GitHub被拒，接连两个晚上都被类似的问题困扰。在求助mentor的过程中，我也学到了一些知识，比如DNS污染是某种结果。

  ​     学习Git的过程确实比我想象的难，但“那些杀不死我的，终将使我更强大”。



## 参考资料

1. [Git安装及使用](https://blog.csdn.net/qq_39809160/article/details/145712755?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522250f5a39f47509b74693bfd3f1d02d6e%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=250f5a39f47509b74693bfd3f1d02d6e&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~hot_rank-4-145712755-null-null.142^v102^pc_search_result_base5&utm_term=%E4%BF%9D%E5%A7%86%E7%BA%A7Git%E5%AD%A6%E4%B9%A0%E6%95%99%E7%A8%8B&spm=1018.2226.3001.4187)

2. [廖雪峰的Git教程](https://liaoxuefeng.com/books/git/introduction/index.html)

