---
---

### 目的
连接本地文件夹与远程仓库

### 步骤
首先查看本地文件夹是否已连接远程仓库
```git
git remote -v
```

没有远程仓库或者连接新的远程仓库
```git
git remote add <name> <address>
```
- name：给远程仓库起一个名字
- address：远程仓库的地址

### 例子
`git remote add gitee-origin git@gitee.com:yunhebuxi/my-blog-obsidian.git`


### 参考
[git 连接远程仓库方法_木偶跳舞的博客-CSDN博客_git连接远程仓库](https://blog.csdn.net/u013372487/article/details/52925960)