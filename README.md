# git-dos
git config --global user.name "wggglggg"                 # 创建用户名,可以谁操作的
git config --global user.email "wggglggg@xxxxxxx.com"    # 创建用户邮箱 ,  可以在c:\users\xxxxx\.gitconfig 查看

# 创建仓库
# 先在电脑上创建一个文件夹,假设我建一个gittest文件夹作为仓库, 这个文件夹作为本地仓库,再进入此仓库
d:\> md gittest
d:\> cd gittest

# 在gittest文件夹中初始化
D:\gittest>git init
Initialized empty Git repository in D:/gittest/.git/

# 在gittest文件夹中创建一个任意的文件, 假设创建一个 README.md文件, windows用 copy cn xxxxxx.xxx(文件名),
# 假设创建一个文件, 名称叫  README.md, 文件中的内容是I am in the file--README.md, 按ctrl+c保存退出
D:\gittest>copy con README.md
I am in the file--README.md
已复制         1 个文件。

# 创建完文件后, status状态是红色的,因为没有add进缓存区
D:\gittest>git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)

# 用git add xxxxxx.xxx(你想add的文件名)后,再次用git status查看状态, xxxxxx.xxx文件变绿色了,分支默认是master
D:\gittest>git add README.md

D:\gittest>git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md

# 提示也显示,如果不想添加到缓存区, 可以用 git rm --cached xxxxx.xxx(文件名)来取消git追踪,git就不再监控xxxx.xx文件是否有更改了
D:\gittest>git rm --cached README.md
rm 'README.md'
# 再次git status查看状态, xxxxx.xx又变成了红色,表示未被 添加进缓存区
D:\gittest>git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)

# 一次性将文件夹所有文件都加入到缓存区中让git 监控可以使用git add -A
D:\gittest>git add -A

# 将文件一次性提交到 本地仓库中,可以用git commit -m 'xxxxxxx', -m 后面为提交说明, 方便以后追踪提交的是什么
D:\gittest>git commit -m 'test'
[master (root-commit) bb4e407] 'test'
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
------------------------------------------以上是本地操作-------------------------------------------------

# 如果要将代码传到github上保存, 要先在github上创建一个仓库, 最好为同名gittest
# 在Github右上角点击'+', 选择New Repository(创建新仓库), 名称设置为gittest
# 如果本地仓库为空的,没有任何文件可以使用"…or create a new repository on the command line"给出的代码
D:\gittest>echo "# gittest" >> README.md
D:\gittest>git init
D:\gittest>git add README.md
D:\gittest>git commit -m "first commit"
D:\gittest>git remote add origin https://github.com/wggglggg/gittest.git
D:\gittest>git push -u origin master

# 如果本地仓库是有文件的可以使用"…or push an existing repository from the command line"提供的代码
D:\gittest>git remote add origin https://github.com/wggglggg/gittest.git
D:\gittest>git push -u origin master

# 上面的内容简单来说是先要让本地与github端创建联系.
D:\gittest>git remote add origin https://github.com/wggglggg/gittest.git
# 多人项目也可以使用 git remote -v查看是否与github端创建联系
D:\gittest>git remote -v
origin  https://github.com/wggglggg/gittest. (fetch)
origin  https://github.com/wggglggg/gittest. (push)

# 创建好联系, 就可以使用git push,将本地文件推送给远端了(保存存到远端github上), -u以后下次再Push就不用写origin master
D:\gittest>git push -u origin master

# 如果在远端修改了代码, 也想让本地也更新,可以使用git pull, git会把远端的代码修改的内容更新到本地仓库
D:\githubtest>git pull
warning: Pulling without specifying how to reconcile divergent branches is
discouraged. You can squelch this message by running one of the following
commands sometime before your next pull:

  git config pull.rebase false  # merge (the default strategy)
  git config pull.rebase true   # rebase
  git config pull.ff only       # fast-forward only

You can replace "git config" with "git config --global" to set a default
preference for all repositories. You can also pass --rebase, --no-rebase,
or --ff-only on the command line to override the configured default per
invocation.

