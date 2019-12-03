# Git 配置

## 配置文件

也许当初你匆匆而过，早已经忘记了在何时何地配置过你的用户名和邮箱地址，但这却是使用 git 最初的一件事，形如：

```shell
git config --global user.name "Your Name"
git config --global user.email "youremail@address.com"
```

初次遇见两段如此长的命令行，我敢打赌你也是像我一样记不住的。接下来我们通过下面的学习，我相信你会慢慢了解到它的简单以及有趣之处。

首先，Git 会读取一系列的配置文件来配置它的行为。第一个读取的文件是系统级别的 `/etc/gitconfig`，配置文件中的内容会作用于系统当中每一个用户以及他们所有的 git 仓库。你可以通过给 `git config` 命令带上 `--system` 参数读写该配置文件，默认情况下，该文件是不存在的，且必须有 root 权限才能操作。

第二个读取的配置文件是用户级别的 `~/.gitconfig` （或者 `~/.config/git/config`），配置文件中的内容仅作用于当前用户。你可以通过给 `git config` 命令带上 `--global` 参数读写该配置文件。如文章开头例子的设定便会写入该配置文件：

```shell
[user]
    name = Your Name
    email = youremail@address.com
```

在这里你可能会有疑问，那什么时候 Git 才会读写 `~/.config/git/config` 呢？[官方文档](https://git-scm.com/docs/git-config)给出的解释是：仅当 `~/.gitconfig` 不存在，且 `~/.config/git/config` 存在时，它才会生效。

最后一个读取的配置文件是当前 Git 目录下的 `.git/config`，配置文件中的内容仅作用于当前 Git 仓库，你可以通过给 `git config` 命令带上 `--local` 参数读写该配置文件，如果你执行命令时不指定任何级别，那么默认级别就是它。

这里面的每一个级别（system，global，local）都会重写上一个级别的配置。如果 `/etc/gitconfig` 当中配置了 `core.editor` 为 `emacs`，而 `~/.gitconfig` 中配置的 `core.editor` 是 `vi`，则最终生效的是 `~/.gitconfig` 中的配置 `vi`，以此类推。

下表总结了以上三个级别各自的命令参数及配置文件：
级别 | 参数  | 文件
-|-|-
系统 | `--system` | `/etc/gitconfig`
用户 | `--global` | `~/.gitconfig` 或 `~/.config/git/config`
仓库 | `--local` | `.git/config`

> Git 的配置文件都是普通文本文件，所以你可以使用普通文本编辑器对配置文件进行修改，这会比运行 `git config` 命令容易得多。

## 基本配置

Git 提供了大量的配置项供你自定义它的非默认行为，你可以在你喜爱的 Linux 终端上输入 `git config` 之后按两次 `TAB` 键并根据提示输入 `y`，列出所有的配置项。当然了，其中大部分的配置都有其特定的使用场景，本文将只关注 Git 通用的一部分配置，每一个配置项的详细信息及注意事项可以参考：
1. 官方文档：[https://git-scm.com/docs/git-config](https://git-scm.com/docs/git-config)
2. 或者参考本地手册：

    ```shell
    git config --help
    git help config
    ```

3. 又或者使用 `man` 指令进行查阅：

    ```shell
    man git-config
    ```

在前面的内容中我们已经了解了 `user.name` 及 `user.email` 的配置，接下来我们再看几个 Git 的常用配置。

**core.editor**

默认情况下，Git 使用当前系统环境变量（`EDITOR` 或者 `VISUAL`）所定义的编辑器进行编辑，如果环境变量为空，在 Linux 操作系统中还可以使用命令 `update-alternative --config editor` 查看当前系统配置的编辑器，比如：

```shell
$ update-alternative --config editor
There are 5 choices for the alternative editor (providing /usr/bin/editor).

  Selection    Path                Priority   Status
------------------------------------------------------------
* 0            /bin/nano            40        auto mode
  1            /bin/nano            40        manual mode
  2            /usr/bin/code        0         manual mode
  3            /usr/bin/emacs24     0         manual mode
  4            /usr/bin/vim.basic   30        manual mode
  5            /usr/bin/vim.tiny    15        manual mode

Press <enter> to keep the current choice[*], or type selection number:
```

在当前系统配置的默认编辑器为 `/bin/nano`，数字前面带有 **\*** 号的便是。如果你不希望使用系统默认配置，那么你可以使用 `core.editor` 进行配置：

```shell
git config --global core.editor vi
```

>关于 `--global` 所代表的级别及应用范围，上文有详细的解释，如果有疑惑的地方可以参考一下**配置文件**一节内容。

这样的话，不管你当前系统的默认编辑器是什么，Git 都会使用 `vi` 作为编辑器来编辑信息。

**alias.\***

Git 配置中最实用的我认为就是 `alias.*` 了，alias 的中文意思是“别名”，意思是可以使用另一个命名来代替本来的名称，这样你就可以使用一些简写来代替长长的命令行输入了。比如，你可以使用 `git st` 代替 `git status` 命令（正如大多数人正在偷懒的做法一样）：

```shell
git config --global alias.st status
```

好了，此时你在命令行输入 `git st` 试试效果如何：

```shell
git st
```

除了 `git st` 之外，你还可以继续将更多的命令进行简写处理，比如使用 `co` 代替 `checkout`，`ci` 代替 `commit`，`br` 代替 `branch`等：

```shell
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
```

这样你需要拉分支的时候就可以简写为：

```shell
git co -b new_branch
```

更多丰富的别名也可以参考[廖雪峰 Git 教程 -- 配置别名](https://www.liaoxuefeng.com/wiki/896043488029600/898732837407424)一文，文中提供了一些好玩的配置。比如配置了 `unstage` 用来撤销缓冲区的修改，以及 `last` 用于显示最后一次提交的日志：

```shell
git config --global alias.unstage 'reset HEAD'
git config --global alias.last 'log -1'
```

这样当你需要撤销缓冲区的修改的时候就可以直接使用 `git unstage` 来完成了：

```shell
git unstage thread.cpp
```

显示最后一次提交信息也是，只需要使用 `git last` 来完成即可。

**color.ui**

Git 配置中另外一个非常重要的特性是颜色。Git 完全支持彩色终端的输出，能够使用不同颜色的可视化标记来达到快速信息分析的目的。颜色输出可以通过 `color.ui` 的值来进行配置，有三个重要的参数值：

* always
* auto
* never

Git 1.8.4 及以后的版本默认参数是 `auto`，意味着默认已经打开颜色支持；而 Git 1.8.3 或之前的版本如果需要颜色支持的话，需要手动配置 `color.ui` 为 `auto` 或 `true`：

```shell
git config --global color.ui auto
```

## 列出配置信息

在**配置文件**一节中的内容提到，Git 会依次读取三个级别（system，global，local）的配置文件信息，因为配置文件都是普通文本文件，你可以直接使用编辑器打开查看，或者使用 Git 提供的 `--list` 进行查看：

```shell
git config --list
```

当不带级别参数（`--system`，`--global` 或 `--local`）调用时，显示的是当前生效的所有配置参数信息，以 `key=value` 的形式显示，如：

```shell
$ git config --list
alias.st=status
alias.co=checkout
user.name=Your Name
user.email=youremail@address.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
```

当带上级别参数调用时，显示的即是对应级别的配置文件的所有信息：

命令 | 说明
-|-
`git config --system --list` | 显示 `/etc/gitconfig` 文件
`git config --global --list` | 显示 `~/.gitconfig` 或 `~/.config/git/config` 文件
`git config --local --list` | 显示 `.git/config` 文件
`git config --list` | 显示最终生效的配置信息

## 编辑配置信息

因为 Git 的配置文件都是普通文本文件，所以你可以直接使用编辑器（如 `vi`，`emacs`）对配置文件进行操作，同时 Git 也提供了一个快捷的打开配置文件进行编辑的参数 `--edit`，可谓是任君选择：

```shell
git config --system --edit
```

将调用一个编辑器（参考 `core.editor` 内容）打开 `/etc/gitconfig` 配置文件进行编辑。但是必须保证用户对 `/etc/gitconfig` 有写权限，否则可能会在 `vi` 保存时提示：`"/etc/gitconfig" E212: Can't open file for writing` 的错误。

>如果是普通用户执行该语句，需要使用：`sudo git config --system --edit`

```shell
git config --global --edit
```

调用一个编辑器打开 `~/.gitconfig` 或者 `~/.config/git/config` 配置文件进行编辑。

```shell
git config --edit
```

调用一个编辑器打开 `.git/config` 配置文件进行编辑，默认是 `--local` 级别。

命令 | 说明
-|-
`git config --system --edit` | 编辑 `/etc/gitconfig` 文件
`git config --global --edit` | 编辑 `~/.gitconfig` 或 `~/.config/git/config` 文件
`git config --edit` | 编辑 `.git/config` 文件

## 删除配置信息

因为 Git 的配置文件都是普通文本文件，所以你可以直接使用编辑器（如 `vi`，`emacs`）对配置文件进行操作。如果删除不再需要的配置项，只需调用编辑器打开配置文件，将配置项从文件移除，最后保存退出即可。同时你也可以使用 Git 提供的 `--unset` 指令来对配置文件进行操作。

比如，某个月黑风高的夜晚，你通过配置命令 `git config --global core.editor emacs` 给 Git 配置了一个酷炫的编辑器，此时在 `~/.gitconfig` 文件中就会生成一条配置信息：

```shell
[core]
    editor=emacs
```

然后有一天，你突发奇想（这种事你经常干）希望 Git 使用系统默认配置的编辑器时，你可以使用 `--unset` 来完成这事了：

```shell
git config --global --unset core.editor
```

执行完上面的命令之后，本来在 `~/.gitconfig` 文件中的 `editor=emacs` 便会被移除，是的，这与你手动删除的效果是一样的。如果不带级别参数调用，默认是移除 `.git/config` 配置文件中的匹配项。

命令 | 说明
-|-
`git config --system --unset key` | 移除在 `/etc/gitconfig` 中匹配 `key` 的一行
`git config --global --unset key` | 移除在 `~/.gitconfig` 或 `~/.config/git/config` 中匹配 `key` 的一行
`git config --unset key` | 移除在 `.git/config` 中匹配 `key` 的一行

## 参考文档

[1] [Pro Git](https://git-scm.com/book/en/v2)  
[2] [git-config](https://git-scm.com/docs/git-config)  
[3] [Git教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)  
[4] `git config --help`
