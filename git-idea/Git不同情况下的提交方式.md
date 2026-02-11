# Git不同情况下的提交方式

### 情况1：远程仓库已经存在，且已有文件在里面，如何将文件夹/文件推送到这个远程仓库main分支里

1. 本地初始化（若未关联远程）
```bash
#进入本地目标文件夹
cd /你的本地文件夹路径
#初始化Git仓库
git init
#关联已存在的远程仓库（替换为你的仓库地址，HTTPS/SSH均可）
git remote add origin git@github.com:用户名/仓库名.git
```
2. 拉取远程 main 分支历史（解决历史不相关问题）
```bash
git pull origin main --allow-unrelated-histories
```
3. 添加并提交本地文件/文件夹
```bash
#添加文件/文件夹（.代表所有，也可指定路径如Phase\ 1/）
git add .
# 提交暂存内容
git commit -m "提交说明：添加XX文件/文件夹"
```
4. 推送到远程 main 分支
```bash

git push origin main
```

### 情况2：远程仓库不存在，需要新建一个远程仓库，如何将文件夹/文件推送到这个新建远程仓库main分支里

1. GitHub端新建仓库
打开GitHub，点击「New repository」，填写仓库名、是否初始化 README.md ，完成创建。
2. 本地操作
```bash
#进入本地文件夹
cd /你的本地文件夹路径
#初始化Git仓库
git init
#添加并提交本地内容
git add .
git commit -m "首次提交：添加XX内容"
#关联新建的远程仓库（替换为你的仓库地址）
git remote add origin git@github.com:用户名/新建仓库名.git
#推送到远程main分支（-u设置默认推送上游）
git push -u origin main
```

若GitHub新建仓库时初始化了 README.md ，需先执行 git pull origin main --allow-unrelated-histories 再推送。

### 情况3：先fork别人的库，再提交我本地的文件到对方库的某个文件夹里，再提PR

1. Fork他人仓库
打开目标仓库页面，点击右上角「Fork」，将仓库复制到自己的GitHub账号下。
2. 克隆自己的Fork仓库到本地
```bash
git clone git@github.com:你的用户名/被Fork的仓库名.git
cd 被Fork的仓库名
```
3. 添加本地文件到指定文件夹并提交
```bash
#若目标文件夹不存在，先创建（如docs/）
mkdir docs
#将本地文件复制到该文件夹，再暂存
git add docs/你的文件.md
#提交修改
git commit -m "添加XX文件到docs文件夹"
```
4. 推送到自己的Fork仓库 main 分支
```bash
git push origin main
```
5. 在GitHub发起PR
打开自己Fork的仓库页面，点击「Compare & pull request」；
选择目标分支（对方仓库的 main ），填写PR说明，点击「Create pull request」完成提交。