remote: Enumerating objects: 8, done.
remote: Counting objects: 100% (8/8), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), 1.24 KiB | 6.00 KiB/s, done.
From https://github.com/wggglggg/githubtest
   96c91f4..63ec8f1  master     -> origin/master
Updating 96c91f4..63ec8f1
Fast-forward
 README.md | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)

---------------------------------------以上是branch基本分支 创建 推送 删除----------------------------------
# 使用git xxxx分支名  创建一个新分支
D:\githubtest>git branch feature1

#使用git branch查看有哪些分支，发现有master和 feature1两个分支, ＊号是显示当前分支
D:\githubtest>git branch
error: cannot spawn less: No such file or directory
  feature1
* master

# 切换分支 git checkout xxxxxx分支名, 再查看分支, 当前分支已经换成了feature1
D:\githubtest>git checkout feature1
Switched to branch 'feature1'

D:\githubtest>git branch
error: cannot spawn less: No such file or directory
* feature1
  master

# 在feature1分支中新创建一个文件a.txt,再add 和commit
D:\githubtest>copy con a.txt
a.txt feature1
^Z
已复制         1 个文件。

D:\githubtest>git add a.txt

D:\githubtest>git status
On branch feature1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   a.txt


D:\githubtest>git commit -m "add a.txt"
[feature1 5ce8771] add a.txt
 1 file changed, 1 insertion(+)
 create mode 100644 a.txt

# 使用git checkout -b feature1-1 =  创建分支 + 跳转到feature1-1分支, 相当于git branch xxxx + git checkout xxx
D:\githubtest>git checkout -b feature1-1
Switched to a new branch 'feature1-1'

D:\githubtest>git branch
error: cannot spawn less: No such file or directory
  feature1
* feature1-1
  master

# 删除分支使用 git branch -d xxxx分支名
D:\githubtest>git branch -d feature1
Deleted branch feature1 (was 5ce8771).

D:\githubtest>git branch
error: cannot spawn less: No such file or directory
* feature1-1
  master

## 如果在feature1-1分支做了修改和创建新文件,并add和commit后, 再删除分支 feature1-1, 系统发现有修改改,会提示无法删除
### 这时会用的 merge合并操作
D:\githubtest>git branch
error: cannot spawn less: No such file or directory
* feature1-1
  master

D:\githubtest>copy con b.txt
in feature1-1 b.txt
^Z
已复制         1 个文件。

D:\githubtest>git add b.txt

D:\githubtest>git commit -m "add b.txt"
[feature1-1 8658370] add b.txt
 1 file changed, 1 insertion(+)
 create mode 100644 b.txt

D:\githubtest>git branch -d feature1-1
error: Cannot delete branch 'feature1-1' checked out at 'D:/githubtest'

如果要把feature1-1合并到master,先切换到master分支,再git merge, 最后将合并后的master代码push 到远端
D:\githubtest>git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

D:\githubtest>git branch
error: cannot spawn less: No such file or directory
  feature1-1
* master

D:\githubtest>git merge feature1-1
Updating e932c5c..8658370
Fast-forward
 a.txt | 1 +
 b.txt | 1 +
 2 files changed, 2 insertions(+)
 create mode 100644 a.txt
 create mode 100644 b.txt

D:\githubtest>git push
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 502 bytes | 502.00 KiB/s, done.
Total 6 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/wggglggg/githubtest.git
   e932c5c..8658370  master -> master

# 合并后的master再push提交到远端, 远端是否就有master和feature1-1两个分支呢?,答案是否定的
## 先切换到feature1-1分支, 再使用git push origin feature1-1将新分支也推到远端github上
D:\githubtest>git checkout feature1-1
Switched to branch 'feature1-1'

D:\githubtest>git branch
error: cannot spawn less: No such file or directory
* feature1-1
  master

D:\githubtest>git push origin feature1-1
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'feature1-1' on GitHub by visiting:
remote:      https://github.com/wggglggg/githubtest/pull/new/feature1-1
remote:
To https://github.com/wggglggg/githubtest.git
 * [new branch]      feature1-1 -> feature1-1

