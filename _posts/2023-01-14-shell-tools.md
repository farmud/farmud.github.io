---
title: Shell工具和脚本
date: 2023-01-14 12:04:00 +0800
categories: [小知识]
tags: [Linux]
pin: false
toc: true
typora-root-url: ../../farmud.github.io
---

# Shell tools

记录一些常见的操作以及shell工具。

## 课程笔记

#### 一些命令

> 一个脚本函数：
>
> ```bash
> mcd(){
> mkdir -p "$1"
> cd "$1"
> }
> ```
>
> 编辑完成后重命名为`mcd.sh` ，运行
>
> ```bash
> source mcd.sh
> ```
>
> 在shell中加载脚本并且执行，之后就可以运行
>
> ```bash
> farmud@farmud-virtual-machine:~/tmp$ mcd hehe
> farmud@farmud-virtual-machine:~/tmp/hehe$
> ```
>
> 创建了名为`hehe`的文件夹，并且进入了该文件夹。
>
> ---
>
> 其他的变量：
>
> `$0` 脚本名
>
> `$1`到`$9` 脚本的参数
>
> `$@` 所有参数
>
> `$#` 参数个数
>
> `$?`  前一个命令的返回值。这里的返回值类似于c语言中return 的返回值，0代表程序正常运行并推出，非0值表示程序不正常结束运行。
>
> `$$` 当前脚本的进程识别码（pid）
>
> `!!` 完整的上一条指令，包括参数。适用于输入一条指令后，提示权限不够时，输入`sudo !!` 即可执行上一条指令
>
> `$_` 上一条命令的最后一个参数。也可以通过`esc`+ `.` 输入

#### 替换

> 当通过`$(CMD)`的方式执行命令时，shell会先执行`CMD`的内容，然后用输出的结果替换掉`$(CMD)`。例如，如果执行 `for file in $(ls)` ，shell首先将调用`ls` ，然后遍历得到的这些返回值。
>
> 还有一种方式为**进程替换**，`<$(CMD)` 会先执行`CMD`的内容，然后将结果输入到一个临时文件中，并将`<$(CMD)`替换成临时文件的文件名。例如，`diff <(ls foo) <(ls bar)` 会显示文件夹 `foo` 和 `bar` 中文件的区别。

#### 通配

>`?`统配一个字符，`*` 统配任意数量的字符。
>
>`{}` 自动展开：
>
>```bash
>convert image.{png,jpg}
># 会展开为
>convert image.png image.jpg
>```
>
>```bash
># 下面命令会创建foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h这些文件
>touch {foo,bar}/{a..h}
>```

#### `shebang`的使用

> 脚本不一定只有用`bash`写的才能在终端调用，比如`python`脚本也可以使用（如在区块链课程中使用的bootstrap.sh脚本）。此时在脚本头将会用到
>
> ```bash
> #!/usr/local/bin/python
> ```
>
> 其中`#!`叫做shebang，通过这一行内核知道用`python`解释器而不是`shell`命令去解释本脚本。
>
> 而目录中`python`脚本的位置在每台主机上未必完全一样，此时就需要用到`env`命令。他会利用环境变量中的程序解释脚本。例如，使用了`env`的shebang看上去时这样的`#!/usr/bin/env python`。

## shell工具

#### `tldr`

> 获得相关指令的信息，通常情况下可以使用`man` 指令。但`man`指令给出的信息有时过于详实，`tldr`是不错的替代品。通过`tldr CMD` 可以获得相关命令的具体解释以及用法。

#### `find`  

> `find`指令可以查找具体文件的路径。有更简单的指令`fd`以及`rg`，要自己手动安装。

## 查找shell命令

#### `history`

> `history`命令支持查找所有历史命令。可以利用管道将输出结果传递给 `grep` 进行模式搜索。 `history | grep find` 会打印包含find子串的命令。可以使用 `Ctrl+R` 对命令历史记录进行回溯搜索。敲 `Ctrl+R` 后可以输入子串来进行匹配，查找历史命令行。使用方向键上或下可以在历史命令中切换。

#### `tree`

> 以树的形式显示文件。
