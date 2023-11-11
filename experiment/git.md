# Git使用

Author: [@Reed Qiuu](https://github.com/Iri-sated) [@Eureka](https://github.com/Eureka-Maggie)

### Why Git?
Git是一个版本控制系统，用于跟踪和管理项目代码的变化。它允许多个开发人员协同工作，并提供了对代码进行版本控制、分支管理和合并等功能的支持。
> 参考阅读：  
> https://zhuanlan.zhihu.com/p/653977584  
> https://www.bilibili.com/video/BV1MU4y1Y7h5/

---
### Git安装
#### Windows
参考[该文章](https://zhuanlan.zhihu.com/p/443527549?utm_id=0&wd=&eqid=e5c20f5500016f85000000036497e96c)进行安装即可。
安装完成后，使用时双击Git Bash的图标，打开一个类似命令行的界面。像在Linux命令行中一样正常使用即可。

---
#### MacOS
MacOS通常自带，通过以下命令验证
``` bash
git --version
> git version 2.39.3 (Apple Git-145)
```

---
### 基本配置
配置用户名和邮箱，local对当前仓库有效，global对该账户所有仓库有效，system对对系统所有用户有效
``` bash
git config --global user.name "YOUR_USER_NAME"
git config --global user.email "YOUR_EMAIL"
```
配置完成的验证
``` bash
git config --list --global
> user.name=YOUR_USER_NAME
> user.email=YOUR_EMAIL
```
*可选：Git中的编辑器配置*
*先检查当前编辑器是什么*
``` bash
git config --global core.editor
```
*若输出不是想要的编辑器，在上述命令之后加上指定编辑器路径即可*

---
### 工作流程
![](1.png)
右侧三个仓库位于本地，从左到右依次为Git仓库、暂存区（Index）和工作区；左侧为远程仓库。接下来先考虑本地仓库，有如下常用命令：
``` bash
git init # 初始化一个git目录，除“.git”文件夹以外所有内容，都已/将处在工作目录下

git status # 查询当前状态
# 对于已有的文件进行了修改但还没有保存，那么这个文件的状态叫做“未暂存 / unstaged”
# 对于新创建的文件的状态，我们称其为“未跟踪 / untracked”

git add FILENAME # 将工作目录下的文件提交到暂存区
# 当FILENAME用符号.代替时，表示把当前目录下所有的文件都提交到暂存区

git commit -m "COMMIT" # 将暂存区文件提交到仓库，COMMIT为注释内容
# 此处即使不填写注释，也会跳转到指定的编辑器，在其中填写完注释后才算commit成功

git log # 查看commit的历史记录（注意：不会打印reset以后的部分）
git log --pretty=oneline --abbrev-commit --all --graph # 加上一些方便阅读的参数
git reflog # 同时打印commit和reset两个操作的历史记录

git reset --hard commitID # 回退/前进到特定版本（commitID通过log/reflog查看）
```
**忽略列表**：可以创建一个名为名为“.gitignore”的文件，来指定一部分文件不让Git托管。
> GitHub上有项目收集了在各种编程语言、框架、工具、环境下所对应的gitignore文件的template：
> https://github.com/github/gitignore

---
### 分支
分支可以把代码从主线中分离出去，让每个人有一个独立的线，从而修改 bug 或者开发新功能，互不影响也不影响主线，在开发完以后，再把代码汇聚到主线上。
``` bash
git branch # 查看所有分支
git branch [-d/-D] BRANCH_NAME # 创建指定名字的分支
# -d检查后删除   -D强制删除
git checkout [-b] BRANCH_NAME # 切换到指定名字的分支（加上参数-b可以创建并切换）
```
如下命令会将指定名字的分支合并到当前分支上，通常会将别的分支合并到master分支上。
``` bash
git merge BRANCH_NAME
```
多个分支中以不同方式修改了同一行代码时，会在merge时出错。此时进入MERGING状态，需手动处理冲突并commit处理的结果。（打开merging出错的文件，里面会有标记）

---
### SSH连接GitHub
#### 生成SSH密钥
> 参考自官方配置说明https://docs.github.com/en/authentication/connecting-to-github-with-ssh

先在本地生成SSH keys，可以选用ed25519，网上也有很多教程用的rsa
``` bash
ssh-keygen -t ed25519 -C "YOUR_EMAIL"
> Generating public/private ed25519 key pair.
> Enter file in which to save the key (/Users/USERNAME/.ssh/id_ed25519): 
> Enter passphrase (empty for no passphrase): 
> Enter same passphrase again: 
```
不想设置存储文件和密码，连续三次回车即可。随后得到终端返回如下四个信息（具体信息已略去）
``` bash
> Your identification has been saved in [xxx]
> Your public key has been saved in [xxx]
> The key fingerprint is: [xxx]
> The key's randomart image is: [xxx]
```
随后在后台运行ssh代理
``` bash
eval "$(ssh-agent -s)"
> Agent pid 8158
```
#### 配置config文件
配置config文件（官方说明中仅要求macOS Sierra 10.12.2之后版本的用户执行这一步）
``` bash
open ~/.ssh/config
> The file /Users/USERNAME/.ssh/config does not exist.
```
若返回文件不存在报错，用touch命令创建文件后再打开
``` bash
touch ~/.ssh/config
```
在文件中写入如下内容（如果之前没有设置passphrase，不用输入UseKeychain那一行）
``` bash
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```
#### 添加私钥
向SSH代理添加SSH私钥（如果之前没有设置passphrase，不用输入--apple-use-keychain）
``` bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```
#### 在GitHub上添加SSH Key
先用cat命令查看公钥并复制
``` bash
cat ~/.ssh/id_ed25519.pub
```
在GitHub点击用户头像 --> Settings --> SSH and GPG keys中添加一个新的SSH key，在key中完整黏贴之前复制的公钥内容，确认即可。随后就能看到自己SSH keys下有了一个新的key，邮箱与GitHub邮箱相对应。
#### 配置完成的测试
在终端执行
``` bash
ssh -T git@github.com
```
会看到一个类似如下的警告（例子来源于官方说明）
``` bash
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
> Are you sure you want to continue connecting (yes/no)?
```
确认fingerprint与自己GitHub设置中所配置的key一致后选择yes，得到如下反馈。
``` bash
> Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```
若USERNAME与自己的一致，即代表配置成功。

---
### 远程仓库的使用（GitHub）
#### 配置
先在GitHub对应仓库上找到SSH地址，复制
![](2.png)
在本地执行如下命令，其中REMOTE_NAME代表了给这个远程仓库起的名字，REMOTE_URL处填写之前复制的SSH地址
``` bash
git remote add REMOTE_NAME REMOTE_URL
```
可以检查是否添加完成
``` bash
git remote
> REMOTE_NAME1
> REMOTE_NAME2
> ...
```
#### push操作
通过下面命令，把本地仓库 Push 到远程仓库
``` bash
git push [-f] [--set-upstream] [REMOTE_NAME [LOCAL_BRANCH][:REMOTE_BRANCH] ]
```
+ [-f] 表示强制推送，可能覆盖其他人的工作
+ [--set-upstream] 设置本地分支对应远程仓库的哪一个分支（通常只需指定一次），可以使用以下代码查看绑定关系
  ``` bash
  git branch -vv 
  ```
+ REMOTE_NAME 远程仓库名称
+ [LOCAL_BRANCH] 本地分支
+ [:REMOTE_BRANCH] 远程分支（不要漏冒号）

执行`git push`命令之前，最好使用`git pull origin master`命令从远程仓库获取最新的更改。这样可以避免可能的冲突。

#### clone操作
把某个项目对应的远程仓库 clone 到本地
``` bash
git clone REMOTE_URL [NAME]
```
不设置NAME，则默认使用远程仓库的名字。

#### fetch操作
在一开始用 clone 从头下载一个远程仓库后，可以使用 fetch 不断把发生变动的部分在本地进行更新
``` bash
git fetch [REMOTE_NAME] [BRANCH_NAME]
```
不指定BRANCH_NAME时抓取所有分支下的更新。需要注意，fetch 指令会将仓库里的更新抓取到本地，但不会将其 merge 到本地仓库中。如果想要更新到本地仓库上，还需要在需要本地需要更新的分支上执行一次 merge 命令
``` bash
git merge [REMOTE_NAME]/[BRANCH_NAME]
```

#### pull操作
相当于结合了 fetch 和 merge
``` bash
git pull [REMOTE_NAME] [BRANCH_NAME]
```
如果不指定远端名称和分支名，则抓取所有并更新当前分支。

#### 省流版：复现他人实验常用的一套流程
```bash
1. git clone +github网址  # 想要复现的实验的repo的github地址
2. clone好后服务器里ls一下，会看到这个文件夹 # 非必要，只是方便下一步进入文件夹
3. cd到这个文件夹中，rm -rf .git  # 把别人的git信息删了，不然你再上传也是传到别人那里，且没权限
4. git init
5. 在github上手动创建一个repository，拿到网址
6. git remote add origin +网址
7. git pull origin branch名 # 通常是master
8. git add .  # 把所有新pull下来的文件全都加入到暂存区
9. git commit -m "写点注释"
10. git push origin branch名 # 通常是master
```
#### 如果push的文件里有大于100M的，需要用lfs
```bash
git init
git remote add origin + 网址
git lfs install
find ./ -size +100M # 找到需要用lfs的文件有什么，假设观察输出都是.bin结尾
git lfs track "*.bin"
git add .gitattributes
git add .
git commit -m "注释"
git config --global https.postBuffer 24288000
git push origin master
```