# 如何 删除本地分支feature1-1与远端分支feature1-1, 先切换到别的分支,再删除
D:\githubtest>git branch
error: cannot spawn less: No such file or directory
* feature1-1
  master

D:\githubtest>git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

## 删除本地分支feature1-1
D:\githubtest>git branch -d feature1-1
Deleted branch feature1-1 (was 8658370).

## 删除远端分支feature1-1, 这样github上feature1-1分支就被 删除了
D:\githubtest>git push origin :feature1-1
To https://github.com/wggglggg/githubtest.git
 - [deleted]         feature1-1

# 本地分支叫feature1-1, 远端的分支叫f1
D:\githubtest>git branch
error: cannot spawn less: No such file or directory
* feature1-1
  master

D:\githubtest>copy con c.txt
in feature1-1 c.txt^Z
已复制         1 个文件。

D:\githubtest>git add -A

D:\githubtest>git commit -m "add c.txt"
[feature1-1 051edf4] add c.txt
 1 file changed, 1 insertion(+)
 create mode 100644 c.txt

D:\githubtest>git push origin feature1-1:f1
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 280 bytes | 280.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'f1' on GitHub by visiting:
remote:      https://github.com/wggglggg/githubtest/pull/new/f1
remote:
To https://github.com/wggglggg/githubtest.git
 * [new branch]      feature1-1 -> f1

-----------------------------------------以下为branch的应用-----------------------------------------------------
一 查看日志, 最上面的是最近操作的日志, git log --oneline为查看简单日志, git log 为查看详细日志
D:\githubtest>git log --oneline
error: cannot spawn less: No such file or directory
8658370 (HEAD -> master, origin/master) add b.txt
5ce8771 add a.txt
e932c5c ''
63ec8f1 Update README.md
82f8433 Update README.md
96c91f4 'first'


D:\githubtest>git log
error: cannot spawn less: No such file or directory
commit 8658370d54747cc66e94b8b035e93b72e47e0840 (HEAD -> master, origin/master)
Author: wggglggg <wggglggg@hotmail.com>
Date:   Thu Jun 10 10:30:54 2021 +0800

    add b.txt

commit 5ce877183f408df38b6f2fed8845a16995400b3f
Author: wggglggg <wggglggg@hotmail.com>
Date:   Thu Jun 10 10:19:05 2021 +0800

    add a.txt

commit e932c5c74e8eb9672f056ec39a628642e87e65ba
Author: wggglggg <wggglggg@hotmail.com>
Date:   Thu Jun 10 10:06:54 2021 +0800

    ''

commit 63ec8f116f1db3a06c24f3902c0bc69795ffbd19
Author: wggglggg <72190085+wggglggg@users.noreply.github.com>
Date:   Thu Jun 10 09:59:15 2021 +0800

    Update README.md

commit 82f8433cbe2a0d546946c6c43e50c0340966fc4a
Author: wggglggg <72190085+wggglggg@users.noreply.github.com>
Date:   Thu Jun 10 09:58:54 2021 +0800

    Update README.md

commit 96c91f48297339312acfed95e3680f5bb1603b0c
Author: wggglggg <72190085+wggglggg@users.noreply.github.com>
Date:   Thu Jun 10 09:49:59 2021 +0800

    'first'

二 只选择前几条修改信息用git log --oneline -3         -3为前三条信息
D:\githubtest>git log --oneline -3
error: cannot spawn less: No such file or directory
8658370 (HEAD -> master, origin/master) add b.txt
5ce8771 add a.txt
e932c5c ''

三 查看每一个修改信息里面做了哪些操作用 git show xxxxxx(hash号)
D:\githubtest>git show 8658370
error: cannot spawn less: No such file or directory
commit 8658370d54747cc66e94b8b035e93b72e47e0840 (HEAD -> master, origin/master)
Author: wggglggg <wggglggg@hotmail.com>
Date:   Thu Jun 10 10:30:54 2021 +0800

    add b.txt

diff --git a/b.txt b/b.txt
new file mode 100644
index 0000000..d106b9c
--- /dev/null
+++ b/b.txt
@@ -0,0 +1 @@
+in feature1-1 b.txt

