# git 基本操作

## 初始化仓库

1.  初始化git仓

```
git init
```
2.   创建裸仓库，--shared选项向仓库的组用户增加可写权限

```
git init --bare --shared 
```
3. 克隆一个仓库， --recursive选项可以使submodule模块添加自动被克隆
```
git clone --recursive [url]
```
## 向提交中添加内容
1. add 操作可以向下一笔提交中添加内容，-p或--patch添加文件部分内容
```
git add   [file-list]
git add -p  [file-list]
```
## 查看git库状态
1. 查看库状态，-s或--short输出简短格式
```
git status

git status -s 
```
## 比较差异
1. 工作目录与快照之间的差别
```
git diff     
```
2. 暂存区与快照之间的差别
```
git diff --staged
git diff --cached 
```
3. 检测空白错误
```
git diff --check  
```
4. 分支间差异

```                 
       A---B---C topic
     /
 D---E---F---G master

```
```
git diff maste    //显示C与G之间的差别
```
```
git diff master...topic   //显示E与C之间的差异
```
## 删除文件
1. 删除工作目录中文件
```
git rm [file-list]
```
2. 删除暂存区中文件
```
git rm -f [file-list]  // 已经放到暂存区并且此时在工作目录中也有修改

git rm --cached [file-list] //删除暂存区但保留工作目录中文件
```
## 重命名
```
git mv file_from file_to
```
## 查看提交历史
1. 按提交时间显示所有更新
```
git log
```
git log常用选项

|选项|说明                                                               |
|--------------|---------------------------------------------------|
|-p             |按照补丁格式显示每个更新之间的差异|
|-n         |显示最近的n笔提交                              |
|--stat        |显示文件修改统计信息                         |
|--shortstat|只显示 --stat 中最后的行数修改添加移除统计|
|--graph     |使用 ASCII 图形显示分支合并历史|
| --oneline  |每个提交信息显示在单独的一行内|
|--all           |显示所有的分支信息|
| --decorate|查看各个分支当前所指的对象|
|--name-only|仅在提交信息后显示已修改的文件清单|
|--name-status|显示新增、修改、删除的文件清单|
|--relative-date|使用较短的相对时间显示（比如，“2 weeks ago”）|
|--since , --after|仅显示指定时间之后的提交|
|--until , --before|仅显示指定时间之前的提交|
|--author|仅显示指定作者相关的提交|
|--committer|仅显示指定提交者相关的提交|
|--grep|仅显示含指定关键字的提交|
|-S<keyword>|仅显示添加或移除了某个关键字的提交|
|--pretty|使用其他格式显示历史提交信息,可用的选项包括 oneline，short,full，fuller 和 format（后跟指定格式）。|

```
git log --pretty=format:"format string"
```
**格式化字符串选项**

| 选项     | 说明              |
|-----------|------------------|
|%H       |commit对象的完整哈希值|
|%h       |commit对象的简短哈希值|
|%T       |tree对象的完整哈希值|
|%t        |tree对象的简短哈希值| 
|%P      |parent对象的完整哈希值|
|%p      |parent对象的简短哈希值|
|%an    |作者名字|
|%ae    |作者email|
|%ad    |作者修改时间|
|%ar    | 作者修改日期，按多久以前的方式显示|
|%cn    |作者名字|
|%ce    |作者email|
|%cd    |作者修改时间|
|%cr    | 作者修改日期，按多久以前的方式显示|
|%s     |注释|

3. 例子
```
$ git log --stat

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date: Mon Mar 17 21:52:11 2008 -0700
changed the version number
Rakefile | 2 +-
1 file changed, 1 insertion(+), 1 deletion(-)
```

```
$ git log --pretty=oneline


ca82a6dff817ec66f44342007202690a93763949 changed the version number
085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 removed unnecessary test
a11bef06a3f659402fe7563abf99ad00de2209e6 first commit
```

```
$ git log --pretty=format:"%h - %an, %ar : %s"

ca82a6d - Scott Chacon, 6 years ago : changed the version number
085bb3b - Scott Chacon, 6 years ago : removed unnecessary test
a11bef0 - Scott Chacon, 6 years ago : first commit
```
```
$ git log --pretty=format:"%h %s" --graph


* 2d3acf9 ignore errors from SIGCHLD on trap
* 5e3ee11 Merge branch 'master' of git://github.com/dustin/grit
|\
| * 420eac9 Added a method for getting the current branch.
* | 30e367c timeout code and tests
* | 5a09431 add timeout protection to grit
* | e1193f8 support for heads with slashes in them
|/
* d6016bc require time for xmlschema
* 11d191e Merge branch 'defunkt' into local
```

