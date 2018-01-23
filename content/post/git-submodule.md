---
title: "Git Submodule"
date: 2018-01-23T15:20:12+08:00
draft: false
---

Git 中有 submodule、subtree，submodule 更像是一个组件，它提供好了功能，你不需要修改它。subtree 我暂时没有弄明白，[具体可以查看一下 differences-between-git-submodule-and-subtree](https://stackoverflow.com/questions/31769820/differences-between-git-submodule-and-subtree)。

对一个仓库添加一个 submodule，使用 `git submodule add <repository> [<path>]`，基本上就可以了，
比如说对一个 hugo 站点添加主题，就可以使用 git submodule。

clone 带有 submodule 的仓库，需要在 clone 时添加 `--recursive` 标志，比如 `git clone https://github.com/aikiframework/json.git --recursive`，如果忘记了，也可以在使用 `git submodule update --init` 补上没有初始化的 submodule。