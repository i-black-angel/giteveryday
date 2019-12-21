# gitignore 忽略特定文件

## 概述

当你在 Linux 环境进行 C++ 开发的时候，每次编译总会产生大量的目标文件，此时使用 `git status` 查看总会提示 `Untracked files`，但这些目标文件又不需要加入到仓库进行管理，所以为了更准确地管理源码文件，并获得更简洁清晰的改动提示。你可以在项目根目录添加一个 `.gitignore` 文件，并将需要忽略的文件写到该文件中去，Git 将自动忽略这些特定文件。

比如一个典型的 C++ `.gitignore` 文件类似这样子：

```bash
# Compiled object files
*.o
*.obj
```

此时 Git 将忽略所有以 `.o` 结尾或者 `.obj` 结尾的编译目标文件。

当然我不建议你从头开始编写自己的 `.gitignore` 文件，因为 [github](https://github.com/github/gitignore) 网站已经为我们提供了各种配置文件，你可以 `git clone` 下来也可以直接在线浏览：[https://github.com/github/gitignore](https://github.com/github/gitignore)，根据自己的需求进行组合即可。比如你可以将 [C.gitignore](https://github.com/github/gitignore/blob/master/C.gitignore) 与 [C++.gitignore](https://github.com/github/gitignore/blob/master/C%2B%2B.gitignore) 组合成一个 `.gitignore` 来满足项目中既有 C 代码也有 C++ 代码的情况。

## 用法例子

还是以 [C.gitignore](https://github.com/github/gitignore/blob/master/C.gitignore) 为例，讲解一下 `.gitignore` 的用法与编写规则：

```bash
# Prerequisites
*.d

```

1. 以 `#` 开头的行代表注释；
2. 匹配当前目录与子目录下所有以 `.d` 结尾的文件或者文件夹；比如它将匹配 `foo.d`，`bar/foo.d` 文件或 `path.d/`，`bar/path.d/` 文件夹；
3. 空行表示不匹配任何文件，所以空行可以用于作分隔行提高可读性；

```bash
*.dSYM/
*.mod*
modules.order
Module.symvers
Mkfile.old
dkms.conf
```

1. 如果某一行是以右斜杠结尾，它只匹配文件夹；换言之，这一行代表的意思是匹配当前目录与子目录下所有以 `.dSYM/` 结尾的文件夹，但不匹配以 `.dSYM` 结尾的普通文件或软链接符号；比如它只匹配 `foo.dSYM/`，`bar/foo.dSYM/` 文件夹；
2. 匹配当前目录与子目录下所有包含 `.mod` 的文件或者文件夹；比如它匹配 `.mod`，`foo.mod`，`foo.module`，`foo.mod.d` 等；
3. 匹配当前目录与子目录下具体名称的 `modules.order` 文件或文件夹；

接下来我们以 [Autotools.gitignore](https://github.com/github/gitignore/blob/master/Autotools.gitignore) 为例，重点看看右斜杠 `/` 在 `.gitignore` 的匹配规则：

```bash
/autoscan.log
m4/libtool.m4
```

## 总结