```
$ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
--before="2008-11-01" --no-merges -- t/

5610e3b - Fix testcase failure when extended attributes are in use
acd3b9e - Enhance hold_lock_file_for_{update,append}() API
f563754 - demonstrate breakage of detached checkout with symbolic link HEAD
d1a43f2 - reset --hard/read-tree --reset -u: remove unmerged new paths
51a94af - Fix "checkout --track -b newbranch" on detached HEAD
b0ad11e - pull: allow "git pull origin $something:$current_branch" into an unborn bran
ch
```
## 提交修改
```
git commit -m "log message"
```
```
git commit --amend
```
## 还原修改
1. 取消暂存区的修改

```
git reset HEAD <file>
```
2. 取消工作区修改

```
git checkout -- <file>
```
## 查看远程仓库
1. 指定选项 -v ，会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL
```
$ git remote -v

origin https://github.com/schacon/ticgit (fetch)
origin https://github.com/schacon/ticgit (push)
```
2. 详细内容

```
* remote origin
  Fetch URL: git@github.com:xxxxx/notebook.git
  Push  URL: git@github.com:xxxxxx/notebook.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up-to-date) 
```
3. 添加远程分支

```
$ git remote add pb https://github.com/paulboone/ticgit

$ git remote -v
origin https://github.com/schacon/ticgit (fetch)
origin https://github.com/schacon/ticgit (push)
pb https://github.com/paulboone/ticgit (fetch)
pb https://github.com/paulboone/ticgit (push)
```
4. 重命名远程仓库

```
git remote rename  from  to  
```
5. 删除远程仓库
```
git remote rm  branch-name
```
## 抓取
1. 只赚取不合并

```
get fetch <remote-branch>
```
2. 抓取并且合并

```
git pull --rebase 

git pull https://github.com/onetimeguy/project  //直接进行抓取和合并，不必建立远程分支
```

## 推送修改
1. git push <remote-host>  <local-branch>

```
git push origin master
```
2. git push <remote>  <local-branch>:<remote-branch> 
```
git push origin topic:master
```
3. 删除远程分支
```
git push <remote>  :<remote-branch> 
```
```
git push --delate <remote-branch> 
```
## 标签
1. 列出标签

```
git tag  
```
2. 查找特定标签

```
git tag -l  tag 
```
3. 创建附注标签

```
git tag -a v1.0  -m "message"  
```
4. 创建轻量标签

```
git tag v1.0   
```
5. 后期给“哈希值”打附注标签

```
git tag -a v1.0  sha-1  
```
6. 删除tag

```
git tag -d <tagname>
```
7.  查看标签内容

```
git show <tagname>  
```
8. 标签推送到远程库

```
git push origin <tagname>  
```
9. 一次推送多个标签

```
git push origin --tags 
```
10. 检出某个标签
```
git checkout -b branchname tagname 
```
## 分支

1. 创建分支
```

git branch <branch-name>     //创建分支

git branch <branch-name> master //基于master创建分支
```
2. 切换分支
```
git checkout branch-name   //切换分支

git checkout -b branch-name  //创建并切换分支

git checkout -b branch-name master //基于master创建及切换分支
```
3. 查看分支
```
git branch  //查看分支

git branch -v //查看每个分支的最后一次提交

git brach -vv  //查看设置的所有跟踪分支

git branch --merged/--no-merged   //查看已经合并/没有合并的分支

```
4. 删除分支
```
git branch -d branch-name  //删除分支

git branch -D branch-name  //强制删除分支

```
## 合并
```
git checkout master     //切换到master分支

       A---B---C hotfix
     /
 D---E---F---G master

git merge hotfix        //将hotfix修改合并到master分支

       A---B---C            hotfix
     /           \
 D---E---F---G ---H     master


```
```
git merge origin/serverfix  //将远程分支合并到当前分支
```
```
git merge --no-commit --squash featureB  //--squash 所有提交压缩成一个变更集，--no-commit 延迟生成合并提交
```
//=====

