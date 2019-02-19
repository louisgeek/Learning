# git basic


1. 设置全局信息 git config --global
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
// 保存账号密码
$ git config --global credential.helper store
```
--global 参数代表机器上所有的 Git 仓库都使用这个配置



2.查看当前全局配置

3.创建版本库  git init
```
Administrator@LouisGeek MINGW64 /d/LouisGit
$ mkdir hello_git  //创建目录文件

Administrator@LouisGeek MINGW64 /d/LouisGit
$ cd hello_git      //切换目录文件

Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git
$ pwd
/d/LouisGit/hello_git  //查看目录路径

Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git
$  git init   //初始化当前目录为版本库
Initialized empty Git repository in D:/LouisGit/hello_git/.git/

```

4.添加文件  git add

```
Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git (master)
$ git add hello.txt   // git add . 添加所有文件

```

5.提交文件  git commit

```
$ git commit -m "add hello"
[master (root-commit) 36a3976] add hello
 1 file changed, 2 insertions(+)
 create mode 100644 hello.txt

```

6.查看状态  git status

```
Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   hello.txt

no changes added to commit (use "git add" and/or "git commit -a")

```
7.查看不同  git diff
```
Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git (master)
$ git diff

```

```
git diff HEAD -- hello.txt  //命令查看工作区和版本库最新版本区别
```


8.查看提交的日志记录  git log

```
Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git (master)
$  git log
commit 36a397685948c3067a7c0131b188ae02968d1a91
Author: louisgeek <louisgeek@aliyun.com>
Date:   Fri Feb 10 23:33:11 2017 +0800

    add hello

```

简洁查看日志  git log --pretty=oneline

```
Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git (master)
$  git log --pretty=oneline
36a397685948c3067a7c0131b188ae02968d1a91 add hello

```

9.回退到之前的版本  git reset

在 Git 中，用 HEAD 表示当前版本，也就是最新的提交，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上 100 个版本写 100 个^比较容易数不过来，所以写成 HEAD~100


```
$ git reset --hard HEAD^ //上一个版本

$ git reset --hard 3628164  //制定版本编号的那个版本
```

查看文件内容  cat 

```
Administrator@LouisGeek MINGW64 /d/LouisGit/hello_git (master)
$  cat hello.txt
Git is a distributed version control system.
Git is free software.

```

10.记录你的每一次命令

```
$ git reflog

```
11.撤销修改 


场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令

```
 git checkout --hello.txt
```


场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令


```
git reset HEAD hello.txt
```

就回到了场景 1，第二步按场景 1 操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考【回退到之前的版本】

12.删除文件 rm

```
rm hello.txt
```

13.关联远程库  git remote add

```
git remote add origin git@github.com:xxx/xxx.git

```
14.内容推送到远程  git push
``` 
git push -u origin master  //把分支 master 推送到远
//加上了-u参数，Git 不但会把本地的 master 分支内容推送的远程新的 master 分支，还会把本地的 master 分支和远程的 master 分支关联起来，在以后的推送或者拉取时就可以简化命令。

git push origin master //把本地master分支的最新修改推送

删除关联

git remote rm origin

```

15.克隆远程版本

```
git clone git@github.com:michaelliao/gitskills.git
```

16.创建分支  git checkout -b

```
git checkout -b dev
//-b参数表示创建并切换，相当于以下两条命令：
$ git branch dev
$ git checkout dev

```
17.查看分支信息  git branch

```
git branch
```
18.切换分支  git checkout

```
git checkout master
```
19.合并分支  git merge

```
git merge dev //把dev的分支内容合并到master上

//Fast-forward信息，Git 告诉我们，这次合并是“快进模式”，也就是直接把 master 指向 dev 的当前提交，所以合并速度非常快。


```
20.删除分支  git branch -d
```
git branch -d dev
```

21.查看分支图

```
git log --graph命令可以看到分支合并图
```
22.合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而 fast forward 合并就看不出来曾经做过合并。
```
准备合并 dev 分支，请注意--no-ff参数，表示禁用 Fast forward
```
22.保存工作现场

```
git stash
```
23.查看保存的工作现场

```
git stash list
```

24.恢复工作现场

```
 git stash pop
 
 相当于下面两个命令
 用git stash apply恢复，但是恢复后，stash 内容并不删除，
 需要用git stash drop来删除
 
 可以多次 stash，恢复的时候，先用git stash list查看，然后恢复指定的 stash，用命令：
  git stash apply stash@{0}

```
25.强制删除分支

```
git branch -D feature-vulcan
```
26.查看远程库的信息


```
git remote

git remote -v  //显示更详细的信息
```

27.创建远程分支


```
创建远程 origin 的 dev 分支到本地，于是他用这个命令创建本地 dev 分支：

$ git checkout -b dev origin/dev
```

28.

```
指定本地 dev 分支与远程 origin/dev 分支的链接，根据提示，设置 dev 和 origin/dev 的链接：

$ git branch --set-upstream dev origin/dev
```

29.打标签

```
git tag <name> //就可以打一个新标签

$ git tag v0.9 6224937 //打标签到指定版本

git tag -a v0.1 -m "version 0.1 released" 3628164
// -a指定标签名，-m指定说明文字
```
30.查看标签

```
git tag
```
31.查看标签信息

```
git show v0.9
```
32.删除标签

```
git tag -d v0.1
```
33.远程标签

```
命令git push origin <tagname>可以推送本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d <tagname>可以删除本地标签；

命令git push origin :refs/tags/<tagname>可以删除远程标签
```

34.配置git

```
让 Git 显示颜色，会让命令输出看起来更醒目：

$ git config --global color.ui true
```



附：
35.生成公钥

```
$ ssh-keygen -t rsa -C "louisgeek@qq.com" //创建ssh

```

36.对终端显示的配置，给文字添加颜色，更易于阅读

```
git config --global color.diff auto  
git config --global color.status auto  
git config --global color.branch auto

```
37.乱码设置（其他方案：http://www.cnblogs.com/wangkongming/p/3821305.html）
```
$ git config --global core.quotepath false          # 显示 status 编码
$ git config --global gui.encoding utf-8            # 图形界面编码
$ git config --global i18n.commit.encoding utf-8    # 提交信息编码
$ git config --global i18n.logoutputencoding utf-8  # 输出 log 编码
$ export LESSCHARSET=utf-8  # 最后一条命令是因为 git log 默认使用 less 分页，所以需要 bash 对 less 命令进行 utf-8 编码

```
38.