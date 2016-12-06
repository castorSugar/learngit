# GitHub 入门与实践
根据<a href="https://book.douban.com/subject/26462816/" target="_blank">《GitHub 入门与实践》]</a>进行学习
****
**如要详细了解，可以购买或者查阅该书**

## 第一步--认识Github

*GitHub 是为开发者提供 Git 仓库的托管服务。*
1. 社会化编程。软件开发者们才真正意义上拥有了源代码。世界上任何人都可以比从前
更加容易地获得源代码，将其自由更改并加以公开。
2. 接触广阔世界。放眼世界，注意那些日新月异的源代码、技术、设计以及文化，会
对自己编写的源代码及成果带来巨大影响。
3. 表现程序员的实力
4. 以人为中心

## 第二步--认识git

*Git 属于分散型版本管理系统，是为版本管理而设计的软件。*
*版本管理就是管理更新的历史记录。*

### 两种形式比较
1. 集中式。集中型将所有数据集中存放在服务器当中，有便于管理的优点。但是一旦开发者所处的环境不能连接服务器，就无法获取最新的源代码，开发也就几乎无法进行。
2. 分散式。GitHub 将仓库 Fork 给了每一个用户。 Fork 就是将 GitHub 的某个特定仓库复制到
自己的账户下。 Fork 出的仓库与原仓库是两个不同的仓库，开发者可以随意编辑。

### 安装

*mac预装，window自装，这里讲window的*
1. 到官方站点<a href="https://git-for-windows.github.io/" target="_blank">msysGit</a>或者通过各种软件中心、安全卫士（速度快）下载最新版本。该书以这软件作为操作，命令行为主。如果设置好后，也可以使用<a href="http://www.cygwin.com/" target="_blank">cygwin</a>(window平台类UNIX模拟环境)进行操作。
2. 图形工具，可以使用GitHub官方软件<a href="https://desktop.github.com/" target="_blank">GitHub Desktop</a>或者第三方软件如<a href="https://www.sourcetreeapp.com/" target="_blank">sourcetree</a>（速度快）来进行，不过还需学习命令行方式进行运用。

### 初始化

首先来设置使用 Git 时的姓名和邮箱地址。名字请用英文输入。


    $ git config --global user.name "Firstname Lastname"
    $ git config --global user.email "your_email@example.com"
提高命令输出的可读性。


    $ git config --global color.ui auto

## 第三步--进入GitHub

### 账号设置

在<a href="https://github.com/" target="_blank">GitHub</a>创建账号。然后设置 SSH Key。


    $ ssh-keygen -t rsa -C "your_email@example.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key
    (/Users/your_user_directory/.ssh/id_rsa): /* 按回车键 */
    Enter passphrase (empty for no passphrase): /* 输入密码 */
    Enter same passphrase again: /* 再次输入密码 */
添加公开密钥

*在 GitHub 中添加公开密钥，今后就可以用私有密钥进行认证了。Key 部分请粘贴 id_rsa.pub 文件里的内容。 id_rsa.pub的内容可以用如下方法查看。*


    /* 查看 */
    $ cat ~/.ssh/id_rsa.pub
    ssh-rsa 公开密钥的内容 your_email@example.com
私人密钥与 GitHub 进行认证和通信


    $ ssh -T git@github.com
    The authenticity of host 'github.com (207.97.227.239)' can't be established.
    RSA key fingerprint is /* fingerprint值 */.
    Are you sure you want to continue connecting (yes/no)? /* 输入yes */

### 仓库使用
新建一个Hello-Word仓库，创建按页面流程执行。
clone 已有仓库，进入本地仓库文件夹


    $ git clone  git@github.com:castorSugar/Hello-Word.git
    Cloning into 'Hello-World'...
    remote: Counting objects: 3, done.
    remote: Total 3 (delta 0), reused 0 (delta 0)
    Receiving objects: 100% (3/3), done.
    $ cd Hello-World

在文件夹内新建文件，查看状态
*git status*

    $ git status
    # On branch master
    # Untracked files:
    # (use "git add <file>..." to include in what will be committed)
    #
    # hello_word.php
    nothing added to commit but untracked files present (use "git add" to track)
