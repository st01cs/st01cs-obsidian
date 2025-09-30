---
title: "扩展 git branch 命令 增加分支描述的功能 · Issue #69 · shangwenhe/shangwenhe.github.io"
source: "https://github.com/shangwenhe/shangwenhe.github.io/issues/69"
author:
  - "[[shangwenhe]]"
published: 2025-07-15
created: 2025-09-30
description: "📝 Git 分支描述工具使用指南 🧭 背景说明 目前，Git 本身并没有内置的分支描述功能，开发者通常通过分支名来了解分支的目的，但这种方式不够直观。为了提升分支管理的清晰度和可读性，我在项目中引入了一个名为 .git/branch-notes 的本地文件，用于记录每个 Git 分支的描述信息。这个文件不会影响 Git 的版本控制功能，仅作为开发人员在本地维护分支说明的工具。 通过添加 git branch.note 命令，可以更方便地为当前分支添加描述，提高团队协作效..."
tags:
  - "clippings"
---
**shangwenhe** opened this issue on 2025/7/15

# 📝 Git 分支描述工具使用指南

## 🧭 背景说明

目前，Git 本身并没有内置的分支描述功能，开发者通常通过分支名来了解分支的目的，但这种方式不够直观。为了提升分支管理的清晰度和可读性，我在项目中引入了一个名为 `.git/branch-notes` 的本地文件，用于记录每个 Git 分支的描述信息。这个文件不会影响 Git 的版本控制功能，仅作为开发人员在本地维护分支说明的工具。

通过添加 `git branch.note` 命令，可以更方便地为当前分支添加描述，提高团队协作效率与代码可维护性。该命令对团队成员完全透明、易于使用，是对外展示的入口。

---

## 📌 一、用户应该如何配置

### 1\. 创建 `.git/branch-notes` 文件

在项目根目录下创建一个名为 `.git/branch-notes` 的普通文本文件，用于存储各分支的描述信息：

touch .git/branch-notes

或者你可以直接写入初始内容：

echo "| main | 主分支，用于生产环境代码" \> .git/branch-notes

### 2\. 配置 Git 别名

将以下配置添加到你的 `.gitconfig` 文件中，使 `git branch.note` 命令正常工作：

> ⚠️ 注意：以下命令为 Mac OS 系统的配置文件。