## 分支跟踪
```
git checkout --track origin/serverfix        //跟踪分支的简写创建方法

git branch -u origin/serverfix               //设置当前分支跟踪远程分支origin/serverfix

git push -u origin origin featureB:featureBee      //推送本地分支到远程仓库并设置featureB跟踪featureBee

@{u} //引用上游分支

git brach -vv    //查看设置的所有跟踪分支
```

## 变基
在分支上重演变基分支的提交
1. 
```
git checkout experiment   //切换到experiment分支

       A---B---C   experiment
     /           
 D---E---F---G   master

git rebase master         //将experiment分支移动到master分支
  
             
 D---E---F---G---A'---B'---C'   experiment
            master

git checkout master       //切换到maser分支

git merge experiment     //执行快速合并，maser和experiment指向同一个位置

 D---E---F---G---A'---B'---C'   experiment/master

```
2. 
```
git rebase --onto maser server client //取出client分支，但是不在server分支的修改，然后把他们在maser分支上重演

git checkout maser

git merge client
```
3. 
```
git rebase master server

git checkout maser

git merge server
```

## 补丁

1. 生成补丁
```
git format-patch -M origin/master  //-M 查找重命名，从origin/master的开始提交的修改
```
2. 检查补丁

```
git apply --check patch //检测patch是否可顺利应用
```
3.应用补丁

```
git apply patch   //类似patch -p1命令，apply all or abort all模式,git diff或者UNIX diff格式补丁
```
```
git am patch     //应用format-patch格式的补丁
```
4. 解决重复提交的补丁

```
git am -3 patch  //对冲突执行三方合并，解决重复提交的补丁

git am -3 -i patch //-i 确认模式
```
5. cherri-pick
```
git cherry-pick e43a6fd3e94888d76779ad79fb568ed180e5fcdf  //拣选,形成新的提交
```

## 构建与发布

### 签名标签与验证
1. 本地配置
```
//export GPG_TTY=$(tty)

//设置pinentry

//gpg --list-key

git config --global user.signingkey pub-key
```
2. 生成公钥的blob对象
```
git -a -export pub-key | git hash-object -w --stdin   //向git中写入公钥blob对象

//659ef797d181633c87ec71ac3f9ba29fe5775b92
```
3. 创建指向公钥的标签
```
git tag -a gpg-pub-key 659ef797d181633c87ec71ac3f9ba29fe5775b92  //创建指向公钥blob
```
4. 创建签名标签

```
git tag -s v1.1 -m "v1.1 tag"  //创建签名的标签
```
5. 推送标签
```
git push --tags 
```
6. 其他人导入公钥签名
```
git show gpg-pub-key | gpg --import  //其他人导入key
```
6. 验证标签签名
```
git tag -v v1.1
```
### 签名commit
```
git commit -S -m "signed commit"  //签名提交

git log --show-signature         //显示签名
```
### 发布
1. 生成一个构建号
```
git description master //最近的标签名、自该标签之后的提交数目和你所描述的提交的部分 SHA-1值

v1.6.2-rc1-20-g8c5b85c
```

2. 快照归档
```
git archive master --prefix='project/' | gzip > xxxxx.tar.gz  //快照归档

git archive master --prefix='project/' --format=zip  > xxxx.zip
```
3. 制作简报
比如，你的上一次发布名称是 v1.0.1，那么下面的命
令可以给出上次发布以来所有提交的总结：
```
$ git shortlog --no-merges master --not v1.0.1

Chris Wanstrath (8):
Add support for annotated tags to Grit::Tag
Add packed-refs annotated tag support.
Add Grit::Commit#to_patch
Update version and History.txt
Remove stray `puts`
Make ls_tree ignore nils
Tom Preston-Werner (4):
fix dates in history
dynamic version method
Version bump to 1.0.2
Regenerated gemspec for version 1.0.2
```
## 协议

### 本地协议
使用本地协议克隆仓库

