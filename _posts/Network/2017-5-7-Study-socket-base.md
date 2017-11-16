---
layout: post
title: socket基础知识
categories: [网络技术]
description: 
keywords: 网络
---

### 简介

> socket原理及主要理解。

#### UDP

> tcp有三次握手，有连接的概念，而udp服务器与tcp服务器不同，udp没有连接的概念。
>
> 启动server后，客户端无需connect，直接用`sendto`向server监听的端口发数据包。
>
> server中直接使用`recvfrom`来等待client收到的数据。

