---
title: sed
public: true
tags:
- Linux
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

删除包含特定字符串的行 `sed '/abc/d;/efg/d' a.txt > a.log`

删除前几行 `sed -i '1,10d' filename`

删除最后几行 `sed -i '$d' fileName`

在每行的头添加字符，比如"HEAD" `sed 's/^/HEAD&/g' test.file`

在每行的行尾添加字符，比如“TAIL” `sed 's/$/&TAIL/g' test.file`

`sed -n`

  + 安靜 (silent) 模式

`[n1[,n2]]function`

function

  + p 打印

mac `sed -i "tmp" "命令" file.txt`

  + 需要指定一个备份字符串，原文件会保存成 `file.txttmp`

  + 如果不需要备份，直接给个空字符串

其他分隔符

  + `@`

  + `|`

  + `!`

  + 反引号
