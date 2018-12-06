# git 基本知识

## 初始化仓库

git init

git clone [url]

## 向下一笔提交中添加内容

git add 

## 查看git库状态

git status

git status -s 

## 比较差异

git diff       //工作目录与快照之间的差别

git diff --staged   //暂存区与快照之间的差别

git diff --check   //检测空白错误

## 删除文件

git rm

git rm -f  // 修改过并且已经放到暂存区

git rm --cached  //删除暂存区但保留工作目录中文件

## 重命名

git mv

## 查看提交历史

git log

git log -p   //显示修改

git log -p -2  //最近两笔提交

git log --stat  //增加统计信息

git log --pretty=  [short|full|fuller]  //显示效果

git log --pretty=format:"%h %an %ad %s"  //显示格式

| 参数| 含义 |
|----|-----|
|%h|提交sha-1|
|%p|父提交hash值|
|%t|tree哈希值|
|%an|作者名字|
|%ae|作者email|
|%ad|修改时间|
|%s|注释|

git log --graph  //图像显示提交过程

git log --before/--since=2011-01-01

git log --after/--until

git log --grep keyword   //检索

git log --author xxx  --grep keyword --all-match //同时满足

git log -Sxxxx    //检索提交的内容中含有某个字符串

git log --oneline --decorate --graph --all   //输出提交历史、各个分支的指向以及分支交叉情况

git log --pretty=format:"%h - %s" --author=gitster --since="2018-01-01" --before="2018-11-01" --no-merges -- t/

## 提交

git commit -m "xxxxxx"

git commit --amend

## 还原暂存区的修改

git reset HEAD <file>

## 还原工作区修改

git checkout -- <file>

## 查看远程仓库

git remote -v

git remote show origin //详细内容

git remote rename x x  //重命名

git remote rm x       //删除

git remote add shortname <url>  //添加，shortname 代表url  git fetch使用

## 抓取

get fetch    //只抓取不合并

git pull     //抓取并且合并

## 推送

git push origin master

## 标签

git tag  //列出标签

git tag -l "xxxxx" //查找特定标签

git tag -a xxxx -m "xxxx"  //创建附注标签

git tag xxxxx   //创建轻量标签

git tag -a xxx 哈希值   //后期给“哈希值”打附注标签

git tag -d tagname //删除tag

git show xxxtag   //查看标签内容

git push origin tagname  //标签推送到远程库

git push origin --tags   //一次推送多个标签

git checkout -b branchname tagname //检出某个标签

## 分支

//======

git branch branch-name     //创建分支

git branch branch-name master //基于master创建分支

git checkout branch-name   //切换分支

git checkout -b branch-name  //创建以及切换分支

git checkout -b branch-name master //基于master创建及切换分支

//=======

git branch  //查看分支

git branch -v //查看每个分支的最后一次提交

git brach -vv  //

git branch --merged/--no-merged   //查看已经合并/没有合并的分支

//=====

git branch -d branch-name  //删除分支

git branch -D branch-name  //强制删除分支

//======

git remote add jessica git://github.com/jessica/myproject.git //添加远程分支
 
git fetch jessica  //抓取远程分支

git checkout -b rubyclient jessica/ruby-client //建立分支

//======

git pull https://github.com/onetimeguy/project  //直接进行抓取和合并，不必建立远程分支

//======

## 合并

git checkout master     //切换回master分支

git merge hotfix        //将hotfix修改合并到master分支

git merge origin/serverfix  //将远程分支合并到当前分支

git merge --no-commit --squash featureB  //--squash 所有提交压缩成一个变更集，--no-commit 延迟生成合并提交

//=====

git push (origin) (branch)

git push origin severfix   //将本地分支推送到远程服务器

git push origin severfix:awesomebranch  //将本地分支推送到远程命令为awesomebranch

git push origin --delete serverfix     //删除远程服务器分支

