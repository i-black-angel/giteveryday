# Git 配置
---
## Git 配置
也许当初你勿勿而过，早已经忘记了在何时何地配置过你的用户名和邮箱地址，但这却是使用 git 最初的一件事，形如：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "youremail@address.com"
```
初次遇见两段如此长的命令行，我敢打赌你也是像我一样记不住的。接下来我们通过学习，我相信你会慢慢了解到它的简单以及有趣之处。

首先，Git 会读取一系列的配置文件来配置它的行为。第一个读取的文件是系统级别的 `/etc/gitconfig`，

/etc/gitconfig
~/.gitconfig 或者 ~/.config/git/config
.git/config

--system, --global, --local(default)
--edit
--list

user.name
user.email
color.ui
core.editor
alias.st
alias.co
alias.br

## 获取帮助信息
git config --help
git help config
man git-config
https://git-scm.com/docs/git-config