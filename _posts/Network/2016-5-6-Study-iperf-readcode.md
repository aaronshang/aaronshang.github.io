---
layout: post
title: IPerf 源码解读
categories: [网络技术]
description: 
keywords: 网络
---

### 准备

> 源码下载
>
> [IPerf2地址](https://sourceforge.net/p/iperf/code/HEAD/tree/)
>
> [Github IPerf地址](https://github.com/esnet/iperf)
>
> [iPerf2 win工程](http://download.csdn.net/download/yangwu070710/8215865)
>
> [code分析参考](http://blog.chinaunix.net/uid-11568125-id-2868801.html)

### 主要版本

1. 1.7.0（2003-3-13 已停止维护）
2. 2.0.10 (2017-8-11 只修正)
3. 3.2 (2017-6-26 迭代中)

### iPerf2 Code (Win)

1.7.0中代码

Lib功能

1. `SocketAddr` 网络地址结构，地址转换
2. `Socket`封装socket文件描述符
3. `Mutex`和`Condition` 封装了POSIX标准的线程同步机制
4. `Thread`封装了POSIX中的多线程机制
5. `tcp_window_size`TCP窗口大小处理函数

### 主要类

![]()

1. `PerfSocket`，实现了通信大多数功能，如手法数据包、报告网络参数等。
2. `Notify`提供对所监控线程进行排他访问的数据区。
3. `Listener`实例是一个执行线程，也具收发数据的能力。其创建Speaker和Audience。
4. Audience，听者线程的监控线程
5. Speaker，说着线程的监控线程
6. Server，实现听者进程
7. Client，实现说着进程