```
git clone --bare /path/to/git/project  project.git  //不创建工作目录
```
```
git clone /opt/git/project.git
```
```
git clone file:///opt/git/prohect.git
```
### 智能HTTP协议
1. 服务器端操作
```
$ cd /var/www/htdocs/

$ git clone --bare /path/to/git_project gitproject.git

$ cd gitproject.git

$ mv hooks/post-update.sample hooks/post-update

$ chmod a+x hooks/post-update
```
2. 客户端操作
```
$ git clone https://example.com/gitproject.git
```
### SSH协议
1. 服务器端操作
```
$ cd /opt/git

$ mkdir project.git

$ cd project.git

$ git init --bare --shared
```
2. 客户端操作
```
$ git clone ssh://user@server/project.git
```
### git协议
1. 服务器端操作
```
git daemon --reuseaddr --base-path=/opt/git/ /opt/git/  //监听9418端口

cd /opt/git

mkdir project.git

cd project.git

git init --bare --shared

touch git-daemon-export-ok
```
2. 客户端操作
```
git clone  git://server/project.git
```
### gitweb
通过web页面查看代码

1. 进入代码仓库
```
cd /opt/git/project.git
```
2. 启动web浏览服务
```
git instaweb    //打开web浏览
```
3. 关闭web浏览服务
```
git instaweb --stop //关闭web浏览
```
## git 工具

### rev-parse

```
git rev-parse topic1   //topic1 对应的hash值
```

### reflog
```
git reflog            //记录HEAD和分支引用的变更
```
### ^与~
~/^回溯的合并分支路径不同

```
git show sha^         //第一父提交

git show sha^2        //第二父提交,适用于分支,即合并过来的提交

git show sha~         //与^等价

git show sha~2        //跟数字式存在区别第一父提交的第一父提交

git show sha~2^2     //第一父提交的第一父提交的第二父提交

```     

### 提交区间

#### 双点

```
git log master..experiment   //在experiment分支但是不在master分支的提交
        E---F  master
      /
A---B---C---D  experiment

C
D

```
```
git log experiment ^master //与上面等价
git log experiment  --not master  //与上面等价
```
#### 三点

```
git log --left-right master...experiment  //在master或experiment分支，但是不同时在两个分支的提交，--left-right 指出在那个分支
```

### 交互式暂存

#### 部分暂存
```
//-p == --patch

git add -p file  //选择咱们这个文件的部分修改 

git reset -p file //重置部分

git checkout -p file

git stash save -p 
```
#### 储藏(stash)

1. 储藏
```
git stash 

git stash --keep-index   //已经add过的文件不储藏

git stash --include-untracked  //储藏包括未跟踪的文件

git stash --patch     //挑选储藏
```
2. 列出储藏栈
```
git stash list   //列出储藏栈
```
3. 应用储藏
```
git stash apply --index  //应用储藏，不清栈,--index 还原到暂存区

git stash pop  //应用并清栈
```
4. 放弃应用
```
git stash drop  //放弃应用
```
5. 基于储藏新建一个分支
```
git stash branch <branch-name>  //基于储藏新建一个分支
```
### 清理工作目录

```
git clean   //清除在.gitignore中未匹配的未跟踪文件

git clean -f -d //强制清除所有未跟踪文件及空目录,不在.gitignore文件, -d 目录

git clean -d -x -f  //忽略.gitignore， 清除所有非git仓内文件

git clean -n       //-n 测试，不真正移除

//git stash --all  //更保险
```
### 搜索

1. git grep str

|参数   |含义                          |
|--------|----------------------------|
|-n       |显示行号|
|-count|显示简短统计信息|
|-p       |查看str属于的方法和函数|
|-and   |查看复杂的字符串组合|

```
git grep --break --heading -n -e '#define' --and \( -e LINK -e BUF_MAX \) v1.8.0  //查看分支
```
2. git log搜索

```
git log -Sxxxxx --oneline  //检索提交的字符串，查看何时引入

git log -L :git_deflate_bound:zlib.c   //查找在zlib.c中函数对应的变更
```
### 修改提交历史

#### 修改最近一次提交历史
```
git commit --amend
```

#### 修改多次提交历史

1. 修改提交
```
git rebase -i HEAD~3

pick f7f3f6d changed my name a bit                           ------pick---> edit  //变更
pick 310154e updated README formatting and added blame
pick a5f4a0d added cat-file

git commit --amend

git rebase --continue
```
2. 重新排序提交

```
git rebase -i HEAD~3

pick f7f3f6d changed my name a bit <-------------------------

pick 310154e updated README formatting and added blame     |--交换

pick a5f4a0d added cat-file       <------------------------
```