\[alias "branch"\]
  clear \= "!f() { if test -f .git/branch-notes ; then grep -v $(git rev-parse --abbrev-ref HEAD) .git/branch-notes \> .git/branch-notes.tmp && mv .git/branch-notes.tmp .git/branch-notes; fi;}; f"
  add \=  "!f() { if \[\[ \-n $1 \]\]; then echo \\"| $(git rev-parse --abbrev-ref HEAD) | $@ |\\" \>> .git/branch-notes ; fi; }; f"
  show \= "!f() { if test -f .git/branch-notes ; then grep --no-filename $(git rev-parse --abbrev-ref HEAD) .git/branch-notes | awk -F '|' '{print $3}'; else echo 'The file \`.git/branch-notes\` does not exist'; fi; }; f"
  notes \= "!f() { git branch --list | tr -d ' \*' | while read -r name; do if \[\[ \-n $(grep ${name} .git/branch-notes) \]\]; then grep ${name} .git/branch-notes| sed 's/^|\[\[:space:\]\]//g' | awk -F '|' '{print $1 \\"\\\\033\[32m\\" $2 \\"\\\\033\[0m\\" }'; else echo  $name; fi; done; }; f"
  note \=  "!f() { if \[\[ \-n $1 && $1 \= '\--add' && \-n $2 \]\]; then shift; git branch.add $@; elif \[\[ \-n $1 && $1 \= '\--clear' \]\]; then git branch.clear; else git branch.show; fi; }; f"

> ✅ 所有分支描述操作均通过内部命令（如 `branch.add`、`branch.show`）实现，因此你只需配置 `branch.note` 命令即可。

---

## 📌 二、介绍一下 `git branch.note` 应该如何使用

### 1\. 添加分支描述

使用如下命令为当前分支添加描述（支持中文）：

git branch.note --add "用于开发用户登录模块，包含前端和后端接口"

> 💡 运行后，`git branch.note` 会自动将描述写入 `.gitbranch` 文件，格式如下：

```
| <branch-name> | <description> |
```

例如：执行 `git branch.note`

```
用于开发用户登录模块，包含前端和后端接口
```

### 2\. 查看当前分支的描述

直接使用以下命令查看当前分支的说明：

git branch.note

> 📝 此命令会自动读取 `.git/branch-notes` 文件中的内容，并输出当前分支的描述。如果没有设置描述，则会显示空白。

### 3\. 清空当前分支的描述

直接使用以下命令清空当前分支的说明：

git branch.note --clear

当前分支的描述将会被清空 ⚠️ 请谨慎操作

### 4\. 查看所有分支的描述

直接使用以下命令查看当前分支的说明：

git branch.notes

列出所有分支并展示出分支的描述

```
eat/cus-register
feat/data-statistics
feat/oAuth
feat/package-switching 这是项目的描述
feat/replace-get-api-list
feat/stat-maas
feat/super-group
feat/test-template
fix/blog
fix/config-base
fix/huoshan-register
fix/optimization
```

**shangwenhe** commented on 2025/7/16

## 增加 快速创建分支 并 添加分支描述 功能

### filename git-co

> 请将 git-co 文件添加到 $PATH 中；

#!/bin/bash

# git-co - 自定义 Git 插件，用于处理带 -m 参数的 checkout 命令
# 使用方法：git co \[checkout 参数\] -m \[注释内容\]

# 初始化变量
note\_message=""
checkout\_args=()
found\_m=false

# 解析命令行参数
for arg in "$@"; do
    if \[\[ $found\_m \== true \]\]; then
        note\_message="$arg"
        found\_m=false
    elif \[\[ $arg \== "\-m" \]\]; then
        found\_m=true
    else
        checkout\_args+=("$arg")
    fi
done

# 检查是否找到了 -m 参数但没有提供值
if \[\[ $found\_m \== true \]\]; then
    echo "错误：-m 选项需要一个参数值。" \>&2
    exit 1
fi

# 执行 git checkout 命令
git checkout "${checkout\_args\[@\]}"
checkout\_status=$?

# 如果 checkout 成功且有注释内容，则添加分支注释
if \[\[ $checkout\_status \-eq 0 && \-n "$note\_message" \]\]; then
    # 获取当前分支名
    current\_branch=$(git rev-parse --abbrev-ref HEAD)
    if \[\[ \-n "$current\_branch" \]\]; then
        git branch.note --add $note\_message;
    fi
fi

exit $checkout\_status

## 使用方式

如 `git co -b feat/test -m '这是一个分支的描述'`

**shangwenhe** commented on 2025/7/16

## 简写 branch

```
[alias "br"]
  clear = "!f() { git branch.clear }; f"
  add =  "!f() {  git branch.add $*; }; f"
  show = "!f() { git branch.show; }; f"
  notes = "!f() { git branch.notes; }; f"
  note =  "!f() { git branch.note $*; }; f"
```

**sonic0002** commented on 2025/7/18

这个能配置强制需要为新建分支添加描述功能么？  
修改描述的话需要clear再创建？

**lengyijun** commented on 2025/7/18

Do you know `git branch --edit-description`

**lengyijun** commented on 2025/7/18

分支描述 能通过 github 同步吗 ？

**Innnsane** commented on 2025/7/18

> 分支描述 能通过 github 同步吗 ？

.git 文件不加入版本管理，猜测应该是不可以的

**zbuzhi92** commented on 2025/7/19

不能同步的话，就等于就是自己备注给自己看

**shangwenhe** commented on 2025/7/22

> 不能同步的话，就等于就是自己备注给自己看

它只是一个记录文件。当然你可以把它放到项目中，让 git 工具把它管理起来。

**shangwenhe** commented on 2025/7/22

> 这个能配置强制需要为新建分支添加描述功能么？ 修改描述的话需要clear再创建？

你把 上面的 git-co 可执行文件保存到 $PATH 下。

[@sonic0002](https://github.com/sonic0002) 使用 `git co -b feat/new-test  -m '这是一个测试的分支'` 就可以为当前新创建的分支添加描述

**shangwenhe** commented on 2025/7/22

[@zbuzhi92](https://github.com/zbuzhi92) [@Innnsane](https://github.com/Innnsane)

如果想把它放到项目中，可以使用下面这个。但你每次切换分支它会变动。需要把它做为一个项目文件管理起来。

## 将配置文件存放到项目中，文件名 `.git-branch-notes`

\[alias "branch"\]
  clear = "!f() { if test -f .git-branch-notes ; then grep -v $(git rev-parse --abbrev-ref HEAD) .git-branch-notes > .git-branch-notes.tmp && mv .git-branch-notes.tmp .git-branch-notes; fi;}; f"
  add =  "!f() { if \[\[ -n $1 \]\]; then echo \\"| $(git rev-parse --abbrev-ref HEAD) | $@ |\\" >> .git-branch-notes ; fi; }; f"
  show = "!f() { if test -f .git-branch-notes ; then grep --no-filename $(git rev-parse --abbrev-ref HEAD) .git-branch-notes | awk -F '|' '{print $3}'; else echo 'The file \`.git-branch-notes\` does not exist'; fi; }; f"
  notes = "!f() { git branch --list | tr -d ' \*' | while read -r name; do if \[\[ -n $(grep ${name} .git-branch-notes) \]\]; then grep ${name} .git-branch-notes| sed 's/^|\[\[:space:\]\]//g' | awk -F '|' '{print $1 \\"\\\\033\[32m\\" $2 \\"\\\\033\[0m\\" }'; else echo  $name; fi; done; }; f"
  note =  "!f() { if \[\[ -n $1 && $1 = '--add' && -n $2 \]\]; then shift; git branch.add $@; elif \[\[ -n $1 && $1 = '--clear' \]\]; then git branch.clear; else git branch.show; fi; }; f"