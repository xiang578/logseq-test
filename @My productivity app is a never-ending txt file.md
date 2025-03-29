---
tags:
  - web
  - Workflow
public: true
categories: 随手记
toc: true
date:
  - 2024/05/25
permalink: note/productivity_text_file
alias:
  - My productivity app for the past 12 years has been a single txt file
title: @My productivity app is a never-ending txt file
updated: 2024-10-05
mathjax: true
---

链接：[My productivity app is a single .txt file (jeffhuang.com)](https://jeffhuang.com/productivity_text_file/)

<!--more-->

## 想法

  + 这几天又看见有人分享这篇文章，想起来第一次，作者的标题还是 past 12 years，一转眼又过去好几年。

  + [[Twitter]] 12 年间使用一个 txt 进行任务管理方法分享。作者提到 to do list 变成 what done list 的过程，每天晚上将日历中第二天的代办事项整理到 txt 中，第二天顺手记录任务相关的信息（比如讨论出的结论，或者得到的信息）。结合自己使用经历，OmniFocus 是一个 to do list，基于纯文本的任务管理方式（org-mode 或 taskpaper）更容易成为 what done list。

    + [[Twitter]] 另外基于 Roam Research 的大纲形式以及 block ref 功能，很容易打造 what done list 。

  + 任务管理系统只需要让使用者有一种自己能掌握全部事情的感觉即可。

## 摘录

  + **Prerequisite** 使用在线日历管理全部的代办事项和未来计划

  + **Making the Daily List** 每天睡觉前将日历中第二天需要完成的任务放到 txt  文件最后

    + scheduled tasks: 2pm meeting with Madonna, 4pm office hours

    + errands: sign a form, return a book

    + work items: review a paper, prepare a presentation

  + **As a Record** to do list 变成  what done list，记录相关的任务细节。

  + **Shortcuts and Features** 使用特定的格式方便搜索以及统计数据

    + 比如 `meet with` 代表 meetings

    + `idea`  代表想法

    + `annual` 写到下一个年度报告中

    + `nextui` 为下一次 next ui 课程增加的内容

  + 邮件处理

    + flag red 需要处理

    + flag Orange  需要其他人帮助处理

    + flag Yellow 等待他们回复

    + 一天结束的时候，查看所有有flag的邮件，看有没有要升级为红色flag的邮件，将红色flag的事情排到第二天的日程中

  + **daily routine**

    + look at the daily todo list I wrote last night to find out what I'm doing today

    + do scheduled things on that list during the day

    + when I have free (unscheduled) time, do the floating tasks on my list and work on Red-flagged emails

    + at the end of the day

      + do a quick review of Orange/Yellow emails to see if they need any handling

      + copy the next day's calendar items to the bottom of the text file

  + 好处

    + 每天早上起来都知道自己需要干什么

    + 长时间联系可以准确估计完成任务的时间

    + 减轻记忆负担(集中管理，知道自己不会错过)

    + 动态调整工作量(减少标记的邮件、减少日历中的待办事项)

  + ## 一天的结束后的记录

```markdown
2017-11-31
11:00am meet with Head TAs
- where are things at with inviting portfolio reviewers? A: got 7/29 replies
- need 3 TAs for Thursday lab
- Redesign assignment handout will be done by Monday, ship Thursday
11:30am meet with student Enya (interested in research)
- they're a little inexperienced, suggested applying next year
review and release A/B Testing assignment grading
12pm HCI group meeting
- automatically generate thumbnails from zoom behavior on web pages
- #idea subliminal audio that leads you to dream about websites
- Eminem presenting Nov 24
- vote for lab snacks. A: popcorn and seaweed thing
got unofficial notification ARO YIP funding award #annual #cv
read Sketchy paper draft
- needs 1 more revision
- send to Gandalf to look at?
Zelda pick up eye tracker
- have her sign for it
update biosketch for Co-PI
unexpected drop in from Coolio! #alumni
- now a PM working on TravelAdvisor, thinking about applying to grad school
3:15pm join call with Umbrella Corp and industry partnership staff
- they want to hire 20 data science + SWE interns (year 3), 4 alums there as SWE
3:45pm advising meet with Oprah
- enjoyed CS 33
- interning at Facebook
4pm Rihanna talk (368 CIT)
5pm 1:1 with Beyonce #phdadvisee
- stuck on random graph generating crash
	- monitor memory/swap/disk?
	- ask Mario to help?
- got internship at MSR with Cher
	- start May 15 or 22
- will send me study design outline before next meeting
- interviewing Spartacus as potential RA for next semester
6pm faculty interview dinner with Madonna (Gracie's)
- ask about connection with computer vision
- cool visual+audio unsupervised comparison, thoughtful about missing data, would work with ugrads (?), likes biking, teach compvis + graphics
- vote #HIRE
#note maybe visit Monsters University next spring, Bono does related work
```

## 参考

  + Hacker News 两次讨论

    + 链接：[2021-12-23](https://news.ycombinator.com/item?id=29661167#/)、[2020-02-08](https://news.ycombinator.com/item?id=22276184#/)

    + Any productivity system can be made to work once it becomes a habit and therefore your default action.

    + We are what we repeatedly do. Excellence, then, is not an act, but a habit.

    + Randy Pausch log format `priority - datetime stamp - keywords/tag - content` [nrr-deprecated/todo: Tools inspired by the late Randy Pausch to help keep me on-task (github.com)](https://github.com/nrr-deprecated/todo#/)

      + `note (maybe some text here)`

    + `vim +'normal Go' +'r!date' did.txt` 打开 vim 然后在文件最后一行加上日期。详细解释 [did.txt file – Patrick (theptrk.com)](https://theptrk.com/2018/07/11/did-txt-file/#/)

  + [X 上的 MindForge (曼福吉)：“我的生产力应用程序是一个永无止境的.txt文件 https://t.co/iBSTeUbnvH Jeff Huang 使用 UltraEdit 手写一个 51,690行 的txt 文件，作为其生产力工具，这个 txt 记录了他作为教授所做的一切，他遇到的几乎每个人，以及关于他们讨论的内容或想法的笔记。 Jeff Huang 的 txt 工作流： -” / X](https://x.com/henices/status/1793289832149499969)

    + 总结的要点

      + 1. started just tracking in a single text file - **在同一个地方**

      + 2. consistent writing style - **以一致的标准**

      + 3. I have some tags like # idea for new ideas to revisit when I want project ideas - **记录你的洞见**

  + [用txt文件做日程管理 (qq.com)](https://mp.weixin.qq.com/s?__biz=MzA3MTk1NzcxNA==&mid=2650523612&idx=1&sn=b4f2d0fcb73c0efb0c6bc8f0821dd998&chksm=872aca61b05d43773be6f376decd5ba24000e54e534b1f8343dfddd988e1395954776ba90b8d&scene=21#wechat_redirect) [[徐颖@笔记花园]]

    + 无论是Luhmann的slip box，还是Jeff的txt文件，都不是笔记软件，而是笔记方法。方法遵循清晰的原则——他们知道自己在记录什么（What）、何时记录（When）、如何记录及检索（How），以及最基本的——为何而记录（Why）

    + 7年记录了37000多行，完全能够记得什么时候，见过什么人，讨论过什么事情，以及自己的想法。

    + slip box笔记法围绕主题和上下文建立卡片笔记，强调笔记的去向。有网友评价其因为具备“耗散结构”而具有活力，笔者赞成这个说法。耗散结构因为能抵抗熵增，被认为是生命的基本特征，可参考《重新认识生命》。也就是说：有效的笔记，就是让信息变得有秩序。

    + 用txt文档做日程管理，就是记流水账，记下将要做的事情，记录做过的事情和有用的想法。笔记中，时间是最重要的维度，这非常有利于时间管理与生产力评估。总的来说记录是线性的，但是，利用关键字或tag，也能组织出主题内容。

    + 做笔记，原则比工具重要，工具可以帮忙更好的实施原则。

      + 笔记软件的用户，应根据自己的意图，定制不同的原则。

      + 笔记软件开发者，则可以根据这些典型用户的做法，改进产品。