3. 压缩提交

```
git rebase -i HEAD~3

pick f7f3f6d changed my name a bit
pick 310154e updated README formatting and added blame    pick-->squash
pick a5f4a0d added cat-file    pick-->squash
```

4. 拆分提交
```
git rebase -i HEAD~3

pick f7f3f6d changed my name a bit
edit 310154e updated README formatting and added blame   //停止
pick a5f4a0d added cat-file

git reset HEAD^      //回退提交

git add README    //拆分开始

git commit -m 'updated README formatting'

git add lib/simplegit.rb

git commit -m 'added blame'  //拆分结束

git rebase --continue
```
#### filter-branch

```
git filter-branch --tree-filter  'rm -f password.txt'  HEAD  //从每次提交中删除一个文件 --all选项应用到所有分支
```
```
git filter-branch  --subdirectory-filter trunk HEAD  //让 trunk 子目录作为每一个提交的新的项目根目录
```
git filter-branch --commit-filter '

	if [ "$GIT_AUTHOR_EMAIL" = "schacon@localhost" ];

	then
		GIT_AUTHOR_NAME="Scott Chacon";

		GIT_AUTHOR_EMAIL="schacon@example.com";

		git commit-tree "$@";

	else

		git commit-tree "$@";

	fi' HEAD                                          //全局修改邮箱地址


### reset

1. index和工作目录区不变
```
git reset --soft  HEAD~   //回退commit的提交，index和工作目录区不变
```
2. 工作目录区不变
```
git reset [--mixed] HEAD~  //回退add的修改，工作目录区不变
```
3. 全部回退
```
git reset --hard HEAD~    //回退仓库、index区、工作目录修改
```
4. 只修改暂存区
```
git reset sha-1 -- file.txt  //直接修改index区   //修改暂存区为sha-1 指定的对象
```
5. 与 check out区别

reset修改label的**_自身_**

checkout移动label的**_指向_**

```
git checkout develop  //HEAD指向了develop，develop和master本身没有变动

git reset master  //develop和master指向同一个提交

```

### 高级merge

#### 自动merge
```
git merge -Xours mundo  //-Xours 冲突时直接使用我们这边的修改  -Xtheirs 冲突时直接使用他们那边的修改
```
#### 合并子树

子树合并的思想是你有两个项目master和rack，你想将rack映射为master的一个子目录，并且可以同时跟踪rack项目，所要做的如下：

1. 项目映射

我们将 Rack 应用添加到你的项目，将rack项目映射为master的一个子目录
```
git remote add rack_remote https://github.com/rack/rack

git fetch rack_remote

git checkout -b rack_branch rack_remote/master

git checkout master

git read-tree --prefix=rack/ -u rack_branch //读取一个分支的根目录树到当前的暂存区和工作目录里
```

2. 如果rack项目有修改，可以获取这些修改

```
git checkout rack_branch

git pull

git checkout master
```
3. 查看这些差异
```
git diff-tree -p rack_branch //查看 rack 子目录和 rack_branch 分支的差异

git diff-tree -p rack_remote/master  //rack 子目和最近一次从服务器上抓取的 master 分支进行比较
```
4. 合并修改
```
git merge --squash -s recursive -Xsubtree=rack rack_branch

```
5. 切换到 rack_branch，向rack项目推送修改




#### 手动merge

1. 获取冲突文件的三方拷贝
```
git show :1:hello.rb > hello.common.rb

git show :2:hello.rb > hello.ours.rb

git show :3:hello.rb > hello.theirs.rb
```
2. 手动修改冲突

3. 手动合并

```
git merge-file -p hello.common.rb hello.ours.rb hello.theirs.rb  > hello.rb
```
4. 提交前查看差异
```
git diff --ours  //提交结果与我们修改的差异

git diff --theirs -b  //提交结果与他们那边的差异

git diff --base -b    //提交结果在两边的差异 
```
5. 清除
```
git clean -f
```

####检出冲突

