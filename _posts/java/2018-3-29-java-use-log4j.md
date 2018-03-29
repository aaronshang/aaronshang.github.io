---
layout: post
title: Java使用日志
categories: [Java]
description:
keywords: Java
---

#### 1 背景

​	使用系统日志有不足如下：

1. 没有时间

2. 没有线程归属

3. 不易关闭

4. 不能生成日志文件

   采用log4j模块，可有效处理以上问题。

#### 2 log4j的使用

​	工程中加载相应的jar包。

​	在src同目录下简历配置文件`log4j.proterties`,内容参考如下

```
### 设置###
log4j.rootLogger = debug,stdout,D,E

### 输出信息到控制抬 ###
log4j.appender.stdout = org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target = System.out
log4j.appender.stdout.layout = org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern = [%-5p] %d{yyyy-MM-dd HH:mm:ss,SSS} method:%l%n%m%n

### 输出DEBUG 级别以上的日志文件设置 ###
log4j.appender.D = org.apache.log4j.DailyRollingFileAppender
log4j.appender.D.File = logfilename.log
log4j.appender.D.Append = true
log4j.appender.D.Threshold = DEBUG 
log4j.appender.D.layout = org.apache.log4j.PatternLayout
log4j.appender.D.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n

### 输出ERROR 级别以上的日志文件设置 ###
log4j.appender.E = org.apache.log4j.DailyRollingFileAppender
log4j.appender.E.File = logfilename.log
log4j.appender.E.Append = true
log4j.appender.E.Threshold = ERROR 
log4j.appender.E.layout = org.apache.log4j.PatternLayout
log4j.appender.E.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n x 
```

 示例代码

```java
	static Logger logger = Logger.getLogger(TestMain.class);
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		System.out.println("yes. i am writting log");
		
		logger.setLevel(Level.DEBUG);
		logger.trace("trace info");
		logger.debug("debug info");
		logger.info("common info");
		logger.error("error info");
	}
```

```java
yes. i am writting log
[DEBUG] 2018-03-29 10:52:24,435 method:log4j.TestMain.main(TestMain.java:22)
debug info
[INFO ] 2018-03-29 10:52:24,435 method:log4j.TestMain.main(TestMain.java:23)
common info
[ERROR] 2018-03-29 10:52:24,435 method:log4j.TestMain.main(TestMain.java:24)
error info
```

