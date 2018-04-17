---
layout: learning
title: difference bewteen ssh and https
date: 2018-04-17 15:14:04 +0800
categories: learn
tags: ssh, https
keywords: ssh
---

Difference between ssh and https 

When git clone some projects in github or other platform, there are basically two ways to get projects locally.

The first one is ssh, and the other one is https.

The major difference of these two is that, ssh can be used without username and password while the https needs.

The way ssh tries to do is to use ssh to generate pair of keys (both public and private)and give github public key to establish SSH connections.

A reference is here.
[HTTPS (SSL) and SSH: A Conceptual Understanding](https://medium.com/@alxsanborn/https-ssl-and-ssh-a-conceptual-understanding-9-2-16-4e75ce8d574)