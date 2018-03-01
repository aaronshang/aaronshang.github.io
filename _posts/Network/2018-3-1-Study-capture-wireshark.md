---
layout: post
title: Wireshark的学习
categories: [网络技术]
description: 
keywords: 网络
---

### 简介

> 1. Wireshark简介
> 2. 如何应用

#### Wireshark介绍

> 用来抓包使用。可以分析网络协议。采用Winpcap抓包。
>

#### Winpcap

原理：绕过操作系统的协议栈，访问原始网卡数据包。直接与网络接口驱动交互，具系统依赖性。

如果抓包，考虑使用`Winpcap`进行抓包。

