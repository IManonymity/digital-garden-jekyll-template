---
title: docker使用
date: 2022-12-30
tags: docker
---

### 资源介绍

首先介绍docker的相关资源，使用docker查询下述两个网址即可：
- [前言 - Docker — 从入门到实践 (gitbook.io)](https://yeasy.gitbook.io/docker_practice/)
- [Docker Documentation](https://docs.docker.com/)

在第一个网址中：
1. 前六章为基础内容，供用户理解 Docker 的基本概念和操作；
2. 7 ~ 9 章介绍包括数据管理、网络等高级操作；
3. 第 10 ~ 12 章介绍了容器生态中的几个核心项目；
4. 13、14 章讨论了关于 Docker 安全和实现技术等高级话题。

在第二个网址中，官方网址提供了Docker的使用文档，不懂的命令都可以在里面查。

下面的网址看起来资源很丰富，留存一下：
[Docker+VSCode配置属于自己的炼丹炉](https://zhuanlan.zhihu.com/p/102385239)

### Docker常用场景和命令

**启动Docker容器的几种方式：**

- CMD命令行启动
- Docker Desktop启动
- Vscode的Docker插件启动

**启动Docker容器的常用命令:**

- 交互式启动：`docker -it container_name bash`
- 仅允许命令：`docker container_name command`
- 启动停止允许的容器：`docker exec -it container_id`
- 保存容器的改变：`docker commit container_name`

