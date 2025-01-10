---
title: hello blinko！
tags: blink
categories: 折腾记录
abbrlink: e4b83efd
date: 2025-01-10 11:01:10
index_img: https://s3.xwoniu.com/blog/posts/3f2a1b9c8d.webp
banner_img:
sticky:
---

Memos 的S3储存太拉跨了，用群友的话就是作者的每次更新都是毁灭性的！进而了解到了 [Blinko](https://blinko.mintlify.app/) 。

<!--more-->

> Blinko 是一个**创新的**开源项目，专为想要快速捕捉和组织转瞬即逝的想法的个人而设计。Blinko 允许用户在想法出现的那一刻无缝记下想法，确保不会丢失任何创意火花。

blinko是老外写的一个开源笔记项目，**具体特点如下**：

- AI增强笔记检索
- 数据存储在本地，不容易丢失
- 支持Markdown编辑器和纯文档
- 代码开源可放心使用

![blinko](https://s3.xwoniu.com/blog/posts/3f2a1b9c8d.webp)

Blinko 所有的公开**闪念**和**笔记**全部展示在 share 页面，例如：https://b.xwoniu.com/share

![blinko](https://s3.xwoniu.com/blog/posts/3456789012aB.webp)

## 介绍

区别与 memos，blinko 拥有 blinko（闪念）以及 note（笔记）两种模式，可以互相切换。

{% fold info @blinko %}

- **目的**：专为快速捕获和临时信息而设计
- **主要特点**：
  - [自动存档](https://blinko.mintlify.app/settings/task#2-schedule-archive-blinko)功能
  - 非常适合临时提醒
  - 非常适合短格式内容
- **使用案例**：
  - 每日任务和提醒
  - 快速的想法和想法
  - 临时信息
  - 不需要长期存放的会议记录

{% endfold %}

{% fold info @note %}

- **目的**：为永久保留知识和详细文档而构建
- **主要特点**：
  - 富文本格式
  - 分层组织
  - 永久存储
- **使用案例**：
  - 项目文档
  - 研究结果
  - 学习资料
  - 重要参考文件

{% endfold %}

> **简单总结：**
>
> **闪念**：快速思考、临时信息、自动存档
>
> **笔记**：长篇内容、永久存储、知识库

## 部署

服务器安装了 1Panel 面板，所以本文来介绍如何通过 1Panel 面板来部署 Blinko。

**容器** - **编排** - **新建编排** - 填入官方安装的 `docker-compose.yml` 内容：

{% fold info @docker-compose.yml %}
```yaml
  networks:
    blinko-network:
      driver: bridge

  services:
    blinko-website:
      image: blinkospace/blinko:latest
      container_name: blinko-website
      environment:
        NODE_ENV: production
        # NEXTAUTH_URL: http://localhost:1111
        # NEXT_PUBLIC_BASE_URL: http://localhost:1111
        NEXTAUTH_SECRET: my_ultra_secure_nextauth_secret
        DATABASE_URL: postgresql://postgres:mysecretpassword@postgres:5432/postgres
      depends_on:
        postgres:
          condition: service_healthy
      # Make sure you have enough permissions.
      # volumes:
        # - ~/your-name/.blinko:/app/.blinko 
      restart: always
      logging:
        options:
          max-size: "10m"
          max-file: "3"
      ports:
        - 1111:1111
      healthcheck:
        test: ["CMD", "curl", "-f", "http://blinko-website:1111/"]
        interval: 30s 
        timeout: 10s   
        retries: 5     
        start_period: 30s 
      networks:
        - blinko-network

    postgres:
      image: postgres:14
      container_name: blinko-postgres
      restart: always
      ports:
        - 5435:5432
      environment:
        POSTGRES_DB: postgres
        POSTGRES_USER: postgres
        POSTGRES_PASSWORD: mysecretpassword
        TZ: Asia/Shanghai
      # Persisting container data
      # Make sure you have enough permissions.
      # volumes:
        # - ~/your-name/.db:/var/lib/postgresql/data
      healthcheck:
        test:
          ["CMD", "pg_isready", "-U", "postgres", "-d", "postgres"]
        interval: 5s
        timeout: 10s
        retries: 5
      networks:
        - blinko-network

```

{% endfold %}

<p class="note note-warning">
<b>注意：</b> 修改掉第11、12行的注释
 </p>

![20250110110945](https://s3.xwoniu.com/blog/posts/20250110110945.webp)

点击确定，启动容器！

## 导入

blinko 支持从 memos 导入数据，这就很方便了。

![image-20250110111725570](https://s3.xwoniu.com/blog/posts/image-20250110111725570.webp)

从本地导入前请把 **存储** 改为本地。

![image-20250110111841368](https://s3.xwoniu.com/blog/posts/image-20250110111841368.webp)

## 参阅

- [Blinko Doc](https://blinko.mintlify.app/introduction)
- https://github.com/blinko-space/blinko
