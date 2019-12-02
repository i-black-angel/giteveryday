# 每天 git

## 概述

* 独立开发者（脱机）
* 独立开发者（联机）

## 独立开发者（脱机）

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

---

## Git 配置

Git 的配置项分为三个级别：--system, --global, --local。

级别 | 参数  | 文件
-|-|-
系统 | --system | /etc/gitconfig
用户 | --global | ~/.gitconfig 或 ~/.config/git/config
仓库 | --local | .git/config

使用 --edit 参数可以打开一个编辑器修改 Git 的配置文件
编辑 Git 的系统配置文件
git config --system --edit
编辑 Git 的用户级别配置文件
git config --global --edit
编辑当前本地仓库配置文件
git config --edit，因为 Git 的默认级别就 --local

查看 Git 配置可以使用 --list 参数，
git config --list 列出当前生效的配置项，
使用 git config --system --list 列出 /etc/gitconfig 文件中所配置的内容项，
使用 git config --global --list 列出 ~/.gitconfig 或 ~/.config/git/config 文件中所配置的内容项，
使用 git config --local --list 列出本地仓库 .git/config 文件中所配置的内容项

> Git 的配置文件都是普通文本文件，所以你可以使用普通文本编辑器对配置文件进行修改或新增配置项，这会比运行 `git config` 命令容易得多。
