# 每天 git

# 概述
* 独立开发者（脱机）
* 独立开发者（联机）

# 独立开发者（脱机）
一个脱机独立开发者不需要与其他人员交换修改补丁，且工作在一个单一的 git 仓库，使用下列命令。
* git init 创建一个新的 git 仓库；
* git log 查看修改日志；
* git checkout 及 git branch 用于转换分去；
* git add 管理标记文件；
* git diff 及 git status 查看你的中途修改；
* git commit 提交修改到当前分支；
* git reset 及 git checkout （带上路径参数）用于回退到某一个版本；
* git merge 合并修改到当前分支；
* git rebase 维护标题分支；
* git tag 打一个标签。

## 例子
使用一个 tar 包作为开始点新建一个 git 仓库。
$ tar -xzvf frotz.tar.gz
$ cd frotz
$ git init
$ git add . (1)
$ git commit -m "import of frotz source tree."
$ git tar v2.43 (2)

1. 在当前目录下添加所有东西
2. 添加一个轻量的，未注释的标签
