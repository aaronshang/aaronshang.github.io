---
layout: post
title: RATreeView(2.1.0) Bug
categories: [iOS]
description: some word here
keywords: RATreeView
---



摘要：RATreeView（2.1.0）Bug及解决方法。

问题1：

​	当有的Row处于展开状态时，调用`ReloadData`，所有Row自动收缩。

问题2：

​	当有的Row处于展开状态时，调用`insertItemAtIndex`，位置错乱



问题1解决方法：

1. 尽量不调用reloadData，采用insert、expand等动作函数
2. 调用reloadData后，针对之前展开的item进行`expand`调用，item需要事先记住

问题2解决方法：

1. 调用Reload方法替代

2. 修改源码文件

   源文件问题代码为：

   ```objective-c
    NSIndexPath *indexPath = [NSIndexPath indexPathForRow:idx inSection:0];
   ```

   改为：

   ```objective-c
      id item = [weakSelf.treeNodeCollectionController childInParent:parent atIndex:index];
       NSIndexPath *indexPath = [weakSelf indexPathForItem:item];
   ```

   位置：

```objective-c
- (void)insertItemAtIndex:(NSInteger)index inParent:(id)parent withAnimation:(RATreeViewRowAnimation)animation
{
  NSInteger idx = [self.treeNodeCollectionController indexForItem:parent];
  if (idx == NSNotFound) {
    return;
  }
  idx += index + 1;
  
  __weak typeof(self) weakSelf = self;
  [self.batchChanges insertItemWithBlock:^{
    [weakSelf.treeNodeCollectionController insertItemsAtIndexes:[NSIndexSet indexSetWithIndex:index] inParent:parent];
    
//    NSIndexPath *indexPath = [NSIndexPath indexPathForRow:idx inSection:0];
    id item = [weakSelf.treeNodeCollectionController childInParent:parent atIndex:index];
    NSIndexPath *indexPath = [weakSelf indexPathForItem:item];
      
    UITableViewRowAnimation tableViewRowAnimation = [RATreeView tableViewRowAnimationForTreeViewRowAnimation:animation];
    [weakSelf.tableView insertRowsAtIndexPaths:@[indexPath] withRowAnimation:tableViewRowAnimation];
    
  } atIndex:idx];
}
```

