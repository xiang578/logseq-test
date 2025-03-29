---
public: true
title: password
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

破译密码的复杂度主要在于密码的长度，包括我在内的大部分人很难记住上百个不同密码。这时候推荐使用密码软件：自动生成长密码，网页和 App 自动填充。当然，如果密码软件泄漏，完全没有办法。

我使用过的密码软件有：

  + `LastPass`：比较简单，只使用过 chrome 插件功能。

  + `1PassWord`：全平台，ui 美观，功能强大。除了能保存密码外，还能保存一些简单的笔记。~~目前主力使用，~~贵的东西除了贵就没有其他缺点了。

  + [[Bitwarden]] 基础功能免费 + 高级功能收费（2FA） 。官方提供 docker 镜像，可以私有化部署，该版本解锁全部会员功能。

    + 提供 iOS、Mac、Chrome 端

  + KeePass：开源方案，提供多种第三方客户端。所有数据保存在单一的文件中，安全性高，但是会带来跨平台同步问题。

    + MacOS

      + `MacPass`：node.js 开发， ui 简洁。

        + `Auto-type` 全局快捷键，不知道为什么在 qq 客户端上不能使用，看提示是 window 找不到，简单看了一下，感觉是软件功能比较弱。

      + `KeeWeb`：qt 开发，ui 古典。

        + `Auto-type`: 打开需要输入密码的软件，光标移动到输入框，然后打开 KeeWeb，按下 cmd+T，就能完成自动填充。

        + 打不开“KeeWeb-1.12.0.mac.dmg”，因为 Apple 无法检查其是否包含恶意软件。

          + `sudo spctl --master-disable`

      + `KeePassXC`：据说功能强大

    + Chrome 通过插件 `KeePassHttp-Connector` 来配合客户端实现网页上的密码填充。

    + iOS 中推荐 `FantasyPass`(12 元)，支持 faceid、touchid 打开，支持网页和 app 的自动填充。

KeePass

  + KeePass 这类软件在实现上有一个缺点：一条密码记录只能对应一个 website？如果有多个网址，就必须创建多条记录。这样带来的烦恼，是如果改变这个帐号对应的密码，就需要一个个修改。

  + MacPass 中可以复制一个项目，然后选择引用用户名和密码。KeeWeb 中不知道如何解决