git push -u origin featureA            //推送本地分支到远程仓库,-u == --set-upstream

//====

git checkout -b branch origin/branch   //创建跟踪分支branch跟踪远程分支origin/branch

git checkout --track origin/serverfix //跟踪分支的简写创建方法

git branch -u origin/serverfix       //设置当前分支跟踪远程分支origin/serverfix

@{u} //引用上游分支

git brach -vv    //查看设置的所有跟踪分支

//
## 变基
git checkout experiment   //切换到experiment分支

git rebase master         //将experiment分支移动到master分支

git checkout master       //切换到maser分支

git merge experiment     //执行快速合并，maser和experiment指向同一个位置

//

git rebase --onto maser server client //取出client分支，但是不在server分支的修改，然后把他们在maser分支上重演

git checkout maser

git merge client

//

git rebase master server

git checkout maser

git merge server

//==============

git pull --rebase  //pull 变基



//============

## 协议

### 本地协议

git clone --bare /path/to/git/project  project.git

git clone /opt/git/project.git

git clone file:///opt/git/prohect.git

### 智能HTTP协议

$ cd /var/www/htdocs/

$ git clone --bare /path/to/git_project gitproject.git

$ cd gitproject.git

$ mv hooks/post-update.sample hooks/post-update

$ chmod a+x hooks/post-update

$ git clone https://example.com/gitproject.git

### SSH协议

$ cd /opt/git

$ mkdir project.git

$ cd project.git

$ git init --bare --shared

$ git clone ssh://user@server/project.git

### git协议

git daemon --reuseaddr --base-path=/opt/git/ /opt/git/  //监听9418端口

cd /opt/git

mkdir project.git

cd project.git

git init --bare --shared

touch git-daemon-export-ok

git git://server/project.git

### gitweb

cd /opt/git/project.git

git instaweb    //打开web浏览

git instaweb --stop //关闭web浏览

## patch

git format-patch -M origin/master  //-M 查找重命名，从origin/master的开始提交的修改

git apply patch   //类似patch -p1命令，apply all or abort all模式,git diff或者UNIX diff格式补丁

git apply --check patch //检测patch是否可顺利应用

git am patch     //应用format-patch格式的补丁

git am -3 patch  //对冲突执行三方合并，解决重复提交的补丁

git am -3 -i patch //-i 确认模式

git cherry-pick e43a6fd3e94888d76779ad79fb568ed180e5fcdf  //拣选,形成新的提交

git log contrib --not master  //检测master分支中尚未包含的提交

git diff  master   //本分支与master最新提交的差异，master变成本分支需要的修改

git diff master...contrib   //master分支与contrib分支的共同祖先到contrib的修改

## 构建与发布

### 签名标签与验证

//export GPG_TTY=$(tty)

//设置pinentry

//gpg --list-key

git config --global user.signingkey pub-key

git -a -export pub-key | git hash-object -w --stdin   //向git中写入公钥blob对象

//659ef797d181633c87ec71ac3f9ba29fe5775b92

git tag -a gpg-pub-key 659ef797d181633c87ec71ac3f9ba29fe5775b92  //创建指向公钥blob

git tag -s v1.1 -m "v1.1 tag"  //创建签名的标签

git push --tags //推送标签

git show gpg-pub-key | gpg --import  //其他人导入key

git tag -v v1.1

//====================

git commit -S -m "signed commit"  //签名提交

git log --show-signature         //显示签名

### 发布

git description master //最近的标签名、自该标签之后的提交数目和你所描述的提交的部分 SHA-1值

git archive master --prefix='project/' | gzip > xxxxx.tar.gz  //快照归档

git archive master --prefix='project/' --format=zip  > xxxx.zip

git shortlog --no-merges master --not v1.0  //制作简报

## git 工具

### rev-parse

git rev-parse topic1   //topic1 对应的hash值

### reflog

git reflog            //记录HEAD和分支引用的变更

### ^与~

