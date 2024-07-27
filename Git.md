# Git

## 版本控制系统的分类

- 分布式版本控制系统：联网运行，支持多人协作开发；**性能优秀、用户体验好**
- 集中化的版本控制系统：联网运行，支持多人协作开发；**性能差、用户体验不好**
- 本地版本控制系统单机运行，使维护文件版本的操作工具化

相关命令

```cmd
#查看系统config
git config --system --list　　
#查看当前用户（global）配置
git config --global  --list
# 设置用户名与邮箱（用户标识，必要）
git config --global user.name "kuangshen"  #名称
git config --global user.email 24736743@qq.com   #邮箱
```

## git基础

### git区域以及状态

使用Git 管理的项目，拥有三个区域，分别是工作区、暂存区、Git 仓库。

- Workspace：工作区，就是你平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

Git 中的三种状态

![1722088995762](D:\applicationSoftware\Typora\typora-user-images\1722088995762.png)

- 已修改:表示修改了文件，但还没将修改的结果放到暂存区
- 已暂存:表示对已修改文件的当前版本做了标记，使之包含在下次提交的列表中
- 已提交:表示文件已经安全地保存在本地的Git 仓库中

### git安装配置

- 在Windows 中下载并安装Git
- 配置用户信息

```bash
# 配置用户名以及邮箱
$git config --global user.name "kevin"
$git config --global user.email "xxx@qq.com"
# 查看全局配置
$git config --list --global
# 命令查看文件处于什么状态
git status 
```

如果使用了--global 选项，那么该命令只需要运行一次，即可永久生效。

工作区中的每一个文件可能有4 种状态，这四种状态共分为两大类

![1722089528961](D:\applicationSoftware\Typora\typora-user-images\1722089528961.png)

### git基本操作

- 跟踪新文件

使用命令git add开始跟踪一个文件。

```bash
# 跟踪当前路径下的所有文件
git add . 
# 跟踪某一特定文件
git add xx.file
```

- 提交更新

执行git commit 命令进行提交暂存区的文件,其中-m 选项后面是本次的提交消息，用来对提交的内容做进一步的描述：

```bash
$ git commit -m "修改了一些文件git,node,springboot等"
```

- 撤销对文件的修改

把对工作区中对应文件的修改，还原成Git 仓库中所保存的版本。操作的结果：所有的修改会丢失，且无法恢复！**危险性比较高，请慎重操作**

```bash
$git checkout --  xx.file
```

-  取消暂存的文件

```bash
git reset HEAD xx.file
```

- 跳过使用暂存区域

为了方便工作的进行，可以跳过暂存区，直接将工作区的代码提交到git仓库，命令如下

```bash
$ git commit -a -m "修改了一些文件git,node,springboot等"
```

-  移除文件

从Git 仓库中移除文件的方式有两种：

1. 从Git 仓库和工作区中同时移除对应的文件
2. 只从Git 仓库中移除指定的文件，但保留工作区中对应的文件

```bash
# 从Git 仓库和工作区中同时移除
git rm -f  xx.file
# 只从Git 仓库中移除指定的文件，但保留工作区中对应的文件
git rm -rf  --cached xx.file
```

- 忽略文件

有些文件我们不想纳入到git的管理之中，这时，我们可以创建一个名为.gitignore的配置文件，列出要忽略的文件的匹配模式。

文件.gitignore 的格式规范如下：

1. 以# 开头的是注释
2. 以/结尾的是目录
3. 以/开头防止递归
4. 以!开头表示取反
5. 可以使用glob 模式进行文件和文件夹的匹配（glob 指简化了的正则表达式）

```bash
# 忽略 index.css 这个文件
index.css

# 忽略 test 目录下所有的文件
test/
# 只忽略当前路径下的TODO文件，不忽略subdir/TOD
/TODO
# 忽略doc/notes.txt但不忽略doc/server/arch.txt
doc/*.txt

```

- 查看提交历史

```bash
git log 
# 查看提交的近两条历史
git log -2 
```

- 回退到指定的版本

```bash
# 在上一行上展示所有的提交历史
git log --pretty=oneline
# 使用 git reset --hard 命令，根据指定的提交的ID 回退到指定版本
git reset --hard <CommitID>
# 在旧版本中使用 git reflog --pretty=oneline 命令，查看命令操作的历史
git reflog --pretty=oneline
# 再次根据最新的提交 ID，跳转到最新的版本
git reset --hard <CommitID>
```

