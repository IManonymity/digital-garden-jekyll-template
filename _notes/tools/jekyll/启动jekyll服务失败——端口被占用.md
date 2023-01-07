---
title: 5. 启动jekyll失败
date: 2022-12-30
tags: jekyll
---

### 问题描述
如图，因为4000端口被占用，无法启动jekyll
![](/assets/images/jekyll端口被占用.png)

### 解决办法
解决办法有两种：
- 更改映射端口：在命令后加"-p 端口号"即可
- 将占用4000端口的服务kill：[ruby - jekyll serve启动报错,error:permission denied -bind(2)](https://segmentfault.com/q/1010000010483290/a-1020000010487387)

以实测第一种方法有效，第二种方法没有使用。