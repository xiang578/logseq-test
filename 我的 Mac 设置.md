---
public: true
title: 我的 Mac 设置
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

使用 [[iTerm]] 作为终端

  + [[Oh My Zsh]] zsh 配制文件

  + [[autojump]]

    + add `[ -f /opt/homebrew/etc/profile.d/autojump.sh ] && . /opt/homebrew/etc/profile.d/autojump.sh` to `.zshrc`

    + add `autojump` to `.zshrc` `plugins=(...)`

  + [[git-open]]

    + `git clone https://github.com/paulirish/git-open.git $ZSH_CUSTOM/plugins/git-open`

    + `.zshrc` change `plugins=(...)` to `plugins=(... git-open)`

  + zsh-syntax-highlighting 用绿色高亮输入正确的命令

    + `git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`

  + zsh-autosuggestions 命令补全建议

    + `git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`

[[Homebrew]] 管理应用下载

  + `mathpix-snipping-tool` [[Mathpix]] 数学公式截图转 latex 格式

  + 

[[Dropbox]]

[[Microsoft Edge]]

  + [[简悦]]

[[坚果云]]

[[截图 Jietu]]

[[Alfred]]

[[Squirrel]]

  + 用户配置文件  `~/Library/Rime`

  + installation.yaml

[[Logi]] Options

  + MX Master 2s 鼠标配置

  + 滚动模式，逐段模式

[[Zotero]]

  + 6 还没有 Apple Silicon 版本，预计 7 会出。

  + [ZotFile - Advanced PDF management for Zotero](http://zotfile.com/index.html#changelog)

    + Renaming Format 修改格式为

      + {%t_}{%y_}{%a}

      + {%t_}{%y_}{%a}

  + [l0o0/jasminum: A Zotero add-on to retrive CNKI meta data. 一个简单的Zotero 插件，用于识别中文元数据 (github.com)](https://github.com/l0o0/jasminum)

[[PDF expert]]

[[DEVONthink]]

[[VS Code]]

  + 

[[Sublime Text]]

[[Sublime Merge]]
