---
public: true
title: "Mac/重置隐私设置"
tags:
date: "2024-10-05"
updated: "2024-10-05"
toc: true
mathjax: true
---

问题

  + 钉钉提示没有麦克风权限，然后在系统设置页面相关选项下没有钉钉可以添加。

  + 重置相关设置，重启钉钉，发起会议，触发请求权限的弹窗。

重制 mac 上麦克风、摄像头、屏幕录制的权限

```bash
sudo tccutil reset Microphone
sudo tccutil reset Camera
sudo tccutil reset ScreenCapture
```


