---
layout: post
title: Lock
categories: [计算机]
description: 
keywords: Lock
---

```c++
class LockImpl
{
public:
	LockImpl();
	~LockImpl();
public:
	void Lock();
	void Unlock();
private:
	NativeHandle os_lock_;
};
```

```c++
#ifdef WIN32
typedef CRITICAL_SECTION NativeHandle;
#else
#include <pthread.h>
#include <errno.h>
typedef pthread_mutex_t NativeHandle;
#endif
```

> critical section, 是每个线程中访问临界资源的那段代码，不论是硬件资源，还是软件资源，多个线程必须互斥的对它进行访问。
>
> 临界区在使用时以`CRITICAL_SECTION`结构对象保护共享资源，并分别用`EnterCriticalSection()`和`LeaveCriticalSection()`函数去标识和释放一个临界区。所用到的`CRITICAL_SECTION`结构对象必须经过`InitializeCriticalSection()`的初始化才可以使用。

