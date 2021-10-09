---
title: Git总结 #文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2020-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: #文章分类目录，可以为空，注意:后面有个空格
tags: [Git] #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
description: git#概要信息
---
![image.png](https://i.loli.net/2021/08/25/49ul86iWdxY7NCg.png)
# 分支 branch

## 查看远程分支

`git remote -v`

## 新建分支

 - 新建不切换

`git branch xxx`

 - 新建并切换分支

`git checkout -b xxx` 

`git switch -c xxx`

类似于两个命令组合

`git branch xxx` 
`git checkout xxx`

更推荐的用法

`git switch -c xxx`(推荐)

[[#switch 与 checkout的区别]]

## 切换分支

`git checkout <branch name>`

`git switch <branch name>`

## 查看本地分支

`git branch`

`git branch -a`

## 查看远程分支

`git branch -r`

## 本地分支与远程关联

`git branch --set-upstream-to=origin/<branch Name> <branch Name>`

错误：[[#fatal branch 'master' does not exist]]

## 拉取远程分支到本地

`git checkout -b localbranch origin/remotebranch`

## 本地分支推送到远程
`git push origin <local branch name>:<remote branch name>`

## 取消与远程分支关联

`git branch --unset-upstream`

取消与远程仓库的关联`git remote remove origin`

## 删除本地分支

`git branch -d <branch name>`

`git branch -d -r` 删除后推送远程

## 删除远程分支

`git push origin --delete <branchName>`

## 切换到commit id 分支

`git checkout commitid`

# 暂存 add

## 添加

`git add .`

不加参数默认为将修改操作的文件和未跟踪新添加的文件添加到git系统的暂存区，注意不包括删除

[[#git add 与 git add 的区别]]

`git add -u`

-u == --update 表示将已跟踪文件中的修改和删除的文件添加到暂存区，不包括新增加的文件，注意这些被删除的文件被加入到暂存区再被提交并推送到服务器的版本库之后这个文件就会从git系统中消失了

`git add -A`

-A == --all

表示将所有的已跟踪的文件的修改与删除和新增的未跟踪的文件都添加到暂存区。

`git add -I` 不常用

## 撤销修改

如果是某个文件回滚到上一次操作： 

`git reset HEAD`  文件名

**撤销add操作**

可以直接使用命令` git reset HEAD`

这个是整体回到上次一次操作

**绿字变红字(撤销add)**

如果是某个文件回滚到上一次操作：` git reset HEAD <file name>`

## 批量添加 （不是add .）

在工作中，使用add . 的情况反而不是最多的，工作区有很多文件不能提交到仓库里，一般情况下需要我们一个一个添加，你的目的是要添加所有的还是需要一种方式添加你需要添加的，如果是前一种 `git add .` 就可以

如果这里还有特殊情况 比如一半需要添加一半不需要 使用 `git add -i` 进入交互式添加

![image-20201217171840684.png](https://i.loli.net/2020/12/30/qAfQ2WjIslnpaOK.png)

![image-20201217171922907.png](https://i.loli.net/2020/12/30/GXfs6C7Si9oTvdh.png)

![image-20201217171948829.png](https://i.loli.net/2020/12/30/Jfi4WSl5VQmt9XY.png)

![image-20201217172008565.png](https://i.loli.net/2020/12/30/KvG8Bc3lr2nhUmZ.png)

# 本地仓库 commit

## 使用amend命令修改commit信息

(注： amend命令只会修改最后一次commit的信息，之前的commit需要使用rebase）

git commit --amend --reset-author

## 当前文件提交到上一次的commit
`git commit --amend` 

## 撤销commit

git reset --soft HEAD~1  //windows的bash

## 查看提交历史记录

_git log_

查看所有的commit提交记录

加上参数 --pretty=oneline，只会显示版本号和提交时的备注信息

_git reflog_

可以查看所有分支的所有操作记录（包括已经被删除的 commit 记录和 reset 的操作）

_git show_

查看提交的详情

-   1.查看最新的commit

_git show_

-   2.查看指定commit hashID的所有修改：

_git show < commitId >_

-   3.查看某次commit中具体某个文件的修改：

_git show < commitId fileName >_

## Commit message 的格式

### 传统方式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。Header 是必需的，Body 和 Footer 可以省略。

（1）type

type用于说明 commit 的类别，只允许使用下面7个标识。

feat：新功能（feature）  
fix：修补bug  
docs：文档（documentation）  
style： 格式（不影响代码运行的变动）  
refactor：重构（即不是新增功能，也不是修改bug的代码变动）  
test：增加测试  
chore：构建过程或辅助工具的变动

（2）scope

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

（3）subject

subject是 commit 目的的简短描述，不超过50个字符。

以动词开头，使用第一人称现在时，比如change，而不是changed或changes  
第一个字母小写  
结尾不加句号（.）

### blingbling emoji

To use gitmojis from your command line install gitmoji-cli. A gitmoji interactive client for using emojis on commit messages.

npm i -g gitmoji-cli

_常用[emoji](https://gitmoji.carloscuesta.me/)_

📝 📝`:memo:`Add or update documentation.
✏️`:pencil2:`Fix typos. 
🐛`:bug:`Fix a bug.
🚀`:rocket:`Deploy stuff. 
✨`:sparkles:`Introduce new features. 
🎉`:tada:`Begin a project. 
💥`:boom:`Introduce breaking changes.
⚡️`:zap:`Improve performance.
🔀`:twisted_rightwards_arrows:`Merge branches.
🏷️`:label:`Add or update types.
参考： [Git 写出好的 commit message](https://ruby-china.org/topics/15737) [Commit message 和 Change log 编写指南](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.htm) [git commit 时使用 Emoji](https://zhuanlan.zhihu.com/p/29764863)

# 推送远程 push

## 推送本地修改到绑定的远程分支

忽略远程分支名
`git push`

## 推送本地修改到指定分支

`git push origin <branch name>`

`git push origin : refs/for/master `

如果远程分支被省略，如上则表示将本地分支推送到与之存在追踪关系的远程分支（通常两者同名），如果该远程分支不存在，则会被新建
如果省略本地分支名，则**表示删除指定的远程分支**，因为这等同于推送一个空的本地分支到远程分支，等同于 `git push origin --delete master`

`git push origin`

如果当前分支与远程分支存在追踪关系，则本地分支和远程分支都可以省略，将当前分支推送到origin主机的对应分支

git push的一般形式为 `git push <远程主机名> <本地分支名> <远程分支名>` ，例如 `git push origin master：refs/for/master` ，即是将本地的master分支推送到远程主机origin上的对应master分支， origin 是远程主机名，第一个master是本地分支名，第二个master是远程分支名。



# 丢弃/撤销 checkout/reset

## 撤销

重置至指定版本的提交，达到撤销提交的目的

git reset –-soft <版本号>

## 丢弃本地所有修改，不包括新增文件

本地所有修改的。没有的提交的，都返回到原来的状态
`git checkout . `

## 回滚

选择要回滚的版本  
`git log` 

回滚到该版本
`git checkout xxx` 

## 滚回来

查看之前操作的commit  
`gitre flog`
回滚到该版本
`git reset --hard xxx`

## git restore

`git restore [--worktree] aaa` # 从staged中恢复aaa到worktree  
`git restore --staged aaa` # 从repo中恢复aaa到staged  
`git restore --staged --worktree aaa `# 从repo中恢复aaa到staged和worktree  
`git restore --source dev aaa` # 从指定commit中恢复aaa到worktree

![542.png](https://i.loli.net/2020/12/30/APhoDGuC1TQw2Oy.png)

## 删除最后一次远程提交

_方式一：使用revert_

`git revert HEAD  `
`git push origin master`

_方式二：使用reset_

`git reset --hard HEAD^ ` 
`git push origin master -f`

_二者区别：_

-   **revert** 是放弃指定提交的修改，但是会生成一次新的提交，需要填写提交注释，以前的历史记录都在；
    
-   **reset** 是指将HEAD指针指到指定提交，历史记录中不会出现放弃的提交记录。

## 删除本地修改

`git checkout .`是本地所有修改的。没有的提交的，都返回到原来的状态。

`git clean -df` 返回到某个节点，（未跟踪文件的删除，即所有新建的未Add的文件，已跟踪的文件不会删）慎用 `git clean` 参数 -n 不实际删除，只是进行演练，展示将要进行的操作，有哪些文件将要被删除。（可先使用该命令参数，然后再决定是否执行） -f 删除文件 -i 显示将要删除的文件 -d 递归删除目录及文件（未跟踪的） -q 仅显示错误，成功删除的文件不显示

注： `git reset` 删除的是已跟踪的文件，将已commit的回退。 `git clean` 删除的是未跟踪的文件

# 拉取 pull

## 拉取默认远程分支到本地
默认拉取远程已绑定的分支到当前分支

`git pull`
与这两句等价  
`git fetch origin master` //从远程主机的master分支拉取最新内容   
`git merge FETCH_HEAD`    //将拉取下来的最新内容合并到当前所在的分支中

取回`origin`主机的分支的最新提交，**并与本地当前分支合并**

## 拉取指定分支

`git pull origin <remotebranshname>`

## 拉取分支与本地分支合并
`git pull origin <remotebranshname>:<localbranshname>`

![clip_image001.jpg](https://i.loli.net/2020/12/30/MrpnYvLAG6jzXiW.jpg)

详情参考[git pull/fetch详解](#%20git%20fetch%20&%20pull%E8%AF%A6%E8%A7%A3)

# 储藏 stash

可以将本地还没有提交的改动全部存储起来 并不提交
`git stash`

恢复
`git stash apply / git stash pop`
这两个命令就可以将刚才暂存起来的内容还原了。但是这里有一个问题，就是 stash apply 和 pop 之间是不同的。 这里涉及到 stash 内部的实现机制，stash 内部其实是通过堆栈实现的。pop 对于堆栈而言很明确，就是弹出的意思。也就是说如果我们使用的是 pop，那么当我们 pop 之后，这条记录会在堆栈当中删除。而如果使用的是 apply 呢，记录不会从堆栈当中删除，仍然会保留下来。 一般情况下我使用 pop 多一些，但是 pop 也有缺点，比如 pop 没有办法选择应用的记录。我们可以使用 git stash list 来查看一下当前堆栈当中已经有的记录。 如果我们使用 git stash pop 的话，默认的是应用的栈顶的记录，也就是 stash@{0}。
但如果我们使用 stash apply 的话，我们可以自由选择我们想要应用的记录。比如如果我们想要应用最后一条记录的话，我们可以这样：`git stash apply stash@{2}`

清空`git stash clear`
删除某个`git stash drop stash@{0}`

# 查看改动 diff

查看当前文件的改动信息

`git diff <filename>`

查看改动文件

`git diff --stat `

查看与另一分支的差别

` git diff <branch> <filename>`

查看与暂存仓库的差别

`git diff --cached <commit> <filename>`

查看与远程仓库的差别

`git diff <commit> <filename>`

`<cmmit>`=`HEAD`时查看工作目录同最近一次 commit 的内容的差异。

两次commit之间的差别

`git diff <commit> <commit>`

以上命令可以不指定 `<filename>`，则对全部文件操作。 以上命令涉及和 Git仓库 对比的，均可指定 commit 的版本。

-   `HEAD` 最近一次 commit
    
-   `HEAD^` 上次提交
    
-   `HEAD~100` 上100次提交
    
-   每次提交产生的哈希值

# 查看历史改动
## 查看某次提交的改动
`git show <commit id>`
要善用git show ，非常好用。
## 查看某一文件的历史改动
`git log <filename>`
查看文件的历次修改记录
`git log -p <filename>`
查看历次修改记录
`git show <commit id> <filename>`
查看某一次提交的历史记录
# 其他
## 公钥
`cd ~/.ssh` 查找有没有`id_rsa..pub`
若存在，则直接用vim打开或者运行指令`cat ~/.ssh/id_rsa.pub`
若不存在，则运行`ssh-keygen -o`生成公钥。

## 查看用户名和邮箱
`git config --list` 查看全部配置
`git config user.name "userName"` 配置当前项目的用户名
`git config user.email "xx@XXX.com"` 配置当前项目的邮箱
`config` 后面加`--global` 为全局配置，不建议这样做。

## git add . 与 git add * 的区别

-   1 git add . 按.gitignore规则全部提交。不会提示.gitignore git add * 与add . 不一样的在于会提示已被忽略的内容。

![image.png](https://i.loli.net/2020/12/31/2qewiGLZths853p.png)

-   2 git add .默认添加. 开头的文件 例如.gitignore git add * 忽略. 开头的文件

## git中出现 > 这个符号怎么退出？

ctrl + d 即可退出。

这个表示没有输入完成，输入没有闭合。比如，只输入了一边的双引号或单引号。

## 修改本项目用户信息：

`git config user.name 'your name'  `
`git config user.email xx@email.com`

## Git中用vim打开、修改、保存文件

一、vim 有两种工作模式：

1.命令模式：接受、执行 vim操作命令的模式，打开文件后的默认模式；

2.编辑模式：对打开的文件内容进行 增、删、改 操作的模式；

3.在编辑模式下按下ESC键，回退到命令模式；在命令模式下按i，进入编辑模式

二、创建、打开文件：

1.输入 touch 文件名 ，可创建文件。

2.使用 vim 加文件路径（或文件名）的模式打开文件，如果文件存在则打开现有文件，如果文件不存在则新建文件。

3.键盘输入字母i进入插入编辑模式。

三、保存文件：

1.在编辑模式下编辑文件

2.按下ESC键，退出编辑模式，切换到命令模式。

3.在命令模式下键入"ZZ"或者":wq"保存修改并且退出 vim。

4.如果只想保存文件，则键入":w"，回车后底行会提示写入操作结果，并保持停留在命令模式。

四、放弃所有文件修改： 1.放弃所有文件修改：按下ESC键进入命令模式，键入":q!"回车后放弃修改并退出vim。

2.放弃所有文件修改，但不退出 vi，即回退到文件打开后最后一次保存操作的状态，继续进行文件操作：按下ESC键进入命令模式，键入":e!"，回车后回到命令模式。

五、查看文件内容：

在git窗口，输入命令：cat 文件名

六、创建文件夹

在git窗口，输入命令：touch 文件夹名

## 使用Git上传项目时需要输入用户名和密码

### 小登陆框

这里简述一下主要步骤：

step1.将上传代码的方式从 https 改成 ssh ![](https://i.loli.net/2020/11/21/f6q1YtxQbuHjTUP.png) 使用命令：`git remote set-url origin git@github.com:LawsonAbs/luogu.git` 后面的用户和项目名需要根据你自己的情况而改变。

step2.在自己本地生成ssh公钥并写在github中指定项目的key中 `ssh-keygen -rsa -C "LawsonAbs"` 生成LawsonAbs这个用户的公钥。

step3.执行命令 `git push -u origin master`

## Git自动push/pull

### windows

bat脚本

@echo off  
e:  
cd C:\Users\Lei Yu\OneDrive - bupt.edu.cn\Document\MarkDownNote  
git config --global credential.helper store  
git pull

将该脚本放到git仓库的根目录中

![image-20201214140659729.png](https://i.loli.net/2020/12/30/I5aPugKB8JsHyN7.png)

![image-20201214140108699.png](https://i.loli.net/2020/12/30/MEGXt1kxI9jyzVH.png)

参考：[https://blog.csdn.net/yougou_sully/article/details/106114253](https://blog.csdn.net/yougou_sully/article/details/106114253)

### Mac

利用[crontab](https://zh.wikipedia.org/wiki/Cron)编写定时脚本，自动同步（可以在macOS和Linux下运行）

crontab -e

输入下列定时任务（每15分钟同步一次）

*/15 * * * * cd /Users/yourname/Markdown;git add .;git commit -m "AutoSave";git push origin master

保存即可，可以用下列命令检验定时脚本是否设置成功。

crontab -l

## [git fetch & pull详解](https://www.cnblogs.com/runnerjack/p/9342362.html)

**1、 简单概括**

先用一张图来理一下git fetch和git pull的概念：

![image-20201216152342411.png](https://i.loli.net/2020/12/30/W5Gpohtq9JMXgSx.png)

可以简单的概括为：

git fetch是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。

而git pull 则是将远程主机的最新内容拉下来后直接合并，即：git pull = git fetch + git merge，这样可能会产生冲突，需要手动解决。

下面我们来详细了解一下git fetch 和git pull 的用法。

**2、分支的概念**

在介绍两种方法之前，我们需要先了解一下分支的概念：

分支是用来标记特定代码的提交，每一个分支通过SHA1sum值来标识，所以对分支的操作是轻量级的，你改变的仅仅是SHA1sum值。

如下图所示，当前有2个分支，A,C,E属于master分支，而A,B，D,F属于dev分支。

A----C----E（master）  
 \  
 B---D---F(dev)

它们的head指针分别指向E和F，对上述做如下操作：

`git checkout master ` //选择or切换到master分支  
` git merge dev`     //将dev分支合并到当前分支(master)中

合并完成后：

A---C---E---G(master)  
 \             \  
 B---D---F（dev）

现在ABCDEG属于master，G是一次合并后的结果，是将E和Ｆ的代码合并后的结果，可能会出现冲突。而ABDF依然属于dev分支。可以继续在dev的分支上进行开发:

A---C---E---G---H(master)  
 \             \  
 B---D---F---I（dev）
 
 **3、git fetch** **用法**

git fetch 命令：

`git fetch <远程主机名> `//这个命令将某个远程主机的更新全部取回本地

如果只想取回特定分支的更新，可以指定分支名：

`git fetch <远程主机名> <分支名>` //注意之间有空格

最常见的命令如取回origin 主机的master 分支：

`git fetch origin master`

取回更新后，会返回一个FETCH_HEAD ，指的是某个branch在服务器上的最新状态，我们可以在本地通过它查看刚取回的更新信息：

`git log -p FETCH_HEAD`

如图：

![clip_image002.png](https://i.loli.net/2020/12/30/u6sKZoTQqXzhP1D.png)

可以看到返回的信息包括更新的文件名，更新的作者和时间，以及更新的代码（19行红色[删除]和绿色[新增]部分）。

我们可以通过这些信息来判断是否产生冲突，以确定是否将更新merge到当前分支。

**4、git pull** **用法**

前面提到，git pull 的过程可以理解为：

`git fetch origin master` //从远程主机的master分支拉取最新内容   
`git merge FETCH_HEAD`   //将拉取下来的最新内容合并到当前所在的分支中

即将远程主机的某个分支的更新取回，并与本地指定的分支合并，完整格式可表示为：

`git pull <远程主机名> <远程分支名>:<本地分支名>`

如果远程分支是与当前分支合并，则冒号后面的部分可以省略：

`git pull origin next`

## git中一些缩写:  

-d  
 --delete：删除  

-D  
 --delete --force的快捷键  

-f  
 --force：强制  

-m  
 --move：移动或重命名  

-M  
 --move --force的快捷键  

-r  
 --remote：远程  

-a  
 --all：所有

## 如何将命令行中的git提示语言改为英文

**mac自带的终端**

`vim ~/.bash_profile`

添加如下内容：

`alias git='LANG=en_GB git'`

更新配置：

`source ~/.bash_profile`

## .gitignore用法
```
# 忽略 .a 文件  
*.a  
# 但否定忽略 lib.a, 尽管已经在前面忽略了 .a 文件  
!lib.a  
# 仅在当前目录下忽略 TODO 文件， 但不包括子目录下的 subdir/TODO  
/TODO  
# 忽略 build/ 文件夹下的所有文件  
build/  
# 忽略 doc/notes.txt, 不包括 doc/server/arch.txt  
doc/*.txt  
# 忽略所有的 .pdf 文件 在 doc/ directory 下的  
doc/**/*.pdf
```

[模板](https://github.com/github/gitignore)

## 其他git命令

1.  修改最近的提交 git commit --amend Copy -amend 参数允许追加修改至最后一次提交之后（比如忘记提交的文件），添加 -no-edit 参数将追加提交至最后一次提交之内并且不改变提交的备注信息。如果没有新的修改提交， -amend 参数将会重写最后一次提交的备注信息。

查看更多：git help commit

2.  交互式选择部分修改 git add -p -p (或 -path) 会允许我们交互式的选择是否提交每一处改动，这样，每次提交就只包含一处修改，即 拆分我们的该次添加修改，每一处修改都有一个提交

查看更多: git help add

3.  交互式的处理储藏中文件的每个部分 git stash -p 跟 git-add 有点类似，你可以使用 --patch 选项交互式地选择每个跟踪文件的要储藏的部分。

通过 git help stash 命令了解更多。

4.  储藏未跟踪的文件 git stash -u 默认情况下，储藏命令是不包括未跟踪的文件的。为了储藏未跟踪的文件你需要使用 -u 参数。 -a (—all) 参数会将未跟踪和忽略的文件一起储藏，通常情况下，这可能不是你需要的。
    
5.  交互式地还原文件的选中部分 git checkout -p --patch 参数还可以用于有选择的丢弃每个跟踪文件的某些部分。我给这个命令起了个别名叫 git discard。

使用 git help checkout 了解更多。

6.  切到上一个分支 git checkout - 该命令可以使你快速切换到之前签出的分支。一般来说 - 是上一个分支的别名。它可以跟别的命令一起使用。我将 checkout 简写成 co ，这样它就变成了 git co - 。
    
7.  还原本地所有修改 git checkout . 在确定可以放弃所有本地修改的情况下可以使用 . 立即去完成。好的习惯是使用 checkout --patch 命令。
    
8.  查看修改 git diff --staged 这个命令会显示已经暂存的文件和上次提交文件之前的差异，git diff 是显示还没有暂存起来的修改；当你使用 git add . 之后再使用 git diff 就会发现什么都没有。

使用 git help diff 了解更多。

9.  重命名本地分支 git branch -m old-name new-name 如果你想重命名当前所在的分支，可以将命令缩短为以下格式:

git branch -m new-name 查看更多: git help branch

10.  重命名远端分支 为了重命名远端分支，你一旦修改本地分支名称，就立即需要删除远端分支，再将重命名后的本地分支推送上去。


git push origin :old-name git push origin new-name

11.  一次性查看所有冲突文件 变基可能会导致冲突，这个命令将打开所有需要你处理的冲突文件。


git diff --name-only --diff-filter=U | uniq | xargs $EDITOR

12.  有哪些改变？ git whatchanged --since="2 weeks ago" 该命令将显示最近两周提交的简单日志，包括每次提交的介绍和修改的文件。下图是译者找的 demo：


13.  从最近一次提交中删除文件 假设你提交了一个错误的文件。你可以通过组合 rm 和 commit --amend 命令从上次提交中快速删除它：


git rm —-cached <file-to-remove> git commit —-amend

14.  查找分支 git branch --contains <commit> 该命令将展示包含指定提交的所有分支。
    
15.  本地储藏优化 git gc --prune=now --aggressive


## switch 与 checkout的区别

<img src="https://i.loli.net/2021/08/25/P92cNFhOet5TpXS.png" alt="image.png" style="zoom: 67%;" />
	
总的来说，switch在分支上与checkout没有什么区别。checkout功能多，除了切换分支还有丢弃更改等功能。git官方推出switch用来专注分支切换功能，防止操作失误。

参考:[git switch branch – Easily checkout git branches with this new command](https://bluecast.tech/blog/git-switch-branch/)
	
## git 默认启动路径
打开git bash时默认是用户文件夹，若想更改则cd到~ 创建.bashrc文件，在文件中输入：
`cd: <c:/your want open path>`  注意要用反斜杠。
参考：https://stackoverflow.com/questions/7671461/how-do-i-change-the-default-location-for-git-bash-on-windows

	
## git bash 添加到Windows Terminal
参考：https://medium.com/@techpreacher/using-git-bash-with-the-microsoft-terminal-bd1f71fa17a1
	
## git 查看某一条语句的修改记录
`git blame <file name>`
# git 报错

## fatal: This operation must be run in a work tree

可能原因： 1.路径不正确 2.git仓库没有正确创建

## fatal: branch 'master' does not exist

若出现错误`fatal: branch 'master' does not exist`原因为本地无分支 新建并checkout 到该分支，再执行此方法，还不行就执行一遍git fetch origin

## warning: LF will be replaced by CRLF in . The file will have its original line endings in y

警告原因：可能是你的项目使用了GitHub的开源项目，这个开源项目上传的环境（Linux）和你本次上传GitHub仓库的环境（Windows）不同 例如：本机上传的环境是win10 ，而在你本机项目中引用的GitHub项目上传环境是Linux

windows中的换行符为 CRLF，而在Linux下的换行符为LF

就会产生如上换行符不同的警告 但是这个错误可以直接忽略，对项目影响不大，我觉着如果以后项目在其他环境上运行的话，还可以通过这个方法改变换行符，是项目在其他环境中正常运行！

## Automatic merge failed; fix conflicts and then commit the result.

自动合并失败；修改冲突然后提交修改后的结果。 
```
<<<<<<<< HEAD

 你写的代码

===============

 别人写的代码

>>>>>>>>>>>>>>> sdhqd128dqwenasjdq
```

## Another git process seems to be running in this repository

windows对于进程的同步互斥管理，是有资源上锁机制的。猜测这里肯定是有进程对某资源进行了加锁，但是由于进程突然崩溃，未来得及解锁，导致其他进程访问不了。 进入工作区目录下的隐藏文件.git，其中的index.lock文件删除掉，然后重新打开git bash进程，问题解决。

## git push错误failed to push some refs to解决方法

**原因**

当我们在git版本库中发现一个问题后，如你在git上对它进行了在线修改，但是没有对本地库进行同步（做到push之前，都先pull下代码，就可以保证本地库和远程库代码一致）。这个时候你再次commit，想把本地库提交到远程git库中，就会出现push失败问题。

> failed to push some refs to

**解决**

方法：1

跟因就是远程库与本地库代码不一致导致的，我们只要把远程库同步到本地库即可，使用如下命令：

> git pull --rebase origin master

指令意思就是把远程库中的跟新合并到本地库中（可能存在冲突需要解决），--rebase的作用是取消本地库中刚刚提交的commit，并把他们接到更新后的版本库中。

方法：2

或者使用如下命令，将commit的代码撤回，然后再git pull也行。

> git reset --soft HEAD^

## refusing to merge unrelated histories

I think you have commit in remote repository and when you pull this error happen.

use this command

git pull origin master --allow-unrelated-histories  
git merge origin origin/master

i suggest reading at [https://stackoverflow.com/questions/39761024/refusing-to-merge-unrelated-histories-failure-while-pulling-to-recovered-repos](https://stackoverflow.com/questions/39761024/refusing-to-merge-unrelated-histories-failure-while-pulling-to-recovered-repos)

This cannot be answered shortly.

**Warning**: You **should not** use the `--allow-unrelated-histories` flag unless you know what unrelated history is and are sure you need it. The check was introduced just to prevent disasters when people merge unrelated projects by mistake.

_As far as I understand_, in your case **has happened the following**:

You have cloned a project at some point `1`, and made some development to point `2`. Meanwhile, project has evolved to some point `3`.

![image.png](https://i.loli.net/2020/12/31/46K8hvcb2szfDei.png)

Then you for some reason lost your local .git subdirectory - which contained all your history from `1` to `2`. You managed to restore the current state though.

![image.png](https://i.loli.net/2020/12/31/lHrdIohY27LnQuR.png)

But now it does not have any history - it looks like the whole project has appeared out of nowhere. If you ask Git to merge them it will not be able to say where your changes are, so it can add them to remote project, as far as I understand it will just report massive add/add conflicts.

**You should** now find back that commit `1` from the remote history where you have cloned the project (I assume you did not pull after that; if you did then you should instead look for the last commit you have pulled). Then you should modify your history so that is starts from that commit 1, and then Git will be able to merge correctly (with pull for example).

So, the steps (assuming you are now in your restored commit without history):

-   estimate where is the commit `1` you have cloned from as some `1?`, based on commit time for example
    
-   run `git diff _1?_..HEAD`, and read carefully. Make sure that the difference contains only edits which you have made. If it contains more then you should have picked a bit wrong `1?` and need to adjust it and repeat this step
    
-   after you have found the commit `1`. You should make it your parent; do `git --reset --soft _1_`, and then `git commit`.

![image.png](https://i.loli.net/2020/12/31/OY9r8AGXcPMBVUe.png)

Now it looks like you have cloned from `1`, then made one commit with all your changes. Your intermediate history is lost anyway with your older `.git` directory, but now you can run your `git pull` - it will merge correctly.

## fatal: Authentication failed for

-   mac上

使用mac下载Azure DevOps项目时，使用git clone xxx 命令后出现需要输入密码，输入后显示报错。原因为mac连接azure项目有bug，官方给出解决方案：

1.终端依次输入

brew tap microsoft/git

brew install --cask git-credential-manager-core

brew upgrade git-credential-manager-core

2.重新输入命令git clone xxx 若跳出登陆窗口输入账户和密码，解决。

参考：[https://github.com/microsoft/Git-Credential-Manager-Core#download-and-install](https://github.com/microsoft/Git-Credential-Manager-Core#download-and-install)

-   一般

可能是设置了token 输入的密码不是账户密码，是token

## error: cannot update the ref 'xxx'

执行git pull时的错误，原因为远程分支与本地冲突？ 解决方法

`git remote prune origin`

然后再git pull即可

参考：[https://stackoverflow.com/questions/10068640/git-error-on-git-pull-unable-to-update-local-ref](https://stackoverflow.com/questions/10068640/git-error-on-git-pull-unable-to-update-local-ref)

## [fatal: unable to access, Received HTTP code 400 from proxy after CONNECT](https://stackoverflow.com/questions/55451735/how-to-solve-fatal-unable-to-access-received-http-code-400-from-proxy-after-co)

Because of some proxy configurations this occurs, to reset all the configurations just run `rm ~/.gitconfig` and start the terminal again.

大坑。。。。每次都劝退

## LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443

run **`networksetup -setv6off Wi-Fi`**

FYI:[https://stackoverflow.com/questions/48987512/ssl-connect-ssl-error-syscall-in-connection-to-github-com443](https://stackoverflow.com/questions/48987512/ssl-connect-ssl-error-syscall-in-connection-to-github-com443)

## git Could not resolve host: socks5

git config http.proxy socks5:192.168.67.1:32767  
git config http.proxy socks5:192.168.67.1(代理ip):32767（代理端口）

然后需要将clashx开启局域网连接！！！！

第二种：

git config -e

删除代理地址

解决以上问题：ClashX的问题，换一个代理工具！！！！！！！