//===========
git show sha^         //第一父提交

git show sha^2        //第二父提交,适用于分支,即合并过来的提交

git show sha~         //与^等价

git show sha~2        //跟数字式存在区别第一父提交的第一父提交

git show sha~2^2     //第一父提交的第一父提交的第二父提交

//===========       ~\^回溯的合并分支路径不同

### 提交区间

#### 双点

git log master..experiment   //在experiment分支但是不在master分支的提交

#### 三点

git log --left-right master...experiment  //在master或experiment分支，但是不同时在两个分支的提交，--left-right 指出在那个分支

#### 多点

git log master --not experiment  //在master分支但是不在experiment分支的修改

git log master ^experiment       //等价

### 交互式暂存

#### 部分暂存

//-p == --patch

git add -p file  //选择咱们这个文件的部分修改 

git reset -p file //重置部分

git checkout -p file

git stash save -p 

#### 储藏与清理

git stash 

git stash --keep-index   //已经add过的文件不储藏

git stash --include-untracked  //储藏包括未跟踪的文件

git stash --patch     //挑选储藏

git stash list   //列出储藏栈

git stash apply --index  //应用储藏，不清栈

git stash pop  //应用并清栈

git stash drop  //放弃应用

git stash branch branch-name  //基于储藏新建一个分支

### 清理工作目录

git clean   //清除在.gitignore中未匹配的未跟踪文件

git clean -f -d //强制清除所有未跟踪文件及空目录,不在.gitignore文件, -d 目录

git clean -d -x -f  //忽略.gitignore

git clean -n       //-n 测试，不真正移除

git stash --all  //更保险

### 搜索

git grep str


参数|含义|
---
|-n|显示行号|
|-count|显示简短统计信息|
|-p|查看str属于的方法和函数|
|-and|查看复杂的字符串组合|

git grep --break --heading -n -e '#define' --and \( -e LINK -e BUF_MAX \) v1.8.0  //查看分支

git log -Sxxxxx --oneline  //检索提交的字符串，查看何时引入

git log -L :git_deflate_bound:zlib.c   //查找在zlib.c中函数对应的变更

### 重新历史

#### 修改最近一次提交历史

git commit --amend

#### 修改多次提交历史


//修改提交
git rebase -i HEAD~3

pick f7f3f6d changed my name a bit                           ------> *edit* f7f3f6d changed my name a bit
pick 310154e updated README formatting and added blame
pick a5f4a0d added cat-file

git commit --amend

git rebase --continue

//重新排序提交

git rebase -i HEAD~3

pick f7f3f6d changed my name a bit <-------------------------
pick 310154e updated README formatting and added blame     |
pick a5f4a0d added cat-file       <------------------------

//压缩提交

git rebase -i HEAD~3

pick f7f3f6d changed my name a bit
*squash* 310154e updated README formatting and added blame
*squash* a5f4a0d added cat-file

//拆分提交

git rebase -i HEAD~3

pick f7f3f6d changed my name a bit
*edit* 310154e updated README formatting and added blame
pick a5f4a0d added cat-file

git reset HEAD^
git add README
git commit -m 'updated README formatting'
git add lib/simplegit.rb
git commit -m 'added blame'
git rebase --continue

#### filter-branch

git filter-branch --tree-filter  'rm -f password.txt'  HEAD  //从每次提交中删除一个文件 --all选项应用到所有分支

git filter-branch  --subdirectory-filter trunk HEAD  //让 trunk 子目录作为每一个提交的新的项目根目录

git filter-branch --commit-filter '
	if [ "$GIT_AUTHOR_EMAIL" = "schacon@localhost" ];
	then
		GIT_AUTHOR_NAME="Scott Chacon";
		GIT_AUTHOR_EMAIL="schacon@example.com";
		git commit-tree "$@";
	else
		git commit-tree "$@";
	fi' HEAD                                          //全局修改邮箱地址


