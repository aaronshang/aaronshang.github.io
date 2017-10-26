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

#### 场景

> 第一，系统有一个处理者对象组成的链。第二，当多于一个处理者对象会处理一个请求，而事先并不知道到底有哪个处理者对象处理一个请求。第三，当系统想发出一个请求给多个处理者对象中的某一个，但是不明显指定。第四，当处理一个请求的处理者对象集合需要动态的指定时。

#### 角色组成![](http://shangkai007.top/images/design-pattern/dp-chain-of-responsibility-compent.png)

UML示例

![](http://shangkai007.top/images/design-pattern/dp-chain-uml.png)

### 命令模式

> 行为型模式。请求以命令的形式包裹在对象中，并传给调用对象。调用对象寻找可以处理该命令的对象，并交由响应的对象执行命令。

#### 场景

> 将一个请求封装成一个对象，从而用不同的请求对客户进行参数化。解决`行为请求者`和`行为实现者`之间的松耦合。

UML示例



![](http://shangkai007.top/images/design-pattern/dp-command-uml.png)



