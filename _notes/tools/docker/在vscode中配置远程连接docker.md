---
title: vscode中配置docker插件
date: 2022-12-30
tags: docker
---

使用docker的终端多有不便，于是便想到了使用vscode远程连接docker。

### 先决条件

- 在vscode中安装docker插件、dev container插件
- 安装Remote Development插件

### 连接本地docker

步骤如下：
- 首先在本地运行docker，然后打开vscode，进入docker插件面板
- 在docker插件面板，运行容器
- 然后右键容器，点击attach to vscode即可

### 将本地文件运行在docker中

[Developing inside a Container using Visual Studio Code Remote Development](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container)

### 将一个git仓库运行在docker中

[Developing inside a Container using Visual Studio Code Remote Development](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume)