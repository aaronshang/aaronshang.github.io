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

> 用来抓包使用。可以分析网络协议。
>
> 启动server后，客户端无需connect，直接用`sendto`向server监听的端口发数据包。
>
> 采用Winpcap抓包。

