---
layout: post
title: AT相关基础
categories: [计算机]
description: 
keywords: Lock
---



参考

[AT命令集概述](http://m.it610.com/article/5308181.htm)



AT+CGDCONT引起的思考

> 作用：sets the PDP context parameters such as PDP type (IP, IPV6, PPP, X.25 etc), APN, data compression, header compression etc.

何为PDP contexts

> 一个PDP上下文提供一个分组数据连接，通过该连接可以在UE和网络之间交换IP包，这些数据连接的使用仅限于特定的服务，这些服务可以通过所谓的接入点来进行访问。

接入点

> 可以理解为IP路由器，它可以为UE喝其所选择的服务之间提供连接，这些服务可以是：
>
> 多媒体消息服务（MMS）
>
> 无线应用协议（WAP）
>
> 直接Internet接入
>
> IP多媒体子系统（IMS）
>
> 根据网络运营商的设定，同一个接入点可以提供不止一种服务。

