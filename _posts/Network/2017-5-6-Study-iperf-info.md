---
layout: post
title: IPerf
categories: [网络技术]
description: 
keywords: 网络
---

### 简介

名词解释

> 一个网络性能测试工具。可以测试最大TCP和UDP带宽性能，具有多种参数和UDP特性，可根据需要调整，可以报告带宽、延迟抖动和数据包丢失。
>
> [官网](https://iperf.fr)
>
> [2&&3区别](https://iperf.fr/iperf-doc.php#3change)

参数解释

| 命令行选项          | 环境变量选项          | 描述            |
| -------------- | --------------- | ------------- |
| -f, format     | $IPERF_FORMAT   | 格式化带宽输出       |
| -i, --interval | $IPERF_INTERVAL | 设置每次报告之间的时间间隔 |
| -p, --port     |                 | 设置端口          |
| -u, --udp      |                 | 使用UDP而非TCP    |
| -c, --client   |                 |               |
| -s, --server   |                 |               |
| -d, --dualtest |                 | 运行双测试模式       |
| -r, --tradeoff |                 | 往复测试模式        |
| -t, --time     |                 | 设置传输的总时间      |

[详细链接](http://man.linuxde.net/iperf)

实例，UDP测试

> 服务器执行：./iperf -u -s
>
> 客户端执行：./iperf -u -c 10.255.255.251 -b 900M -i 1 -w 1M -t 60
>
> 其中-b表示带宽

功能（UDP）

> 1. 测量丢包
> 2. 测量延迟
> 3. 测量多播