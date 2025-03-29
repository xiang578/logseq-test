---
categories: 随手记
tags:
- webmention
- IndieWeb
date:
- 2023/04/06
public: true
permalink: note/641ea60f-a31e-4979-9327-c50509c146e3
title: Webmention 实现参考
lastMod: 2024-10-05
toc: "true"
---

关于博客内实现 webmention 功能相关文章收集
<!--more-->
## 综合
[IndieWebify.Me - a guide to getting you on the IndieWeb](https://indiewebify.me/) 逐级引导如何使网站符合 IndieWeb 规范
KRISTOF ZERBE 三篇文章详细介绍 hexo 博客如何支持 Webmention。
[Hexo and the IndieWeb - kiko.io](https://kiko.io/post/Hexo-and-the-IndieWeb/) 介绍 `h-card`、`h-entry` 等 html 标签用法。
发送 response 支持的标签
`u-in-replay-to`
`In reply to: <a class="u-in-reply-to" href="https://jacks-blog.com/awesome-work">Jacks Blog: Awesome Work</a>`
`u-link-of`
`Kristof liked <a class="u-like-of" href="https://jacks-blog.com/awesome-work">Jacks Awesome Work at https://jacks-blog.com/awesome-work</a>`
`u-repost-of`
`u-bookmark-of`
[Hexo and the IndieWeb (Sending Webmentions) - kiko.io](https://kiko.io/post/Hexo-and-the-IndieWeb-Sending-Webmentions/) 向被你提及的网站发送 webmention 消息
[webmention.app](https://www.webmention.app/)：~~打开一直显示 404，服务挂了？~~ 评论区 **Mirakelor** 提醒网址必须加上 `www`
解析你博客的 RSS feed，匹配出提及的网址，然后发出 mention
[Hexo and the IndieWeb (Receiving Webmentions) - kiko.io](https://kiko.io/post/Hexo-and-the-IndieWeb-Receiving-Webmentions/) 使用 `webmention.io` 接收其他站点发送的 mention 以及如何在博客页面展示。
集成收到的 mention 信息有两种方式：
`Static` hexo 博客生成时写相关的数据到 html 页面中
`Dynamic` 访问网站时 javascript 实时解析数据展示
[IndieWeb, Webmentions | ./kwaa.dev](https://kwaa.dev/indieweb): [藍+85CD](https://kwaa.dev/about) 在 [Urara](https://github.com/importantimport/urara) 博客系统中实现的过程记录。该博客系统已开源，详见[RE:Introducing Urara | ./kwaa.dev](https://kwaa.dev/intro-urara/re)
[Webmention-developer#Sending - IndieWeb](https://indieweb.org/Webmention-developer#Sending) indieweb.org 收集的实现 Sending 功能开源项目列表
[Refactor your blog comments system with Webmention.io](https://geekplux.com/posts/webmention): GeekPlux 使用 twitter + webmention 实现博客评论系统
相关代码参考 [site/theme.config.js at main · geekplux/site (github.com)](https://github.com/geekplux/site/blob/main/blog/theme.config.js#L20-L149)
[Now, I'm in IndieWeb? - Owen Young's Blog](https://www.owenyoung.com/en/blog/indieweb/) zola 博客
定期拉取站点全部 mention 信息，生成站点时在 html 页面写入对应的 mention
[blog/send-webmention.yml at main · theowenyoung/blog · GitHub](https://github.com/theowenyoung/blog/blob/main/workflows/send-webmention.yml) 解析 rss feed 发送 mention 脚本
评论展示可以参考，如果匹配到作者发的推，用专门的卡片样式呈现
![](https://media.xiang578.com/202304011210483-owen-comment.png)
[Joining the Webmentions Community: A Beginner's Guide (eindex.me)](https://eindex.me/posts/webmentions/)  提供基于js 的 send mention 脚本
[Webmention - KAIX.IN](https://kaix.in/0001/webmention/)：介绍为什么要使用 webmention 以及写了个 webmention 接收器，不过没有找到相关代码链接。
## 发送
[Automatically sending Webmentions from a static website - James Mead](https://jamesmead.org/blog/2020-10-13-sending-webmentions-from-a-static-website)：解析站点 rss 然后通过 ifttt 发送请求
[Telegraph (p3k.io)](https://telegraph.p3k.io/)：手动发送链接
[kristofzerbe/hexo-console-webmention: Sending webmentions for posts within Hexo (github.com)](https://github.com/kristofzerbe/hexo-console-webmention)：解析最新 x 篇文章中引用的链接，然后发送到对应的接收服务。下载后，运行报错。
[Bridgy](https://brid.gy/) 获取 twitter 交互
## 接收
[Webmention.io](https://webmention.io/) 公开的接收服务，支持以 html，atom feed，json 等格式获取指定网址的 mention 信息
[Webmentions on a static site with GitHub Actions \ Seb De Deyne (sebastiandedeyne.com)](https://sebastiandedeyne.com/webmentions-on-a-static-site-with-github-actions/)：定时拉取 webmention.io 上的 webmention 结果
[新增对 Webmention 的支持 | Re:Linked (outv.im)](https://blog.outv.im/2021/webmention/)：基于 hexo+sass 的博客，提到 self-host 的接收服务 [outloudvi/workers-webmention-server: Webmention server on Cloudflare Workers. (github.com)](https://github.com/outloudvi/workers-webmention-server)
## 展示
[透過 webmention 來搜集 blog 的社群迴響 (jason-memo.dev)](https://jason-memo.dev/posts/webmention/) 评论展示形式很美观，值得学习。
![](https://media.xiang578.com/202303312113043-jason-webmention-example.png)
[拥抱独立网站运动 | M-x Chris-An-Emacser (chriszheng.science)](https://chriszheng.science/2022/02/09/Embracing-IndieWeb/)：hexo 博客，基于 webmention.js 展示收到的反馈。
[PlaidWeb/webmention.js: Client-side library for rendering webmentions from webmention.io (github.com)](https://github.com/PlaidWeb/webmention.js)：第三方 js 库
[Webmention Demo - IndieWeb Hexo Icarus (whyouare111.github.io)](https://whyouare111.github.io/hexo-icarus-showcase/2021/02/02/webmention-demo/) hexo+icarus 主题博客，实现 webmention + mastodon 集成。 修改后主题代码在 [whyouare111/hexo-theme-icarus at matataki (github.com)](https://github.com/whyouare111/hexo-theme-icarus/tree/matataki)。
提到 [About | Seviche.cc](https://seviche.cc/about/) 通过标签切换多种评论
评论模块以时间线形式展示 webmention
![](https://media.xiang578.com/202303252117168-whyouare111-webmention.png)

## 提醒
[回复《webmention 实现参考》 - IndieWeb Hexo Icarus (whyouare111.github.io)](https://whyouare111.github.io/hexo-icarus-showcase/2023/03/31/reply-to-ryen-xiang-20230331/)：`webmention.io` 提供 mention 的 rss feed，配合 rss 阅读器/IFTTT 等工具可以查看是否收到新的 mention
## 测试数据
[Owen 的「Now, I'm in IndieWeb? 」相关 mention](https://webmention.io/api/mentions.json?target=https://www.owenyoung.com/en/blog/indieweb/)
