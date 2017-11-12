---
layout: learning
title: cocos2dx-anchorpoint and position
date: 2017-11-12 21:03:42 +0800
categories: game
tags: cocos2dx
keywords: cocos2dx
---

#cocos2dx-anchorpoint and position

最近在学写小游戏。遇到anchorpoint和position非常懵。

anchorpoint 都是0-1的
(0,0) 指的是左下角
(1,1) 指的是右上角
以此类推

position的坐标轴是从左下角开始计算的。左下角为（0，0）。
setposition中visiblesize.height*0.75则y轴为0.75高。x轴没弄明白，有点奇怪。