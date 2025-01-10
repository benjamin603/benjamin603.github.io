---
title: Hexo Deployment!
date: 2025-01-10 13:01:37
tags:
  - Hexo
  - Github
index_img:
banner_img:
sticky:
---

前面文章讲解了如何在本地部署 Hexo，部署成功之后我们需要托管才可以外网访问。

<!--more-->

## Github Pages

首选需要有一个 Github 账号。

### 建立仓库

1. 建立名为 **username.github.io** 的储存库。

2. 将 Hexo 文件夹中的文件 push 到储存库的默认分支。 默认分支通常名为**main**。（旧一点的储存库可能名为**master**）

   {% fold info @blinko %}
   
   ```bash
   git init
   git commit -m "first commit"
   git branch -M main
   git remote add origin git@github.com:username/username.github.io.git
   git push -u origin main
   ```
   
   {% endfold %}



