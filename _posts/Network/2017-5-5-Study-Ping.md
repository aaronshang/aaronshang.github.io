---
layout: post
title: Ping
categories: [网络技术]
description: 
keywords: 网络
---



### 1 简介

名词解释

> Ping，（Packet Internet Groper）,  因特网包嗅探器，用于测试网络连接量的程序。

原理

> 利用网络上机器IP地址的唯一性，给目标地址发送一个数据包，再要求对方返回一个同样大小的数据包来确定两台机器是否连接相通，时延是多少。

参数

> TTL：数据包的生存时间。（Time To Live）。
>
> 介绍：用来计算数据包在路由器的消耗时间。小于1s算1s，每经过一个路由器节点TTL减1。实际中把时间限制改成`跳数`限制。
>
> 系统集成的Ping默认值：Linux的TTL为64或245，Unix主机的TTL为255。比如ping百度TTL应该为64，返回60，则经过64-60=4个路由器。TTL减到0，就自动消失。

### 2 ICMP协议

名词解释

> Internet Control Message Protocol，Internet控制报文协议。是TCP/IP协议族的一个子协议，用于在IP主机、路由器之间传递控制消息。
>
> `控制消息`是指网络通不通、主机是否可达、路由是否可用等网络本身的消息。不传递用户数据。