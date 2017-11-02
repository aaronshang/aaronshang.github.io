---
layout: post
title: 设计模式
categories: [计算机]
description: 
keywords: 设计模式
---

### 简介

> 设计莫模式代表了最佳的实践。为了重用代码、让代码更容易被理解、保证代码可靠性。
>
> 设计模式主要有三大类，创建型模式、结构型模式、行为型模式。
>
> 设计原则：
>
> 1. 对接口编程而不是对实现编程
> 2. 优先使用对象组合而不是继承

### 综述

创建型模式：

> 创建对象同时隐藏创建逻辑的方式。

1. 工厂模式（Factory Pattern）
2. 抽象工厂模式（Abstract Factory Pattern）
3. 单例模式（Singleton Pattern）
4. 建造者模式（builder Pattern）
5. 原型模式（Prototype Pattern）

结构型模式：

> 关注类和对象的组合。

1. 适配器模式（Adapter Pattern）
2. 桥接模式（Bridge Pattern）
3. 过滤器模式（Filter、Criteria Pattern）
4. 组合模式（Composite Pattern）
5. 装饰器模式（Decorator Pattern）
6. 外观模式（Facade Pattern）
7. 享元模式（Flyweight Pattern）
8. 代理模式（Proxy Pattern）

行为型模式：

> 特别关注对象之间的通信。

1. 责任链模式（Chain of Responsibility Pattern）
2. 命令模式（Command Pattern）
3. 解释器模式（Interpreter Pattern）
4. 迭代器模式（Iterator Pattern）
5. 中介者模式（Mediator Pattern）
6. 备忘录模式（Memento Pattern）
7. 观察者模式（Observer Pattern）
8. 状态模式（State Pattern）
9. 空对象模式（Null Object Pattern）
10. 策略模式（Strategy Pattern）
11. 模板模式（Template Pattern）
12. 访问者模式（Visitor Pattern）

J2EE模式

> 特别关注表示层。

1. MVC模式
2. 业务代表模式
3. 组合实体模式
4. 数据访问对象模式
5. 前端控制器模式
6. 拦截过滤器模式
7. 服务定位器模式
8. 传输对象模式

### 责任链模式

> 一种对象的行为模式。含`抽象处理者角色`。
>
> 一个纯的责任链模式要求一个具体的处理者对象只能在两个行为中选择一个：一个承担责任，二是把责任推给下家。

#### 场景

> 第一，系统有一个处理者对象组成的链。第二，当多于一个处理者对象会处理一个请求，而事先并不知道到底有哪个处理者对象处理一个请求。第三，当系统想发出一个请求给多个处理者对象中的某一个，但是不明显指定。第四，当处理一个请求的处理者对象集合需要动态的指定时。

#### 角色组成

[责任链模式组成]()

UML示例

[责任链模式UML](http://shangkai007.top/images/design-pattern/dp-chain-uml.png)

### 命令模式

> 行为型模式。请求以命令的形式包裹在对象中，并传给调用对象。调用对象寻找可以处理该命令的对象，并交由响应的对象执行命令。

#### 场景

> 将一个请求封装成一个对象，从而用不同的请求对客户进行参数化。解决`行为请求者`和`行为实现者`之间的松耦合。

UML示例

[命令模式UML](http://shangkai007.top/images/design-pattern/dp-command-uml.png)

### 解释器模式

> 提供了评估语言的语法或表达式的方式。属于行为型模式。这种模式被用在SQL解析、符号处理引擎等。这种模式实现了一个表达式接口，该接口解释一个特定的上下文。

### 迭代器模式

> Java和.net常用的设计模式。用于顺序访问集合对象的元素，不需要知道集合对象的底层表示。属于行为型模式。



> 提供一种方法顺序访问一个聚合对象中各个元素，而又无须暴露该对象的内部表示。

