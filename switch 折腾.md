---
public: true
title: switch 折腾
tags:
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

数据备份
`atmosphere` 大气层系统相关文件
`emuMMC` 虚拟系统内存中数据
`Nintendo` 虚拟系统 SD 卡中数据
游戏安装
DBI [DBI实用功能介绍 (qq.com)](https://docs.qq.com/doc/DVW9SVnBGb2R5emdB?u=c3365b5d53db4c069396ff8bab44d960)
Switch 打开 DBI，选择 Run MTP Server
Mac 下载 [Android File Transfer](https://www.android.com/filetransfer/)，然后将数据拖到 MicroSD install 目录
无线安装 [【DBI 258】【支持xci】摆脱USB线！用DBI HTTP 方式无线安装游戏 - NS工具研究区 - nsboy-下载Switch游戏,NS游戏下载,网盘下载 - Powered by Discuz!](https://www.nsboy.net/thread-13141-1-1.html)
mac 游戏目录运行 `python -m http.server` 成为主机，默认地址是 `http://ip:8000`
switch 打开 dbi 或者 awoo installer 等工具，输入上面的地址，等待连接成功，就可以通过网络安装游戏
Awoo installer
可以直接安装阿里云盘内资源
使用 mac 系统更换 SD 内存卡
1. 使用 mac 上 `磁盘工具 Disk Utility` 制作镜像，备份旧 SD 卡全部内容
`文件 -> 新建映像 -> 基于 "xxx" 新建映像`，其中 xxx 就是你旧 SD 卡的名称
2. 将新 SD 卡格式化成 exfat 格式
3. 复制镜像文件中的全部数据到新 SD 卡
4. 修改新 SD 内文件属性
参考
[How to transfer SD card data using macOS : r/NintendoSwitch](https://www.reddit.com/r/NintendoSwitch/comments/emjvdf/how_to_transfer_sd_card_data_using_macos/)
[Mac电脑操作导致NS无法读取SD卡的解决 – XK's Blog (1vr.cn)](https://1vr.cn/?p=2721)
游戏格式
NSP
Nintendo Submission Package
eshop 中的数字版
压缩格式为 NSZ
XCI
NX Card Image
卡带 dump 文件镜像
压缩格式为 XCZ
报错
无法启动软件，请在HOME菜单中再试一次
[修复switch游戏无法启动的问题 (zfdang.com)](https://blog.zfdang.com/2022/02/switch-fix-unable-to-start-software-issue/)：进入维护模式再重新启动
failed to get update information daybreak mac
[Daybreak will fail to validate Updates with Mac OS ._ files present · Issue #1487 · Atmosphere-NX/Atmosphere (github.com)](https://github.com/Atmosphere-NX/Atmosphere/issues/1487) 看这个链接大概是 macos 在外部存储设备上创建了隐藏文件导致 daybreak 校验数据不通过，其他人给的建议是不要用 mac 拷贝游戏文件。。。
存档管理
[Switch 存档工具 JKSV 图文使用教程 | 时鹏亮的Blog (shipengliang.com)](https://shipengliang.com/games/switch-%e5%ad%98%e6%a1%a3%e5%b7%a5%e5%85%b7-jksv-%e5%9b%be%e6%96%87%e4%bd%bf%e7%94%a8%e6%95%99%e7%a8%8b.html)
相关资源
[switch问题自查 (qq.com)](https://docs.qq.com/doc/DVVFMWXRLQ096RXVG?&u=c3365b5d53db4c069396ff8bab44d960)
[Home Page (tinfoil.io)](https://tinfoil.io/)