---
layout: post
title: 设计模式
categories: [计算机]
description: 
keywords: 设计模式
---

### 总序

> 设计模式有接口型模式、责任链模式、构造型模式、操作型模式、扩展型模式。

### 责任链模式

> 一种对象的行为模式。含`抽象处理者角色`。
>
> 一个纯的责任链模式要求一个具体的处理者对象只能在两个行为中选择一个：一个承担责任，二是把责任推给下家。

#### 何时使用责任链模式

> 第一，系统有一个处理者对象组成的链。第二，当多于一个处理者对象会处理一个请求，而事先并不知道到底有哪个处理者对象处理一个请求。第三，当系统想发出一个请求给多个处理者对象中的某一个，但是不明显指定。第四，当处理一个请求的处理者对象集合需要动态的指定时。

#### 角色组成![](http://shangkai007.top/images/design-pattern/dp-chain-of-responsibility-compent.png)

Java代码示例

```java
public abstract class AbstractLogger {

	public static int INFO = 1;
	public static int DEBUG = 2;
	public static int ERROR = 3;
	
	protected int level;
	protected AbstractLogger nextLogger;
	
	public void setNextLogger(AbstractLogger nextLogger){
		this.nextLogger = nextLogger;
	}
	
	public void logMessage(int level, String message){
		if(this.level <= level){
			write(message);
		}
		if(nextLogger != null){
			nextLogger.logMessage(level, message);
		}
	}
	
	abstract protected void write(String message);
}
```

```java
public class ConsoleLogger extends AbstractLogger {

	public ConsoleLogger(int level){
		this.level = level;
	}
	@Override
	protected void write(String message) {
		// TODO Auto-generated method stub
		System.out.println("Standard Console::Logger:"+message);
	}

}
```

```java
public class ErrorLogger extends AbstractLogger {

	public ErrorLogger(int level){
		this.level = level;
	}
	@Override
	protected void write(String message) {
		// TODO Auto-generated method stub
		System.out.println("Error Console::Logger:: "+message);
	}

}
```

```java
public class FileLogger extends AbstractLogger {

	public FileLogger(int level){
		this.level = level;
	}
	@Override
	protected void write(String message) {
		// TODO Auto-generated method stub
		System.out.println("File::Logger: "+message);
	}

}
```

```java
public class ChainPatternDemo {
	
	private static AbstractLogger getChainOfLoggers(){
		AbstractLogger errorLogger = new ErrorLogger(AbstractLogger.ERROR);
		AbstractLogger fileLogger = new FileLogger(AbstractLogger.DEBUG);
		AbstractLogger consoleLogger = new ConsoleLogger(AbstractLogger.INFO);
		errorLogger.setNextLogger(fileLogger);
		fileLogger.setNextLogger(consoleLogger);
		return errorLogger;
	}
	
	public static void main(String[] args){
		
		System.out.println("ChainPatternDemo");
		AbstractLogger logChain = getChainOfLoggers();
		logChain.logMessage(AbstractLogger.INFO,  "Info");
		logChain.logMessage(AbstractLogger.DEBUG, "Debug");
		logChain.logMessage(AbstractLogger.ERROR, "Error");
	}
}
```

```java
ChainPatternDemo
Standard Console::Logger:Info
File::Logger: Debug
Standard Console::Logger:Debug
Error Console::Logger:: Error
File::Logger: Error
Standard Console::Logger:Error
```



