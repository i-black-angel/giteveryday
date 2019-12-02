# Git 配置

## 配置文件

也许当初你匆匆而过，早已经忘记了在何时何地配置过你的用户名和邮箱地址，但这却是使用 git 最初的一件事，形如：

```shell
$ git config --global user.name "Your Name"
$ git config --global user.email "youremail@address.com"
```

初次遇见两段如此长的命令行，我敢打赌你也是像我一样记不住的。接下来我们通过下面的学习，我相信你会慢慢了解到它的简单以及有趣之处。

首先，Git 会读取一系列的配置文件来配置它的行为。第一个读取的文件是系统级别的 `/etc/gitconfig`，配置文件中的内容会作用于系统当中每一个用户以及他们所有的 git 仓库。你可以通过给 `git config` 命令带上 `--system` 参数读写该配置文件，默认情况下，该文件不存在，且必须有 root 权限才能操作。

第二个读取的配置文件是用户级别的 `~/.gitconfig` （或者 `~/.config/git/config`），配置文件中的内容仅作用于当前用户。你可以通过给 `git config` 命令带上 `--global` 参数读写该配置文件。如文章开头例子的设定便会写入该配置文件：

```shell
[user]
    name = Your Name
    email = youremail@address.com
```

在这里你可能会有疑问，那什么时候 Git 读写 `~/.config/git/config` 配置文件呢？[官方文档](https://git-scm.com/docs/git-config)给出的解释是：仅当 `~/.gitconfig` 不存在，且 `~/.config/git/config` 存在，它才会生效。

最后一个读取的配置文件是当前 Git 目录下的 `.git/config`，配置文件中的内容仅作用于当前 Git 仓库，你可以通过给 `git config` 命令带上 `--local` 参数读写该配置文件，如果你执行命令时不指定任何级别，那么默认级别就是它。

这里面的每一个级别（system，global，local）都会重写上一个级别的配置。如果 `/etc/gitconfig` 当中配置了 `core.editor` 为 `emacs`，而 `~/.gitconfig` 中配置的 `core.editor` 是 `vi`，则最终生效的是 `~/.gitconfig` 中的配置 `vi`，以此类推。

下表总结了以上三个级别各自的命令参数及配置文件：
级别 | 参数  | 文件
-|-|-
系统 | `--system` | `/etc/gitconfig`
用户 | `--global` | `~/.gitconfig` 或 `~/.config/git/config`
仓库 | `--local` | `.git/config`

> Git 的配置文件都是普通文本文件，所以你可以使用普通文本编辑器对配置文件进行修改或新增配置项，这会比运行 `git config` 命令容易得多。

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