---
laypost: post
title: "Github免密码提交"
date: 2018-10-10
excerpt: "简单介绍通过修改项目Url方式，以SSH协议提交项目源代码"
tags: [github, git]
comments: true
---

In case you are indeed using the SSH URL, but still are asked for username and password when git pushing:
`git remote set-rul origin git@github.com:<Username>/<Project>.git`

You should try troubleshooting with:
`ssh -vT git@github.com`
