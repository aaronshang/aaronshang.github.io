---
layout: post
title: LMAlertView控件分析
categories: [iOS]
description: 分析控件
keywords: 控件
---

分析目标：

1. 如何呈现与`AlertView`控件相似的`Cancel`和`OK`背景效果（潜在方案，做图或UIImageView单像素呈现）
2. 如何呈现模态对话框（潜在方案，view controller的present或window自定义）
3. Title和Message如何布局（默认还是动态调整）
4. 如何实现自定义view的加载

> github地址：[LMAlertView](https://github.com/lmcd/LMAlertView)

答案：

1. 如何绘制背景线

   view绘制，设高为1px。

2. 如何呈现模态

   采用自定义window。具体细节见下方。

3. Title和Message布局方式

   硬编码。

4. 如何自定义View

   通过UIViewAutoresizingFlexibleTopMargin等自动布局保持相对位置。具体细节见下方。

代码赏析：

变参：

```objective-c
 va_list args;
 va_start(args, otherButtonTitles);
 newOtherButtonTitles = [[NSMutableArray alloc] initWithObjects:otherButtonTitles, nil];
            id obj;
            while ((obj = va_arg(args, id)) != nil) {
                [newOtherButtonTitles addObject:obj];
            }
 va_end(args);
```

模态对话框：

Step-1 将当前窗口颜色稍稍置暗

```objective-c
	self.window = [[UIWindow alloc] initWithFrame:[appDelegate window].frame];
	self.window.tintColor = self.tintColor;
```

Step-2 自定义window

```objective-c
LMEmbeddedViewController *viewController = [[LMEmbeddedViewController alloc] init];
	viewController.alertView = self;

	self.window.rootViewController = viewController;
	
	// Without this, the alert background will appear black on rotation
	self.window.backgroundColor = [UIColor clearColor];
	// Same window level as regular alert views (above main window and status bar)
	self.window.windowLevel = UIWindowLevelAlert;
	self.window.hidden = NO;

    [self transformAlertContainerViewForOrientation];

	[self.window makeKeyAndVisible];
	
	if (self.controller == nil) {
		viewController.view = self.alertContainerView;
	}
	else {
		UIViewController *viewController2 = [[UIViewController alloc] init];
		viewController2.view = self.alertContainerView;
		
		// We fake "present" this view controller so it can be dismissed elswhere
		[viewController presentViewController:viewController2 animated:NO completion:nil];
		
		[viewController2 addChildViewController:self.controller];
	}
	
```

Button如何布局位置

```objective-c
_buttonTableView = [self tableViewWithFrame:CGRectMake(0.0, yOffset, alertWidth, tableHeight)];
...
//通过UIViewAutoresizingFlexibleTopMargin，自动调整与superView高度，保持与底部距离不变
tableView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleTopMargin;
```



> UIViewAutoresizingNone就是不自动调整。
> UIViewAutoresizingFlexibleLeftMargin 自动调整与superView左边的距离，保证与superView右边的距离不变。
> UIViewAutoresizingFlexibleRightMargin 自动调整与superView的右边距离，保证与superView左边的距离不变。
> UIViewAutoresizingFlexibleTopMargin 自动调整与superView顶部的距离，保证与superView底部的距离不变。
> UIViewAutoresizingFlexibleBottomMargin 自动调整与superView底部的距离，也就是说，与superView顶部的距离不变。
> UIViewAutoresizingFlexibleWidth 自动调整自己的宽度，保证与superView左边和右边的距离不变。
> UIViewAutoresizingFlexibleHeight 自动调整自己的高度，保证与superView顶部和底部的距离不变。
> UIViewAutoresizingFlexibleLeftMargin  |UIViewAutoresizingFlexibleRightMargin 自动调整与superView左边的距离，保证与左边的距离和右边的距离和原来距左边和右边的距离的比例不变。比如原来距离为20，30，调整后的距离应为68，102，即68/20=102/30。

