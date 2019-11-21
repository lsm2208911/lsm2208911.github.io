---
layout:     post
title:      "Git配置网络代理"
subtitle:   "世界没有难用的工具"
date:       2019-11-21
author:     "无力去闹"
header-img: "img/post-bg-js-version.jpg"
tags:
    - springboot
---
配置 git 代理- 通过 git config 命令：
```
Config file location
    --global              use global config file
    --system              use system config file
    --local               use repository config file
    --worktree            use per-worktree config file
    -f, --file <file>     use given config file
    --blob <blob-id>      read config from given blob object
```
可以看出：
> - '-- global' 允许对当前用户全局的git配置文件进行配置 (~/.gitconfig 文件，属于某个计算机用户)
> - '-- system' 允许对系统全局的配置文件进行配置(/etc/gitconfig 文件，属于计算机) 
> - '-- local' 允许对当前工作目录的git进行配置(位于 clone 仓库下 .git/config)。

上面各种配置应该需要充分考虑含义。
比如，有些是从 github 远程仓库的 clone， 有些是公司内网仓库的 clone，前者需要配置网络代理才能拉取、提交代码，后者不能配置网络代理。

那我们的操作就是只对 github 的 clone 仓库配置：进入 github clone 仓库，运行 `git config --local http.proxy 192.168.4.12:8080`之后就可以看到 .git/config 文件中多了最下面两行:
```
[http]
proxy = 10.xx.xx.xx:8080
```
这也意味着，我们直接按上面改这个配置文件也能达到同样的目的。

原文：[Git 设置网络代理](https://blog.csdn.net/lizhihaoweiwei/article/details/76849755)