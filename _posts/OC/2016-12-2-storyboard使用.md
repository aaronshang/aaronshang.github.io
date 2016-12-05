---
layout: post
title: iOS Storyboard的应用
categories: [iOS]
description: iOS
keywords: Storyboard
---



> storyboard的用法
>
> [优雅使用规范](http://www.cocoachina.com/ios/20160714/17035.html)

问题列表：

1. A-B通过连线连接，B-A若用连线，会创建新的对象，而不是返回？

新建storyboard如何使用？

初始窗体

```swift
let vc = UIStoryboard(name: "Second", bundle: nil).instantiateInitialViewController() as! UIViewController
self.navigationController?.pushViewController(vc, animated: true)
```

设置了storyboard ID

```swift
let vc = UIStoryboard(name: "Second", bundle: nil).instantiateViewControllerWithIdentifier("First") as! UIViewController
self.navigationController?.pushViewController(vc, animated: true)
```