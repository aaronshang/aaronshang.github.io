---
layout: post
title: 编译USBPcap
categories: [网络技术]
description: 
keywords: USBPcap
---

#### 1教程

##### 1.1简介

USBPcapCMD-用户示例命令行程序。

USBPcapDriver-用于捕获数据的驱动

#### 1.2编译

> Windows 8 Build instructions:
>   In order to compile for Windows 8, you need to have Visual Studio 2013
>   Community and install Windows Driver Kit 8.1 Update.
>   To create solution file use the following command from Visual Studio 2013
>   Command Prompt (while being chdired into usbpcap sources directory):
>
>   > Nmake2MsBuild dirs 
>
>   This will create solution dirs.sln. You can build the driver from the
>   Visual Studio 2013 Command Prompt:
>
>   > MSBuild dirs.sln /p:Configuration="Win8 Debug"