```
git checkout --conflict=diff3 hello.rb  //在冲突文件中显示三方修改
```
```
git checkout --ours                    //冲突文件替换为我方的
```
```
git checkout --theirs                  //冲突文件替换为他方的
```
#### 合并日志
```
git log --oneline --left-right HEAD...MERGE_HEAD    //每一个分支的所有独立提交的列表

< f1270f7 update README
< 9af9d3b add a README
< 694971d update phrase to hola world
> e3eb223 add more tests
> 7cff591 add testing script
> c3ffff1 changed text to hello mundo
```
```
git log --oneline --left-right --merge  //查看两个分支中产生冲突的提交

< 694971d update phrase to hola world
> c3ffff1 changed text to hello mundo

```
#### 回退合并
```
git reset --hard HEAD~
```
```
git revert -m 1 HEAD  //由于合并节点有两个父节点，-m  1 需要被保留下来的父节点, -m 2 被合并的分支
```

## 使用Git调试

### 文件标注
```
git blame -L 12,22 Simplegit.rb   //显示文件每行的最近修改提交  -L 指定行号范围
```
```
git blame -C GITPackUpload.m   // -C 分析代码的原始出处
```
### 二分查找

1. 手动方式
```
git bisect start  

git bisect bad    //当前提交存在文件

git bisect good V1.0  //正常状态的开始处

//test, 设置bad或者good

git bisect reset  //检测后重置

```

2. 脚本方式
```
git bisect start HEAD V1.0    //设置有问题区间

git bisect run test-error.sh  //每次检出都会自动执行脚本，在正常的情况下返回 0，在不正常的情况下返回非 0.脚本内可以执行make等测试
```

### 子模块
#### 子模块操作

1. 添加子模块
```
git submodule add  https://github.com/chaconinc/DbConnector  //添加字模块
```
2. 查看项目变革
```
git diff --cached --submodule

diff --git a/.gitmodules b/.gitmodules
new file mode 100644
index 0000000..71fc376
--- /dev/null
+++ b/.gitmodules
@@ -0,0 +1,3 @@
+[submodule "DbConnector"]
+ path = DbConnector
+ url = https://github.com/chaconinc/DbConnector
Submodule DbConnector 0000000...c3f01dc (new submodule)
```
3. 提交增加的子模块
```
git commit -am 'added DbConnector module'

[master fb9093c] added DbConnector module
2 files changed, 4 insertions(+)
create mode 100644 .gitmodules
create mode 160000 DbConnector
```
4. 检出子模块
```
git clone https://github.com/chaconinc/MainProject    MainProject 

cd  MainProject

git submodule init   

git submodule update   //下载代码
```

5. 如果子模块有修改，拉取子模块修改
```
git submodule update --remote DbConnector
```
6. 在子模块中修改

```
//进入子模块

git checkout stable  //检出分支

git submodule update --remote --merge

//修改

git commit
```

7. 在我们改动后,同时上游也有个修改，可以通过rebase合入
```
git submodule update --remote --rebase
```
8. 在主项目发布子模块改动

```

//进入主目录

git push --recurse-submodules=check   //如果子模块有未推送的修改，则push失败

git push --recurse-submodules=on-demand //尝试提交子模块

```

#### 子模块技巧
```
git submodule foreach 'git stash'  //遍历子模块
```

### 二进制打包

1. 打包整个仓库
```
git bundle creat repo.bundle HEAD master    //创建bundle
```
```
git clone repo.bundle repo    //检出

//git clone repo.bundle -b master repo  //创建bundle时未指明HEAD时需要加 -b master支持从哪里检出
```
2. 打包某些提交
```
git bundle create commit.bundle master ^ead459   //^= --not

git bundle  list-head  commit.bundle   //查看

git bundle verify  commit.bundle  //验证，有共同的祖先

git fetch  commit.bundle  master:other-master  //合入到other-master  //获取
```
### 拆分仓库
1. 保存就仓库
```
git branch history sha-1

git remote add project-his ssh://192.168.31.6:/opt/git/project-his.git  //创建旧版本库

git push project-his  history:master    //推送旧版本库
```
2. 创建新仓库
```
echo "get history form ssh://192.168.31.6:/opt/git/project-his.git" | git commit-tree history^{tree}  //基于旧仓库创建新库的初始提交
622e88e9cbfbacfb75b5279245b9fb38dfea10cf

git rebase --onto 622e88e9cbf history^   //将新库变基到新的初始提交上

git remote add project-new ssh://192.168.31.6:/opt/git/project-new.git  //引入远程仓库

git push project-new history:master   //推送到新仓库
```
3。 合并新旧仓库

