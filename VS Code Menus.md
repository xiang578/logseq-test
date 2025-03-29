---
tags:
- VS Code
public: true
categories: 随手记
toc: true
date:
- 2024/06/21
deck: being/VSC
permalink: note/vs_code_menus
title: VS Code Menus
lastMod: 2024-10-05
toc: "true"
---

跟着 [[@如何提高编程速度：Emacs高手教授轻松精通所有编辑器和IDE的秘诀]] 过 VS Code 菜单的笔记，有些功能不看真不知道。
<!--more-->
## [[VS Code Menus/File]]
`Auto Save` 可以打开，自动保存文件
## [[VS Code Menus/Edit]]
### Find And Replace
移动搜索框到下方，解决部分文件路径过长。`"search.location": "panel"`
Advanced search options 中支持 glob syntax 语法指定搜索路径，具体用法见 [Basic Editing in Visual Studio Code](https://code.visualstudio.com/docs/editor/codebasics#_advanced-search-options)
![image.png](/assets/image_1718822131511_0.png)

### Toggle Comment 注释
Toggle Line Comment `cmd+/` 单行注释
Toggle Block Comment 多行注释
### [[Emmet]]
`Emmet is a plugin for many popular text editors which greatly improves HTML & CSS workflow.` 前面是官网介绍，简单说是加快写 HTML 和 CSS 的速度
写前端重复代码时使用，现在前端框架不太依赖这些。
`Emmet: Go to Matching Pair` 实现从 tag 的开头跳到结尾
## [[VS Code Menus/Selection]]
文本选择 `shift + 方向键`，以词为单位文本选择  `ctrl + shift + 方向键`
Expand Selection/Shrink Selection 选中从中心词往智能扩展/缩减选择区域，web 编程可以使用
![image.png](/assets/image_1718824319331_0.png)
`Copy Line Down` 在下方复制当前选中的行
Multi-Cursor [[Sublime Text]] 中的多行光标
Add Next Occurrence 选中当前词的下一个词，每个词后面加一个光标。实现的部分功能可能和 Replace 重复
![image.png](/assets/image_1718824742736_0.png)
## [[VS Code Menus/View]]
### Command Palette
[[滴答清单]] 和 cmd shift p 有冲突 [visual studio code - VSCode Command Palette (Ctrl + Shift + P) keyboard shortcut isn't working on new installation - Stack Overflow](https://stackoverflow.com/questions/67324821/vscode-command-palette-ctrl-shift-p-keyboard-shortcut-isnt-working-on-new)
### Open view
view 打开左侧或下面的面板
`Source Control` 源代码管理器
windows 系统支持按住 alt + 下划线对应的快捷键打开功能
### Appearance
Zen Mode 隐藏边栏，全屏
Primary Side Bar 左侧面板 Secondary Side Bar 右侧面板
Activity Bar Position 左侧几个大的图标
Zoom In/out `cmd -/=` 调整字体大小
![image.png](/assets/image_1718825591059_0.png)
### Editor Layout
`split Editor Down/Up/Left/Right` 创建子窗口
`Single` 单列
`three column` 三列，默认不打开
`Flip Layout` 行列布局互换
### 其他
word wrap 软换行
show minimap 右侧代码视图
show breadcrumbs 文件地址面包屑，点击跳转
Render Control Characters  显示老式打印机对应的一些字符。
render Whitespace 查看隐藏字符
## [[VS Code Menus/GO]]
### 跳转相关
[[GO to Definition]]
[[Go to Declaration]]  :<-> 跳转到声明
vim快捷键 :-> `g d`
如果在打开的多个文件中找到，跳出小窗让你选择。
![image.png](/assets/image_1718980695727_0.png)
### Switch Group 和 Switch Editor
group 对应子窗口
editor 对应group里面不同的 tab
`cmd + 数字` 切换光标到不同的 group
### 其他
Go File 文件名模糊搜索
Back 返回
Last Edit Location 返回最后编辑
Go to Line/Column 跳到指定行
[[Go to Bracket]] 跳转括号
### Peek
弹出窗口查看定义之类的，和 go to 对应。
### Next/Previous  Problem
错误之间跳转
### Next/Previous  Change
在没有提交到 Git 的改动之间跳转
Emacs [[git-gutters]] 支持模糊搜索改动，更加使用
## Debug
建议使用语言对应的第三方调试器
## Terminal
run task
## Help
Documentation 跳转到文档
Open Process Explorer 打开进程管理器
