git is a version control system.
git is a good software.

命令行教程：
http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/

git command line:
1.设置全局用户名和邮箱
git config --global user.name ""
git config --global user.email ""

2.初始化git仓库
git init

3.添加上传文件
git add readme.txt

4.提交仓库
git commit -m ""
参数:
    -m 表示提交注释性文字

5.查看当前仓库状态
git status

6.解决编码问题?
git config --global core.autocrlf true

7.查看提交日志
git log
git log --pretty=oneline

8.回退到上一个版本
git reset --hard HEAD^
注意：
HEAD指向的版本就是当前版本.
上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100.
如果知道commit_id(一个长的字符串)可以直接回退到某个版本
git reset --hard aee4fc7
这个配合 git reflog查看执行过的命令

9.查看执行过的命令
git reflog

10.查看工作区和版本库里面最新版本的区别
git diff HEAD -- readme.txt

11.放弃工作区的修改，回退到最近一次commit或者add的状态
git checkout -- readme.txt

12.把暂存区的修改撤销掉（unstage），重新放回工作区
git reset HEAD readme.txt

13.又到了小结时间。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- readme.txt
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

14.删除文件
rm temp.txt
git rm temp.txt
git commit -m "delete file"

15.恢复误删除的文件
git checkout -- temp.txt

16.
在继续阅读后续内容前，请自行注册GitHub账号。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），
创建SSH Key：
$ ssh-keygen -t rsa -C "youremail@example.com"
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
在 git bash 里面切换到.ssh目录，查看pub中的密钥 cat id_rsa.put


17.添加已有的本地仓库到github:
git remote add origin git@github.com:dev-eric-cf/git-study.git
推送
git push -u origin master
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。


18.查看分支
git branch 
当前分支前面会标一个*号

19.创建分支
git branch branchname

20.切换分支
git checkout  branchname
(19和20命令合并可以使用 git checkout -b branchname)创建并切换到branchname分支

21.合并分支,切换当前分支为主线(master)
git merge branchname

22.删除分支
git branch -d branchname

23.查看分支合并图
git log --graph


24.克隆远程仓库(分支)
git clone git_url
git checkout -b dev origin/dev

25.推送分支
git push origin/dev

26.
你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送
推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：
git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接
git branch --set-upstream dev origin/dev
再pull
这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：


因此，多人协作的工作模式通常是这样：

首先，可以试图用git push origin branch-name推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。


=======
小结

查看远程库信息，使用git remote -v；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。