四 使用 git log --all --decorate --oneline --graph来查看日志
D:\githubtest>git log --all --decorate --oneline --graph
error: cannot spawn less: No such file or directory
* 8658370 (HEAD -> master, origin/master) add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'
使用简写来查看, 要先去c:\users\xxxxx\.gitconfig文件中[alias]项下面添加dog = log --all --decorate --oneline --graph
这样可以使用git dog查看所有日志
D:\githubtest>git dog
error: cannot spawn less: No such file or directory
* 8658370 (HEAD -> master, origin/master) add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'

--------------------------------------回滚branch----------------------------------------------------
# 当commit后, 想回滚前一个记录可以用git reset xxxxxx记录id, 常用参数有--soft(保留仓库与缓存区) --mixed(默认保存仓库) --hard(都不保留),  如果个人开发, reset适合在自己的分支上回滚, 如果多人开发, revert适合在master上回滚自动commit记录, 因为revert会保留所有记录.
D:\githubtest>git branch
error: cannot spawn less: No such file or directory
* master

D:\githubtest>copy con m1.txt
this is m1.txt create from master^Z
已复制         1 个文件。

D:\githubtest>dir
 驱动器 D 中的卷是 bak
 卷的序列号是 22CC-5F5E

 D:\githubtest 的目录

2021/06/10  13:47    <DIR>          .
2021/06/10  13:47    <DIR>          ..
2021/06/10  10:35                16 a.txt
2021/06/10  10:35                21 b.txt
2021/06/10  13:32                24 fa.txt
2021/06/10  13:47                33 m1.txt
2021/06/10  10:05                24 README.md
               5 个文件            118 字节
               2 个目录 821,066,039,296 可用字节

D:\githubtest>git add m1.txt

D:\githubtest>git ci -m "add m1.txt"
[master 66481ad] add m1.txt
 1 file changed, 1 insertion(+)
 create mode 100644 m1.txt

D:\githubtest>git dog
error: cannot spawn less: No such file or directory
* 66481ad (HEAD -> master) add m1.txt
* 16ff125 (origin/master) add fa.txt
* 8658370 add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'

D:\githubtest>git reset 16ff125                       -----------------回滚操作

D:\githubtest>git dog
error: cannot spawn less: No such file or directory
* 16ff125 (HEAD -> master, origin/master) add fa.txt
* 8658370 add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'

# 如果不保留仓库与缓存区  就使用--hard
D:\githubtest>dir
 驱动器 D 中的卷是 bak
 卷的序列号是 22CC-5F5E

 D:\githubtest 的目录

2021/06/10  13:47    <DIR>          .
2021/06/10  13:47    <DIR>          ..
2021/06/10  10:35                16 a.txt
2021/06/10  10:35                21 b.txt
2021/06/10  13:32                24 fa.txt
2021/06/10  13:47                33 m1.txt
2021/06/10  10:05                24 README.md
               5 个文件            118 字节
               2 个目录 821,066,039,296 可用字节

D:\githubtest>git dog
error: cannot spawn less: No such file or directory
* 16ff125 (HEAD -> master, origin/master) add fa.txt
* 8658370 add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'

D:\githubtest>git reset 63ec8f1 --hard
HEAD is now at 63ec8f1 Update README.md

D:\githubtest>git dog
error: cannot spawn less: No such file or directory
* 16ff125 (origin/master) add fa.txt
* 8658370 add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 (HEAD -> master) Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'

D:\githubtest>dir
 驱动器 D 中的卷是 bak
 卷的序列号是 22CC-5F5E

 D:\githubtest 的目录

2021/06/10  13:53    <DIR>          .
2021/06/10  13:53    <DIR>          ..
2021/06/10  13:47                33 m1.txt
2021/06/10  13:53                32 README.md
               2 个文件             65 字节
               2 个目录 821,065,936,896 可用字节

