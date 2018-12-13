# repo工作原理

/bin/repo : python脚本负责执行repo命令，通过init命令下载repo仓和manifest仓

./repo/repo : 一个git仓，包含repo使用的各种命令集和操作方法

./repo/manifest : 一个git仓，包含很多xml配置文件，xml文件指明代码树包含的project集合

# manifest文件

> &lt;?xml version="1.0" encoding="UTF-8"?&gt;

 &lt;manifest&gt;

    &lt;remote  name="aosp"

             fetch=".."

             review="https://android-review.googlesource.com/" /&gt;

    &lt;default revision="master"

             remote="aosp"

             sync-j="4" /&gt;

    &lt;project path="build" name="platform/build" groups="pdk,tradefed" &gt;

	        &lt;copyfile src="core/root.mk" dest="Makefile" /&gt;

    &lt;/project>

    &lt;project path="abi/cpp" name="platform/abi/cpp" groups="pdk" /&gt;

 &lt;/manifest&gt;

*remote* : 描述了远程仓库的基本信息。

name描述的是一个远程仓库的名称;

fetch用作项目名称的前缘;

review描述的是用作code review的server地址

*default* : default标签的定义的属性，将作为<project>标签的默认属性，在<project>标签中，也可以重写这些属性

revision表示当前的版本，也就是我们俗称的分支;

remote描述的是默认使用的远程仓库名称，即<remote>标签中name的属性值

*project* : 每一个repo管理的git库

path描述的是项目相对于远程仓库URL的路径，同时将作为对应的git库在本地代码的路径;

name用于定义项目名称，命名方式采用的是整个项目URL的相对地址.譬如，项目的URL为https://example.com/，命名为platform/build的git库，访问的URL就是https://example.com/platform/build

# repo命令

## init

创建仓库

repo init -u <URL> -m <MANIFIST> -b <BRANCH> --repo-url <REPO URL> --no-repo-verify

-u : 指定manifest仓获取地址

-m : 指定manifest仓中使用的manifest文件

-b ：指定使用manifest仓检出的分支

--repo-url : 指定repo仓的获取地址

--no-repo-verify : 不检验下载的代码

--reference : 指定参考工程，加速代码下载

## sync

repo sync [project_list]

下载远程代码

-j<n> : 开启多线程同步

-c, –current-branch : 只同步manifest中指定的分支而不是全部分支

-d, –detach : 同步代码时不与当前分支代码合并

-f, –force-broken ：某个库失败时继续同步其他库

–no-clone-bundle : 不使用git bundle初始化git库,而是直接从服务器下载git库

--no-tags : 不下载tag标签

## upload

repo upload [project_list]

上传代码进行审核

**Change-ID** 针对每个review任务都生成一个Change-ID,多个Commit-ID(git commit --amend)可以对应同一个Change-ID

## download

repo download <TARGET> <CHANGE>

下载gerrit上的改动

TARGET : 指的是下载的project， eg frameworks/base

CHANGE : 指定要下载的改动内容,不是Commit-ID也不是Change-ID而是像https://example.com/#/c/23823/中的数字23823 

## forall

repo forall [project_list] -p -c <COMMOND>

遍历指定的project执行指定的命令

-p : 输出结果中打印project名称

-c : 指定执行的命令

## prune

repo prune [<project_list>]

删除指定的project中已经合并的分支

## start

repo start <BRANCH_NAME> [<project_list>]

repo start -all master

为指定的project创建分支

-all : 为所有的project都创建分支

## status

repo status [<project_list>]

查看project状态

# 使用场景

## 新建代码树流程

repo init ... ...

repo sync -c --no-tags -j4

repo start --all master

edit code

repo upload

## 快速下载代码

repo init --reference=~/android-exsit  -u xxx -m xxx -b xxx --repo-url xxxx 

repo sync 


