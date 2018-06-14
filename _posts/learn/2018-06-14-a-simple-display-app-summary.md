---
layout: learn
title: 一个展示型小项目的简单总结
date: 2018-06-14 11:08:05 +0800
categories: learn
tags: js, react
keywords: js, react
---
这篇文章是为了总结最近做的一个小项目。大概一年半多没有做一个完整的前端项目了。
这次遇到了一些坑，也学到了一些东西。特来总结。
主要分成以下几个部分。

### 路由设计 （BrowerRouter && HashRouter 对比)
### 结构设计
这个项目的结构其实是非常简单清楚的。 它最开始是有一个主屏幕上面有八个按钮，任意点击其中一个按钮可以跳转到内容页。
内容页是侧边按钮，右边显示相应内容。

最开始采用的是将首页和内容页分开。分为Home和Other。然后再Other下面分成八个子components。这样的设计在实践的过程中，
发现有很多冗余重复的部分。因为这八个components其实是有很多类似的地方。首先，有五个component都是有list,就是类似tab，
每个tab下都是单独的内容。然后他们都需要去向后端获取数据来呈现相关内容。于是我花了一天来重构了整个子component下的结构。

我将Other下这八个component分成四个部分，分别是BasePage, ComponentSet, RouteInfo, Layout。

- RouteInfo是根据ComponentSet中提供的type参数去Layout里选择相应的layout。
-  Layout根据RouteInfo传的相关参数和数据来显示不同的页面，主要负责样式的显示和管理，
后续加了maintain组件，在无数据的时候显示加载中。
-  BasePage主要是负责是否有list的显示，相关路由（根据JSON文件去配置相关数据），以及作为整个template的基础和入口。
-  ComponentSet主要是使用BasePage和RouteInfo来组成相关的八个component。

然后我把api调用单独分出来放在api的文件里，方便调用。这个下面会说。

我觉得有几个地方没做好。最近动态的地方，无数据没有加提示；是room因为逻辑有点小复杂没有合并进去做，但其实是可以合并的；api好像没有做到多线程；还有就是没有控制页面的zoom-in, zoom-out。


### api调用以及缓存管理
最开始把api单独封装在一个文件里其实是为了减少代码的重复。于是，参考一篇文章封装了api。后来在做缓存管理的时候，又更新了相关的代码。
主要参考了这两篇文章。
[这篇-api封装](https://github.com/xiaohesong/ums/wiki/React%E5%B0%81%E8%A3%85Fetch%E8%8E%B7%E5%8F%96Api,-%E7%88%B6%E7%BB%84%E4%BB%B6%E4%B8%8E%E5%AD%90%E7%BB%84%E4%BB%B6%E7%9A%84%E9%80%9A%E8%AE%AF)
和[这篇-缓存](https://www.sitepoint.com/cache-fetched-ajax-requests/)

### 部署
react的部署服务器用的是nginx。
### 其他（包括第三方库的引用，idle activity，svg的引用）
