---
title: SSH key (win)
date: 2017-05-05 14:21:40
tags:
---

## window系统

```
//运行git Bash客户端
$ cd ~/.ssh

//查看目录文件
$ ls

//创建一个SSH key
$ ssh-keygen -t rsa -C "your_email@example.com"

//拷贝 id_rsa.pub 文件的内容，你可以用编辑器打开文件复制，也可以用git命令复制该文件的内容
$ clip < ~/.ssh/id_rsa.pub

//测试一下该SSH key
$ ssh -T git@github.com
```

