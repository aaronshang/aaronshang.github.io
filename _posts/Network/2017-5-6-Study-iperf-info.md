---
layout: post
title: iPerf
categories: [网络技术]
description: 
keywords: 网络
---

### 简介

名词解释

> 一个网络性能测试工具。可以测试最大TCP和UDP带宽性能，具有多种参数和UDP特性，可根据需要调整，可以报告带宽、延迟抖动和数据包丢失。
>
> `iPerf3`与`iPerf2` 是相互独立的，前者包含后者部分代码。前者是ESnet/Lawerence Berkeley National Laboratory开发基于BSD许可。后者是NLANR/DAST开发。
>
> [官网](https://iperf.fr) 
>

参数解释

[详细链接](http://man.linuxde.net/iperf)

实例，UDP测试

> 服务器执行：./iperf -u -s
>
> 客户端执行：./iperf -u -c 10.255.255.251 -b 900M -i 1 -w 1M -t 60

[运行图](http://shangkai007.top/images/network/iperf-dual-client.png)

### iPerf特性

1. TCP and SCTP：可测量带宽，报告MSS/MTU大小，通过套接字缓冲区支持窗口大小。
2. UDP：客户端可创建UDP流，测量丢包，测量抖动。
3. 客户端和服务器可同时有多个连接
4. 服务器处理多个连接，而不是一定等到一次测试后结束
5. 可运行指定的时间
6. 打印周期，中间带宽，抖动，丢包在指定的间隔下
7. 运行服务器作为一个守护进程
8. 服务器接收单个客户端（iPerf3），多个客户端同时（iPef2）
9. *新* ：忽视TCP慢启动
10. *新*：为TCP和UDP设置带宽 
11. *新*： 使用SCTP而不是TCP
12. *新*： 输出JSON格式

### iPerf3用途

ESNet开发iPerf3的主要兴趣是测试高性能研究、教育、网络。但缺乏iPerf2的一些特点，比如`multicast tests`、`bidirectional tests`、`multi-threading`、`official windows support`。