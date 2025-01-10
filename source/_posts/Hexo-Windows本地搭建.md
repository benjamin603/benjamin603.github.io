---
title: Windows 本地搭建 Hexo
abbrlink: 924f775e
date: 2024-12-24 11:57:34
tags: Hexo
categories: 折腾记录
index_img: https://s3.xwoniu.com/blog/9f05367481.webp
banner_img:
sticky:
---

本文用来介绍如何在 Windows 本地搭建 Hexo 博客框架！

<!-- more-->

## 准备

- [Node.js](http://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- [Git](http://git-scm.com/)

## 安装 Hexo

按照以下步骤即可在本地部署 Hexo：

```bash
npm install hexo-cli -g
hexo init blog
cd blog
hexo server
```

初始化后，您的项目文件夹将如下所示：

```yaml
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

## 问题

### 解决 npm 安装慢

npm 默认的镜像源是 `https://registry.npmjs.org/`，由于服务器在国外，下载速度较慢。可以通过切换到国内镜像源（如淘宝镜像）来加速。

我们可以采取使用 **国内镜像** 的方法来加速 npm 包的下载。

1. 临时切换镜像源：
   ```bash
   npm install express --registry=https://registry.npmmirror.com
   ```
   
2. 永久切换镜像源：
   ```bash
   npm config set registry https://registry.npmmirror.com
   ```

验证镜像源是否修改成功：

```bash
npm config get registry
```

