# 创建 Git 仓库

## 概述

Git 使用 `git init` 命令创建一个空的仓库，基本上就是在当前目录下创建一个 `.git` 目录，目录下面存储着仓库的各项信息。

在一个已经创建过 Git 仓库的目录下执行 `git init` 命令也是没有问题的，它不会去重写任何已经存在的内容。最主要的原因，在已有的 Git 仓库下执行该命令就是获取新添加的模板。

如果带上路径执行 `git init <path>` 命令，它会在 `<path>` 目录下创建 `.git` 目录，如果该路径不存在，Git 同时也会创建该目录出来。比如命令：

```shell
$ git init /tmp/hello
Initialized empty Git repository in /tmp/hello/.git/
```

将同时创建 `/tmp/hello` 与 `.git` 两个目录，并初始化 Git 仓库。

## 例子

```shell
git init
git add .
git commit -m 'comment'
```

1. 创建一个 `.git` 目录；
2. 将当前路径下的所有文件添加到 Git 仓库的缓存区；
3. 将缓存区的文件提交到 Git 仓库。