提交并且备注新建文件到仓库
*通过 git add命令将文件加入暂存区 A，再通过 git commit命令
提交。git log命令查看提交日志。*


    $ git add hello_word.php

    $ git commit -m "add hello word script by php"
    [master 0285491] add hello word script by php
    1 file changed, 3 insertions(+)
    create mode 100644 hello_word.php


    $ git log
    commit 0285491fe2b9e374fa16bcb4e64bb1d106f0b662
    /* 略 */
之后只要执行 push， GitHub 上的仓库就会被更新。


    $ git push
    Counting objects: 3, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 333 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To git@github.com:castorSugar/Hello-Word.git
    bfba36c..0285491  master -> master

## 操作git
### 基本操作
#### git init——初始化仓库
实际建立一个目录并初始化仓库


    $ mkdir git-tutor
    $ cd git-tutor
    $ git init
    Initialized empty Git repository in ./../git-tutor/.git/
#### git status——查看仓库的状态
*当前正处于 master 分支下，所谓提交
（Commit），是指“记录工作树中所有文件的当前状态”。*


    $ git status
    # On branch master
    #
    # Initial commit
    #
    nothing to commit (create/copy files and use "git add" to track)
建立 README.md 文件作为管理对
    象，为第一次提交做前期准备


    $ touch README.md
    $ git status
    # On branch master
    #
    # Initial commit
    ## Untracked files:# (use "git add <file>..." to include in what will
    be committed)#
    # README.md
    nothing added to commit but untracked files present (use "git add" to
    track)
#### git add——向暂存区中添加文件
*暂存区是提交之前的一个临时区域*


    $ git add README.md
    $ git status
    # On branch master
    #
    # Initial commit
    #
    # Changes to be committed:
    # (use "git rm --cached <file>..." to unstage)
    #
    # new file: README.md
    #
#### git commit——保存仓库的历史记录
*-m 参数后的 "First commit"称作提交信息，是对这个提交的
概述*


    $ git commit -m "first commit"
    [master (root-commit) 46a61a7] first commit
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 README.md
*如果想要记述得更加详
细，请不加 -m，直接执行 git commit命令*

在编辑器中记述提交信息的格式如下。
1. 第一行：用一行文字简述提交的更改内容
2. 第二行：空行
3. 第三行以后：记述更改的原因和详细内容

*如果在编辑器启动后想中止提交，请将提交信息留空并直接关闭编
辑器，随后提交就会被中止*
#### git log——查看提交日志


    $ git log
    commit 46a61a7769ebc69237d23ac48a5e6266ec7b9255
    Author: castorSugar
    Date:   Tue Nov 29 19:19:38 2016 +0800

        first commit
*如果只想让程序显示第一行简述信息，可以在 git log命令后加
上 --pretty=short*

    $ git log --pretty=short
*只要在 git log命令后加上目录名，便会只显示该目录下的日志。
如果加的是文件名，就会只显示与该文件相关的日志*


    $ git log README.md
*如果想查看提交所带来的改动，可以加上 -p参数，文件的前后差
别就会显示在提交信息之后*


    $ git log -p
#### git diff——查看更改前后的差别

在刚刚提交的 README.md 中写点东西
*“ +”号标出的是新添加的行，被删除的
行则用“ -”号标出*

    $ git diff
    diff --git a/README.md b/README.md
    index e69de29..ae5cf4d 100644
    --- a/README.md
    +++ b/README.md
    @@ -0,0 +1 @@
    +# Git教程
将 README.md 文件加入暂存区。查看工作树和最新提交的差别


    $ git add README.md
    $ git diff HEAD
    diff --git a/README.md b/README.md
    index e69de29..ae5cf4d 100644
    --- a/README.md
    +++ b/README.md
    @@ -0,0 +1 @@
    +# Git教程
*在执行 git commit命令之前先执行
git diff HEAD命令，查看本次提交与上次提交之间有什么差别，等
确认完毕后再进行提交。这里的 HEAD 是指向当前分支中最新一次提交
的指针。*

提交和查看日志


    $ git commit -m "second commit"
    [master 87a3d53] second commit
     1 file changed, 1 insertion(+)
     $ git log
     commit 87a3d53c97f240d769a419c4cd5fda166233f433
     Author: castorSugar
     Date:   Tue Nov 29 19:36:21 2016 +0800

         second commit
### 分支的操作
#### git branch--显示分支一览表
#### git checkout--转换分支
