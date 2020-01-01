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

克隆远程 gitignore 仓库：

```bash
git clone https://github.com/github/gitignore
```

## 用法例子

还是以 [C.gitignore](https://github.com/github/gitignore/blob/master/C.gitignore) 为例，讲解一下 `.gitignore` 的用法与编写规则：

```bash
# Prerequisites
*.d

```

1. 以 `#` 开头的行代表注释；
2. 匹配当前目录与子目录下所有以 `.d` 结尾的文件或者文件夹；比如它将匹配 `foo.d`，`bar/foo.d` 文件或 `path.d/`，`bar/path.d/` 文件夹；
3. 空行表示不匹配任何文件，所以空行可用作分隔行提高可读性。

```bash
*.dSYM/
*.mod*
modules.order
Module.symvers
Mkfile.old
dkms.conf
```

1. 如果某一行是以右斜杠结尾，它将只匹配文件夹；换言之，`*.dSYM/` 代表的意思是匹配当前目录与子目录下所有以 `.dSYM/` 结尾的文件夹，但不匹配以 `.dSYM` 结尾的普通文件或软链接符号；比如它只匹配 `foo.dSYM/`，`bar/foo.dSYM/` 文件夹；
2. 匹配当前目录与子目录下所有包含 `.mod` 的文件或者文件夹；比如它匹配 `.mod`，`foo.mod`，`foo.module`，`foo.mod.d` 等；
3. 匹配当前目录与子目录下具体名称的 `modules.order` 文件或文件夹。

接下来我们以 [Autotools.gitignore](https://github.com/github/gitignore/blob/master/Autotools.gitignore) 为例，重点看看右斜杠 `"/"` 在 `.gitignore` 的匹配规则：

```bash
Makefile.in
/autoscan.log
m4/libtool.m4
```

1. 不带右斜杠，匹配当前目录与子目录下所有的 `Makefile.in` 文件或文件夹；
2. 以右斜杠开头，将仅匹配当前目录下的 `autoscan.log`，但不匹配 `foo/autoscan.log` 文件；
3. 模式当中包含右斜杠 `("/")` 的话，将只匹配当前目录下的 `m4/libtool.m4`，但不匹配 `foo/m4/libtool.m4`；
4. 归纳为，如果模式当中包含右斜杠，将只匹配当前目录下的文件或文件夹；因此 `m4/libtool.m4` 也等同于 `/m4/libtool.m4` 的写法。

我们再以 [CakePHP.gitignore](https://github.com/github/gitignore/blob/master/CakePHP.gitignore) 为例，讲解一下感叹号 `"!"` 的用法：

```bash
/tmp/cache/models/*
!/tmp/cache/models/empty
```

1. 忽略 `/tmp/cache/models` 文件夹下的所有文件；
2. 但不忽略 `/tmp/cache/models/empty` 文件；
3. 以 `("!")` 开头的行将不会被忽略，一般用于希望忽略整个文件夹的内容，但仍有部分文件或文件夹需要更新到仓库中的情况。
4. 使用 `"\"` 能够对 `"!"` 进行转义，如 `\!important.txt` 匹配的是文件名以 `"!"` 开头的 `!important` 文件。

接下来我们看看 [NetBeans.gitignore](https://github.com/github/gitignore/blob/master/Global/NetBeans.gitignore) 与 [JetBrains.gitignore](https://github.com/github/gitignore/blob/master/Global/JetBrains.gitignore) 关于 `("**")` 双星号的用法：

```bash
**/nbproject/private/
.idea/**/workspace.xml
```

1. 以 `"**"` 加上 `"/"` 开头匹配所有的文件夹；
2. 右斜杠带上 `"**"` 后面再带一个右斜杠表示匹配 0 个或任意多个文件夹；`.idea/**/workspace.xml` 匹配 `.idea/workspace.xml`，`.idea/foo/worksapce.xml`或者 `.idea/foo/bar/workspace.xml`；

最后我们看看一些中括号表达式的使用例子，可以参考 [Actionscript.gitignore](https://github.com/github/gitignore/blob/master/Actionscript.gitignore)，[Vim.gitignore](https://github.com/github/gitignore/blob/master/Global/Vim.gitignore) 或 [TeX.gitignore](https://github.com/github/gitignore/blob/master/TeX.gitignore) 等：

```bash
[Bb]in/
*.py[cod]
[._]sw[a-p]
*.eledsec[1-9][0-9]
```

1. `[]` 是定义匹配的字符范围。比如 `[a-zA-Z0-9]` 表示相应位置的字符要匹配英文字符和数字；`[Bb]in/` 匹配 `Bin/` 与 `bin/` 文件夹；
2. 匹配 `*.pyc`，`*.pyo` 及 `*.pyd`；
3. 匹配以 `.` 或 `_` 开头，后跟 `swa`，`swb`，`swc...swp` 的字符；
4. 匹配最后两位从 `10` 开始直到 `99` 的数字。

## 编写规则

- 空行不匹配任何文件；
- 以 `"#"` 开头的行代表注释；
- 以 `"!"` 开头的行不被忽略；
- 反斜杠 `"\"` 代表转义；
- 右斜杠 `"/"` 结尾仅匹配文件夹；
- 以右斜杠 `"/"` 开头或包含在模式中，仅匹配当前文件夹；
- 星号 `"*"` 匹配任何字符；
- 两个星号 `"**"` 匹配 0 个或任意多个文件夹；
- 中括号 `"[]"` 表达式定义匹配的字符范围。

## 作用文件

在 gitignore 文件中的每一行指定了一个模式，当决定是否忽略一个路径的时候，Git 通常会从多个源检查 gitignore 文件。

- `.gitignore`
- `.git/info/exclude`
- `~/.config/git/ignore`，`core.excludesFile`

## 参考文档

[1] [Pro Git](https://git-scm.com/book/en/v2)  
[2] [gitignore 官方文档](https://git-scm.com/docs/gitignore)  
[3] [Git教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208)  
[4] `git help ignore`  
[5] `man gitignore`
