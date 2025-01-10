---
title: Hexo Deployment!
tags:
  - Hexo
  - Github
abbrlink: 77a9ed5e
date: 2025-01-10 13:01:37
index_img: https://s3.xwoniu.com/blog/9f05367481.webp
banner_img:
sticky:
---

前面文章讲解了如何在本地部署 Hexo，部署成功之后我们需要托管才可以外网访问。

<!--more-->

## Github Pages

首选需要有一个 Github 账号。

### 配置 SSH

使用 git 设置 Github 的用户名和邮箱：
```bash
git config --global user.name "GitHub 用户名"    
git config --global user.email "GitHub 邮箱"
```

使命下面命令创建密钥：

```bash
ssh-keygen -t rsa -C "GitHub 邮箱"
```

复制 `id_rsa.pub` 文件中的内容：

![id_rsa.pub](https://s3.xwoniu.com/blog/posts/20250110131820.webp)

**Github** - **settings** - **SSH and GPG keys** - **New SSH key**

![New SSH key](https://s3.xwoniu.com/blog/posts/20250110132000.webp)

使用下面命令检查是否连接成功：

```bash
ssh -T git@github.com
```

![x ssh -T git@github.com](https://s3.xwoniu.com/blog/posts/20250110132315.webp)

### 部署至 Github Pages

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
   
   > 默认情况下 `public/` 不会被上传(也不该被上传)，确保 `.gitignore` 文件中包含一行 `public/`
   
3. 使用 `node --version` 指令检查你电脑上的 Node.js 版本。 记下主要版本（例如，`v20.y.z`）

4. 在储存库中前往 **Settings** > **Pages** > **Source** 。 将 source 更改为 **GitHub Actions**，然后保存
   ![GitHub Actions](https://s3.xwoniu.com/blog/posts/20250110132648.webp)

5. 在储存库中建立 `.github/workflows/pages.yml`，并填入以下内容 (将 `20` 替换为上个步骤中记下的版本)

   > [**pages.yml**](https://github.com/benjamin603/benjamin603.github.io/blob/main/.github/workflows/pages.yml)

6. 部署完成后，前往 *username*.github.io 查看网页。