# 可以使用 git reflog 查看所有的commit id, 并回滚
D:\githubtest>git reflog
error: cannot spawn less: No such file or directory
63ec8f1 (HEAD -> master) HEAD@{0}: reset: moving to 63ec8f1
16ff125 (origin/master) HEAD@{1}: reset: moving to 16ff125
66481ad HEAD@{2}: commit: add m1.txt
16ff125 (origin/master) HEAD@{3}: merge f1: Fast-forward
8658370 HEAD@{4}: checkout: moving from f1 to master
16ff125 (origin/master) HEAD@{5}: commit: add fa.txt
8658370 HEAD@{6}: checkout: moving from master to f1
8658370 HEAD@{7}: checkout: moving from 'f1' to master
4662d64 HEAD@{8}: checkout: moving from master to 'f1'
8658370 HEAD@{9}: checkout: moving from master to master
8658370 HEAD@{10}: checkout: moving from 'f1' to master
4662d64 HEAD@{11}: commit: add fa.txt
8658370 HEAD@{12}: checkout: moving from master to 'f1'
8658370 HEAD@{13}: checkout: moving from feature1-1 to master
051edf4 HEAD@{14}: commit: add c.txt
8658370 HEAD@{15}: checkout: moving from master to feature1-1
8658370 HEAD@{16}: checkout: moving from feature1-1 to master
8658370 HEAD@{17}: checkout: moving from master to feature1-1
8658370 HEAD@{18}: merge feature1-1: Fast-forward
e932c5c HEAD@{19}: checkout: moving from feature1-1 to master
8658370 HEAD@{20}: commit: add b.txt
5ce8771 HEAD@{21}: checkout: moving from feature1 to feature1-1
5ce8771 HEAD@{22}: commit: add a.txt
e932c5c HEAD@{23}: checkout: moving from master to feature1
e932c5c HEAD@{24}: commit: ''
63ec8f1 (HEAD -> master) HEAD@{25}: pull: Fast-forward
96c91f4 HEAD@{26}: commit (initial): 'first'

D:\githubtest>git reset 16ff125 --hard         ----------用了hard回滚, 但是m1.txt却不在缓存区,即使git push也无法将此文件推送到github
HEAD is now at 16ff125 add fa.txt

D:\githubtest>dir
 驱动器 D 中的卷是 bak
 卷的序列号是 22CC-5F5E

 D:\githubtest 的目录

2021/06/10  14:03    <DIR>          .
2021/06/10  14:03    <DIR>          ..
2021/06/10  14:03                16 a.txt
2021/06/10  14:03                21 b.txt
2021/06/10  14:03                24 fa.txt
2021/06/10  13:47                33 m1.txt
2021/06/10  14:03                24 README.md
               5 个文件            118 字节
               2 个目录 821,065,842,688 可用字节

D:\githubtest>git st
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        m1.txt

nothing added to commit but untracked files present (use "git add" to track)

# git revert  适合在公共分支master上回滚, 回滚结束后会自动添加一条commit记录, 也之前之后保留所有的commit记录
D:\githubtest>git dog
error: cannot spawn less: No such file or directory
* 4e0d976 (HEAD -> master, origin/master) add m1.txt
* 16ff125 add fa.txt
* 8658370 add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'

D:\githubtest>git revert 16ff125


D:\githubtest>git commit -m "delete fa.txt"
[master 8b6fc54] delete fa.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 fa.txt

D:\githubtest>dir
 驱动器 D 中的卷是 bak
 卷的序列号是 22CC-5F5E

 D:\githubtest 的目录

2021/06/10  14:12    <DIR>          .
2021/06/10  14:12    <DIR>          ..
2021/06/10  14:03                16 a.txt
2021/06/10  14:03                21 b.txt
2021/06/10  13:47                33 m1.txt
2021/06/10  14:03                24 README.md
               4 个文件             94 字节
               2 个目录 821,065,703,424 可用字节

D:\githubtest>git dog
error: cannot spawn less: No such file or directory
* 8b6fc54 (HEAD -> master) delete fa.txt
* 4e0d976 (origin/master) add m1.txt
* 16ff125 add fa.txt
* 8658370 add b.txt
* 5ce8771 add a.txt
* e932c5c ''
* 63ec8f1 Update README.md
* 82f8433 Update README.md
* 96c91f4 'first'
