---
date: {{ .Date }}  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "{{ replace .Name "-" " " | title }}"  # 文章标题
description: "文章描述"
url:  "{{ .Name }}"  # 设置网页链接，默认使用文件名
tags: [ "tag1", "tag2"] # 自定义标签

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

draft: false  # 草稿
---