## Github

 Github 是全球最大的开源项目托管平台。因为只支持Git 作为唯一的版本控制工具，故名GitHub。

1、新建远程仓库

### 远程仓库的两种访问方式

Github 上的远程仓库，有两种访问方式，分别是HTTPS和SSH。它们的区别是：
① HTTPS：零配置；但是每次访问仓库时，需要重复输入Github 的账号和密码才能访问成功
② SSH：需要进行额外的配置；但是配置成功后，每次访问仓库时，不需重复输入Github 的账号和密码
注意：在实际开发中，推荐使用SSH 的方式访问远程仓库。

```bash
# 将本地仓库与远程仓库相连，并把远程仓库命名为orign
git remote  add orign git地址 
# 将本地仓库推送到远程orign仓库中
git push -u orign -master
```

### SSH key

 SSH key 的作用：实现本地仓库和Github 之间免登录的加密数据传输。
SSH key 的好处：免登录身份认证、数据加密传输。
SSH key 由两部分组成，分别是：
① id_rsa（私钥文件，存放于客户端的电脑中即可）
② id_rsa.pub（公钥文件，需要配置到Github 中）

生成SSH key

```bash
# 在C:\Users\用户名文件夹\.ssh目录中生成id_rsa和id_rsa.pub 两个文件
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# 在浏览器中登录Github，点击头像-> Settings-> SSH and GPG Keys -> New SSH key，将
# id_rsa.pub里面的内容复制到粘贴到Key 对应的文本框中
 ssh -T git@github.com # 检测Github 的SSH key 是否配置成功
```

## git分支

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努
力学习SVN。如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了Git又学会了SVN！

### master 主分支

在初始化本地Git 仓库的时候，Git 默认已经帮我们创建了一个名字叫做master的分支。通常我们把这个
master 分支叫做主分支

在实际工作中，master 主分支的作用是：用来保存和记录整个项目已完成的功能代码。
因此，不允许程序员直接在master 分支上修改代码，因为这样做的风险太高，容易导致整个项目崩溃。

### 功能分支

功能分支指的是专门用来开发新功能的分支，它是临时从master 主分支上分叉出来的，当新功能开发且测试
完毕后，最终需要合并到master 主分支上

![1722094266538](D:\applicationSoftware\Typora\typora-user-images\1722094266538.png)

- 查看分支列表

```bash
git branch
```

分支名字前面的*号表示当前所处的分支

![1722094351987](D:\applicationSoftware\Typora\typora-user-images\1722094351987.png)

- 创建新分支

可以基于当前分支，创建一个新的分支，此时，新分支中的代码和当前分支完全一样：

```bash
git branch 分支名称
```

- 切换分支

```bash
git checkout 分支名称
```

- 分支的快速创建和切换

可以创建指定名称的新分支，并立即切换到新分支上：

```bash
git checkout  -b 分支名称
```

- 合并分支

功能分支的代码开发测试完毕之后，可以使用如下的命令，将完成后的代码合并到master 主分支上：

```
git checkout master
# 将其他分支上的代码合并到master上
git merge other
```

- 删除分支

当把功能分支的代码合并到master 主分支上以后，就可以使用如下的命令，删除对应的功能分支：

```
git branch  -d 分支名称
```

- 遇到冲突时的分支合并

```bash
# 假设:在把 reg 分支合并到 master分支期间，代码发生了冲突
git checkout master
git merge reg
#打开包含冲突的文件,手动解决冲突之后，再执行如下的命令
git add .
git commit -m "解决了分支合并冲突的问题"
```

- 将本地分支推送到远程仓库

```bash
# -u 表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数#
git push -u 远程仓库的别名 本地分支名称:远程分支名称
# 示例
git push -u origin payment:pay
如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化
git push -u origin payment
```

-  查看远程仓库中所有的分支列表

```bash
git remote  show  远程仓库名称
```

- 跟踪分支

跟踪分支指的是：从远程仓库中，把远程分支下载到本地仓库中。需要运行的命令如下：

```bash
# 从远程仓库中，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
git checkout 远程分支的名称
# 示例:
git checkout pay
#从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
git checkout -b 本地分支名称 远程仓库名称/远程分支名称
# 示例:
git checkout -b payment origin/pay
```

- 
  拉取远程分支的最新的代码

```
git pull
```

- 删除远程分支

```bash
# 删除远程仓库中，指定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称
# 示例:
git push origin --delete  pay
```

