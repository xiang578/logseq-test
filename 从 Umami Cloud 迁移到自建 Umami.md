---
tags:
- docker
- umami
public: true
permalink: note/umami-docker
categories: 随手记
date:
- 2023/05/07
title: 从 Umami Cloud 迁移到自建 Umami
updated: 2024-10-05
toc: true
mathjax: true
---

Umami 是自己从今年年初开始使用网站统计工具，和 Google Analytics 相比，Umami 更加轻量和美观。根据 [P.J. Wu 吳秉儒](https://twitter.com/WuPingJu) 在 [博客文章](https://pinchlime.com/blog/started-using-umami-cloud/) 中介绍，一直通过 Umami Cloud 免费试用。

5 月 5 日突然收到官方邮件，Umami Cloud 结束 Beta 测试以及公布 Pricing，基础 Hobby Plan(Free) 支持 3 个网站/保存 6 个月内统计数据/10k以内请求量，下一档 Basic 直接是 9 刀一个月。由于免费计划保留数据时间太短，收费计划价格太贵，开始考虑从 Umami Cloud 迁移。

<!--more-->

使用 Umami Cloud 差不多 5 月时间，本博客统计到 1.26k 浏览量，从来源域名分析超过一半以上访问都是自己贡献的。毕竟之前在 v2ex 看过网友锐评“大部分个人网站一天就 3 个访客，一个是自己家中电脑，一个是自己公司电脑，最后一个是自己手机”。

![](https://media.xiang578.com/202305071614198-blog.png)

## 使用 Docker 自建 Umami

  + 自建 Umami 有很多方式，比如 Pseudoyu 写过 [从零开始搭建一个免费的个人博客数据统计系统（umami + Vercel + Heroku）](https://www.pseudoyu.com/zh/2022/05/21/free_blog_analysis_using_umami_vercel_and_heroku/)，由于自己不太再想依赖其他“免费”服务，直接选择在服务器使用 Docker Compose 一步安装 Umami。

  + 官方在 [umami/docker-compose.yml at master · umami-software/umami · GitHub](https://github.com/umami-software/umami/blob/master/docker-compose.yml) 提供 docker-compose 文件。复制到服务器，保存成 `docker-compose.yml`，然后 `docker-compose up -d` 启动容器。

```yml
---
version: '3'
services:
  umami:
    image: ghcr.io/umami-software/umami:postgresql-latest
    ports:
      - "3000:3000"
    environment:
      DATABASE_URL: postgresql://umami:umami@db:5432/umami
      DATABASE_TYPE: postgresql
      APP_SECRET: replace-me-with-a-random-string
    depends_on:
      - db
    restart: always
  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: umami
      POSTGRES_USER: umami
      POSTGRES_PASSWORD: umami
    volumes:
      - ./sql/schema.postgresql.sql:/docker-entrypoint-initdb.d/schema.postgresql.sql:ro
      - umami-db-data:/var/lib/postgresql/data
    restart: always
volumes:
  umami-db-data:
```

  + 根据 `docker-compose.yml` 中的设置，自建 umami 端口是 3000，所以可以直接访问 `ip:3000`。Umami 默认账户是 admin，密码是  umami。对于自建服务，一般出于安全考虑都不太建议通过 ip + 端口访问，加上也不太熟悉通过 nginx 配置反向代理，最终通过 [[Cloudflare Zero Trust]] 给端口绑定一个二级域名。

  + 博客相关访问数据可以在 [算法花园 Umami 统计](https://umami.xiang5.top/share/xnuNULQGsOZCYkuK/blog) 查看。

## 导入 Umami Cloud 数据

  + 首先，从 Umami Cloud 导出数据。从下图位置点击 Export 后，会收到一封邮件，然后访问邮件中链接，浏览器会自动下载一个 `csv` 文件。

![](https://media.xiang578.com/202305071605375-umami-cloud-export-data.png)

  + 下载的 `csv` 文件没有标题栏，但是根据文件内数据形式猜测，每一行可能对应一条站点访问记录。

```csv
"7e782528-455f-4f0a-acc5-01ec7ed759ff","24876f1d-7941-5c58-a549-737ebe7515b1","40bc9a7c-a2dc-4e6a-b126-c26313d4d66f","blog.xiang578.com","edge-chromium","Mac OS","desktop","2560x1440","zh-CN","HK","","","","/movie/age-of-dynamic.html","","/travel/san-feng-huan-chuan.html","","blog.xiang578.com","@激流时代 - 算法花园",1,"","2023-05-07 07:03:00"
"7e782528-455f-4f0a-acc5-01ec7ed759ff","2ffcc2a9-670c-5454-8913-0e6ad2a814a9","97b49b96-1f25-40a2-8465-565f2d1f3642","blog.xiang578.com","chrome","Mac OS","desktop","1920x1080","zh-CN","HK","HK-HCW","","Central","/post/are-transformers-effective-for-time-series-forecasting.html","","/","","google.com.hk","【时间序列预测】Are Transformers Effective for Time Series Forecasting? - 算法花园",1,"","2023-05-03 07:12:35"
"7e782528-455f-4f0a-acc5-01ec7ed759ff","ed67da59-da08-5525-9be2-cd2035f7fc95","49891f43-46db-4ec4-a412-b68eaf136e8e","blog.xiang578.com","chrome","Windows 10","laptop","1536x864","zh-CN","HK","HK-HCW","","Central","/post/reinforce-learnning-basic.html","","/","","google.com.hk","李宏毅强化学习课程笔记 PG PPO Q-Learing - 算法花园",1,"","2023-05-03 11:35:33
```

  + 目前（5.7）没有在网上找到相关导入数据的教程，已经发邮件给官方求助，等收到回复后再来更新。

## Umami Docker 数据自动备份

  + 保存 postgres 中数据就可以，暂时还没有时间研究，等有空再回来更新。

## 参考

  + [Umami Docker 部署及优化 - 大大的小蜗牛 (eallion.com)](https://eallion.com/umami/)
