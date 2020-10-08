---
date: 2020-10-06T11:57:22+08:00  # 创建日期
author: "Rustle Karl"  # 作者
# cover: "/examples/imgs"  # 封面图，可以是相对于 static 的路径，也可以是相对于当前的路径

# 文章
title: "Hogo 网站页面小部件合辑"  # 文章标题
description: "统计文章篇数、字数、社交图标、看板娘等小部件"
url:  "posts/2020/10/06/components"  # 设置网页链接，默认使用文件名
tags: [ "hugo", "js", "css", "html"]  # 自定义标签
series: [ "博客系统摸爬滚打"]  # 文章主题/文章系列
categories: [ "浅尝辄止"]  # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

index: true  # 文章是否可以被索引
draft: false  # 草稿
---

## 看板娘

`layouts/partials/prepended_head.html`

```html
{{- if .Site.Params.Live2D -}}
<script>
    {{/*  设置看板娘样式  */}}
    localStorage.setItem("modelId", 5);
    localStorage.setItem("modelTexturesId", 0);
</script>
<style>
    #waifu {
        margin-bottom: 0 !important;
    }
    {{/*  隐藏设置和对话  */}}
    #waifu-tool {
        display: none;
    }
    #waifu-tips {
        display: none;
    }
    #waifu #live2d {
        height: 200px !important;
        width: 200px !important;
    }
</style>
<script src="https://cdn.jsdelivr.net/gh/stevenjoezhang/live2d-widget/autoload.js"></script>
{{- end -}}
```

## 右上角图标

`layouts/partials/menu.html`

{{<code language="html" title="layouts/partials/menu.html" id="1" expand="" collapse="" isCollapsed="true" >}}
<style>
  #github svg {
    transition: all 1s;
    fill: #222;
    color: #fff;
    position: absolute;
    top: 0;
    right: 0;
    border: 0;
    width: 70px;
    height: 70px;
  }

  #github:hover svg {
    width: 140px;
    height: 140px;
  }
</style>

<a id="github" href="https://github.com/fujiawei-dev" target="_blank">
  <svg viewBox="0 0 250 250" aria-hidden="true">
    <path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path>
    <path
      d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2"
      fill="currentColor" class="octo-arm"></path>
    <path
      d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z"
      fill="currentColor" class="octo-body"></path>
  </svg>
</a>
{{</code >}}

## 统计文章篇数、字数

`layouts/partials/footer.html`

{{<code language="html" title="layouts/partials/footer.html" id="2" expand="" collapse="" isCollapsed="true" >}}
<!-- 统计文章篇数和字数 -->
{{ $scratch := newScratch }}
{{ range (where .Site.Pages "Kind" "page" )}}
{{ $scratch.Add "total" .WordCount }}
{{ end }}

<footer class="footer">

  <!-- 统计文章篇数和字数 -->
  <div class="footer__inner">
    <div class="copyright copyright--user">
      <span>计 {{ len (where .Site.RegularPages "Section" "posts") }} 篇 | {{$scratch.Get "total" }} 字</span>
    </div>
  </div>
  <br>
  <!-- Copyright -->
  <div class="footer__inner">
    <div class="copyright copyright--user">
      <span>Copyright © 2019-{{ now.Year }} | Rustle Karl</span>
    </div>
</footer>

<script src="{{ "assets/main.js" | absURL }}"></script>
<script src="{{ "assets/prism.js" | absURL }}"></script>

{{- partial "extended_footer.html" . }}
{{</code >}}

## 评论

`layouts/partials/comments.html`