```
git clone ssh://192.168.31.6:/opt/git/project-new.git

git remote add project-his  ssh://192.168.31.6:/opt/git/project-his.git

git fetch project-his

git replace project-new第一笔提交sha-1   project-old最后一笔提交sha-1
```

## git内部工作原理

### git对象
1. 生成git对象
```
git hash-object -w  test.txt   //存储数据对象,返回hash值

83baae61804e65cc73a7201a7252750c76066a30
```
```
echo 'version 1 ' | git hash-object -w --stdin  // 从stdin读取数据

```
2. 查看git对象
```
git cat-file -p  83baae61804e65cc73a7201a7252750c76066a30   //查看数据对象内容
```
3. 向暂存区添加文件
```
git update-index --add --cacheinfo 100644  83baae61804e65cc73a7201a7252750c76066a30 test.txt  //新增文件增加到index区
```
新增与更新文件
```
git update-index test.txt

git update-index --add new.txt
```
4. 写入树对象
```
git write-tree     //写入树对象,返回hash值

d8329fc1cc938780ffdd9f94e0d364e0ea74f579
```
5. 生成提交对象
```
echo 'first commit' | git commit-tree d8329fc1cc938780  //生成提交,返回提交hash值

fdf4fc3344e67ab068f8368
```
```
git read-tree  --prefix=bak d8329fc1cc938780ffdd9f94e0   //基于树对象创建新目录,放到bak目录下

git write-tree

```
7.  commit形成链表
```
//git cat-file -p master^{tree}  //查看最近一次master分支提交的树对象

echo 'second commit ' | git commit-tree dffdefdfdf -p fdf4fc334   //-p 指明父提交

```
8.  查看提交历史
```
git log --state fdf4fc3  //查看提交
```
### git引用

1.  .git/refs/heads目录保存每个分支的最新hash值
```
git update-ref refs/heads/test   sha-1  //更新或增加test分支引用
```
2. HEAD保存当前使用的是哪一个分支
```
$ cat .git/HEAD

ref: refs/heads/test
```
```
git symbolic-ref  HEAD //查看HEAD值
```
```
git symblioc-ref HEAD refs/heads/master  //更新分支指向
```
3. 标签

```
//轻量级标签
git update-ref refs/tag/v1.0 cac0cab538b970a37ea1e769cbbde60  //生成轻量级标签
```
```
//附注标签

git tag -a v1.1 1a410efbd13591db07496601eb -m "test tag"

```
//附注标签原理
```
$ cat .git/refs/tags/v1.1

*9585191f37f7b0fb9444f35a9bf50de191beadc2*

$ git cat-file -p *9585191f37f7b0fb9444f35a9bf50de191beadc2*

*object 1a410efbd13591db07496601ebc7a059dd55cfe9*

type commit

tag v1.1

tagger Scott Chacon <schacon@gmail.com> Sat May 23 16:48:58 2009 -0700

test tag

```

4.  .git/refs/remotes/origin/master   //远程引用

### 引用规格
引用规格的格式由一个可选的 + 号和紧随其后的 <src>:<dst> 组成，其中 <src> 是一个
模式（pattern），代表远程版本库中的引用； <dst> 是那些远程引用在本地所对应的位置。
```
cat .git/config

[remote "origin"]

url = https://github.com/schacon/simplegit-progit   //远程地址

fetch = +refs/heads/*:refs/remotes/origin/*        //将远程的引用更新到本地， +标识不能快进的情况下也更新引用

```
```
fetch = +refs/heads/master:refs/remotes/origin/master  //只拉取master分支
```
```
fetch = +refs/heads/experiment:refs/remotes/origin/experiment  //也可同时指定多个分支

```
```
git fetch origin master:refs/remotes/origin/mymaster   //将远程分支拉取到本地的origin/mymaster分支

```
```
git push origin master:refs/head/qa/master  //将本地master分支推送到远程的qa/master上

```
```
[remote "origin"]

url = https://github.com/schacon/simplegit-progit

fetch = +refs/heads/*:refs/remotes/origin/*

push = refs/heads/master:refs/heads/qa/master    //默认推送

```

### 数据恢复
```
git reflog   //查询丢失的提交
```
```
git fsck --full  //丢失的提交
```
```
git rev-list --objects --all | grep 82c99a3   //82c99a3提交的文件
```