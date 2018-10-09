---
layout: post
title: "Gems镜像源配置"
date: 2018-10-09
excerpt: "简单介绍Gems镜像源配置方法。"
tags: [sample post, readability, test]
comments: true
---

# RubyGems 镜像

中国RubyGems镜像的管理工作[Ruby China](https://gems.ruby-china.com/)组织负责，以便能有更多的社区爱好者参与进来，保持持续发展。建议使用所在区域的源，可以保证软件包更新速度快速、稳定。

### Gems源修改方法

```shell
$ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
# gem sources -l
*** CURRENT SOURCES ***

https://gems.ruby-china.com
# 请确保只有 gems.ruby-china.com
$ gem install rails
```

###  Bundle源修改方法

可以采用Bundler的Gem源代码镜像命令：

```shell
$ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

而不必修改项目的Gemfile的source：

```
source 'https://rubygems.org/'
gem 'rails', '4.1.0'
...
```
