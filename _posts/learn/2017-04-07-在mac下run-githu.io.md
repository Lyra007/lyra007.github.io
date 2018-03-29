---
layout: learn
title: 在mac下run github.io
date: 2017-04-07 15:23:23 +0800
categories: learning
tags: [ruby, conf]
keywords: none
---

# 在mac下run github.io

之前在ubuntu上写的博客,最近迁移到mac上写就一直报错。报错如下：


<img src="/img/blog/error1.png" style="width:80%" />


出现这个问题的原因主要是Ruby环境需要2.2版本以上，所以要<mark>更新Ruby环境</mark>。


虽然mac有自带的ruby,但是还是不要再那个基础上改好。我现在的做法是下载rvm，然后再下载下相应版本的ruby。
另外，gem需要替换成淘宝镜像源。


同时，在升级ruby的过程中，遇到了如下问题。【ruby 2.2.1， EI Captian】
<img src="/img/blog/error2.png" style="width:80%" />

使用 <mark>xcode-select --install</mark>可以解决这个问题


还有一个问题是升级homebrew，可以用<mark>sudo chown -R $(whoami) /usr/local</mark>

BTW, using <mark>jekyll serve</mark> to run github.io


bundler: exec needs a command to run

bundle exec jekyll serve
