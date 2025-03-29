---
tags:
  - Vim
public: true
categories: 随手记
toc: true
date:
  - 2024/06/21
permalink: note/vimtutor
deck: being/Vim
title: vimtutor
updated: 2025-01-23
mathjax: true
---

跟着 [[@如何提高编程速度：Emacs高手教授轻松精通所有编辑器和IDE的秘诀]] 学习 vim 官方教程的记录。

<!--more-->

[[vimtutor/第二讲]]

## 第三讲

  + 删除的内容会被放入 Vim 寄存器

  + `p` :<-> 将最后一次删除的内容置入光标之后。
  + 更改类操作符 `c [number] motion`

    + `ce` :<-> 从当前位置删除到单词结尾，然后进入插入模式
    + 感觉 c 比 d 就多了一个删除完之后进入插入模式？

## 第四讲

  + `CTRL-G` :<-> 显示当前编辑文件中当前光标所在行位置以及文件状态信息
  + 输入行号 + G（或 gg）:-> 跳转到对应行
  + 查找字符串，方向

    + `/` :<-> 正向
    + `?` :<-> 逆向
  + `jump list` 查看访问过位置的历史记录命令 :-> `:jumps`
    + `CTRL-O` :<-> jump back 跳转到上一个历史位置，回到之前编辑的位置
    + `CTRL-I` :<-> jump forward 跳转到下一个历史位置
  + `%` :<-> 查找匹配括号对
  + 字符串替换

    + `:s/old/new` 替换光标所在行的第一个匹配，`/g` 替换全行的匹配串

    + `:#,#s/old/new/g` :<-> 指定行号之间
    + `:%s/old/new/g` :<-> 整个文件中的每个匹配
    + `:%s/old/new/gc` :<-> 提示是否进行替换，
      + c 对应单词 :-> confirm
[[vimtutor/第五讲]]

## 第六讲

  + 打开类命令 `o` 和 `O`

  + 插入

  + `a` 光标后插入

  + `A` 行末插入

  + `R` 连续替换多个字符

  + `j$` 光标移动到下一行末尾

  + ### 设置类命令

    + `:set ic` Ignore Case，忽略大小写。取消 `:set noic`

      + `/ignore\c <回车>` 一次查找忽略大小写

    + `:set hls is`

      + `hlsearch` 高亮

      + `incsearch` 查找短语时显示部分匹配

## 第七讲

  + `:help 参数` :<-> 看指定参数的含义
  + `CTRL-W CTRL-W` :<-> 不同窗口切换
  + 启动脚本 `vimrc 文件`

  + `CTRL-D` :<-> 命令行补全，列出已输入字符对应可能的命令
    + TAB 命令行补全


