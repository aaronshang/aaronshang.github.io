---
layout: post
title: 串口访问
categories: [网络技术]
description: 
keywords: 网络
---



### 1 简介

串口通信

> Serial Communication，串口按位发送和接收字节。

重要参数

> 波特率：衡量符合传输速率的参数。
>
> 数据位：衡量通信中实际数据位的参数。
>
> 停止位：用于表示单个包的最后一位。
>
> 奇偶校验位：检错方式。

### 2 VC++串口编程

#### 2.1 打开串口

```c++
HANDLE CreateFile( LPCTSTR lpFileName, DWORD dwDesiredAccess, DWORD dwShareMode, LPSECURITY_ATTRIBUTES lpSecurityAttributes, DWORD dwCreationDistribution, DWORD dwFlagsAndAttributes, HANDLE hTemplateFile);    
       lpFileName：将要打开的串口逻辑名，如“COM1”；
       dwDesiredAccess：指定串口访问的类型，可以是读取、写入或二者并列； 
       dwShareMode：指定共享属性，由于串口不能共享，该参数必须置为0； 
       lpSecurityAttributes：引用安全性属性结构，缺省值为NULL； 
       dwCreationDistribution：创建标志，对串口操作该参数必须置为OPEN_EXISTING； 
       dwFlagsAndAttributes：属性描述，用于指定该串口是否进行异步操作，该值为FILE_FLAG_OVERLAPPED，表示使用异步的I/O；该值为0，表示同步I/O操作；
       hTemplateFile：对串口而言该参数必须置为NULL。
```

#### 2.2 配置串口

```c++
typedef struct _DCB{ ……… 
DWORD BaudRate;//波特率，指定通信设备的传输速率。这个成员可以是实际波特率值或者下面的常量值之一：  CBR_110，CBR_300，CBR_600，CBR_1200，CBR_2400，CBR_4800，CBR_9600，CBR_19200， CBR_38400， CBR_56000， CBR_57600， CBR_115200， CBR_128000， CBR_256000， CBR_14400
DWORD fParity; // 指定奇偶校验使能。若此成员为1，允许奇偶校验检查 …
BYTE ByteSize; // 通信字节位数，4—8
BYTE Parity; //指定奇偶校验方法。此成员可以有下列值： EVENPARITY 偶校验 NOPARITY 无校验 MARKPARITY 标记校验 ODDPARITY 奇校验
BYTE StopBits; //指定停止位的位数。此成员可以有下列值： ONESTOPBIT 1位停止位 TWOSTOPBITS 2位停止位
ON 5STOPBITS   1.5位停止位
```

​	在查询和配置串口的属性时，用DCB结构来作为缓冲区。

​	一般在打开串口后，先用`GetCommState`函数来获取串口的初始配置。要修改串口配置，要修改DCB结构。然后再调用`SetCommState`函数来设置串口。

​	除了BCD设置外，程序一般还需`SetupComm`函数设置`I/O缓冲区的大小`和`超时`。

```c++
BOOL SetupComm( HANDLE hFile, // 通信设备的句柄 
            DWORD dwInQueue, // 输入缓冲区的大小（字节数） 
            DWORD dwOutQueue // 输出缓冲区的大小（字节数） ); 
```

​	用`ReadFile`和`WriteFile`读写串口时，需要考虑超时问题。超时分间隔超时和总超时。`间隔超时`是在接收时两个字符的最大时延。`总超时`指读写操作总花费的最大时间。写操作只支持总超时，而读操作支持两种。

```c++
typedef struct _COMMTIMEOUTS { 
         DWORD ReadIntervalTimeout; //读间隔超时
         DWORD ReadTotalTimeoutMultiplier; //读时间系数
         DWORD ReadTotalTimeoutConstant; //读时间常量
         DWORD WriteTotalTimeoutMultiplier; // 写时间系数
         DWORD WriteTotalTimeoutConstant; //写时间常量
} COMMTIMEOUTS,*LPCOMMTIMEOUTS; 
COMMTIMEOUTS结构的成员都以毫秒为单位。
总超时的计算公式是：总超时＝时间系数×要求读/写的字符数＋时间常量
```

​	如果所有写超时参数设为0，则不使用写超时。

​	如果读间隔超时设为`MAXWORD`并且读时间系数和读时间常量都为0，则在读一次输入缓冲区的内容后读操作就立即返回，而不管是否读了要求的字符。

示例代码

```c++
 SetupComm(hCom,1024,1024); //输入缓冲区和输出缓冲区的大小都是1024 
    COMMTIMEOUTS TimeOuts; //设定读超时
    TimeOuts.ReadIntervalTimeout=1000;
    TimeOuts.ReadTotalTimeoutMultiplier=500;
    TimeOuts.ReadTotalTimeoutConstant=5000; //设定写超时
    TimeOuts.WriteTotalTimeoutMultiplier=500;
    TimeOuts.WriteTotalTimeoutConstant=2000;
    SetCommTimeouts(hCom,&TimeOuts); //设置超时
    DCB dcb; 
    GetCommState(hCom,&dcb);
    dcb.BaudRate=9600; //波特率为9600
    dcb.ByteSize=8; //每个字节有8位
    dcb.Parity=NOPARITY; //无奇偶校验位
    dcb.StopBits=TWOSTOPBITS; //两个停止位
    SetCommState(hCom,&dcb);
    PurgeComm(hCom,PURGE_TXCLEAR|PURGE_RXCLEAR); 
```

​	读写串口前，要调用`PurgeComm()`清空缓冲区。

```
    BOOL PurgeComm( HANDLE hFile, //串口句柄 
                DWORD dwFlags // 需要完成的操作 ); 
参数dwFlags指定要完成的操作，可以是下列值的组合： 
    PURGE_TXABORT 中断所有写操作并立即返回，即使写操作还没有完成。 
    PURGE_RXABORT 中断所有读操作并立即返回，即使读操作还没有完成。 
    PURGE_TXCLEAR 清除输出缓冲区   
    PURGE_RXCLEAR 清除输入缓冲区 
```

#### 2.4 读写串口

​	读写串口时，读写可以同步执行，也可以重叠执行。`重叠执行`时，即使操作还未完成，这两个函数也会立即返回，费时的I/O操作在后台进行。是否重叠，由`FILE_FLAG_OVERLAPPED`标志指定。

​	重叠操作时，线程需要创建`OVERLAPPED`结构以供这两个函数使用。其中`hEvent`是读写事件。当调用`ReadFile`和`WriteFile`函数的时候，该成员置为无信号状态；重叠完成后，该成员变量会自动被置为有信号状态。

​	异步读示例代码

```C++
char lpInBuffer[1024]; 
DWORD dwBytesRead=1024; 
COMSTAT ComStat; 
DWORD dwErrorFlags; 
OVERLAPPED m_osRead; 
memset(&m_osRead,0,sizeof(OVERLAPPED)); 
m_osRead.hEvent=CreateEvent(NULL,TRUE,FALSE,NULL); 
ClearCommError(hCom,&dwErrorFlags,&ComStat); 
dwBytesRead=min(dwBytesRead,(DWORD)ComStat.cbInQue); 
if(!dwBytesRead) return FALSE; 
BOOL bReadStatus; 
bReadStatus=ReadFile(hCom,lpInBuffer, dwBytesRead,&dwBytesRead,&m_osRead);
if(!bReadStatus) 
//如果ReadFile函数返回FALSE 
{ 
    if(GetLastError()==ERROR_IO_PENDING) 
    //GetLastError()函数返回ERROR_IO_PENDING,表明串口正在进行读操作 
    { 
        WaitForSingleObject(m_osRead.hEvent,2000); 
        //使用WaitForSingleObject函数等待，直到读操作完成或延时已达到2秒钟 
        //当串口读操作进行完毕后，m_osRead的hEvent事件会变为有信号 
        PurgeComm(hCom, PURGE_TXABORT| PURGE_RXABORT|PURGE_TXCLEAR|PURGE_RXCLEAR); 
        return dwBytesRead; 
    }
    return 0; 
}
PurgeComm(hCom, PURGE_TXABORT| PURGE_RXABORT|PURGE_TXCLEAR|PURGE_RXCLEAR); 
return dwBytesRead; 
```

#### 2.4 关闭串口

```c++
BOOL CloseHandle(
    HANDLE hObject; //handle to object to close
);
```

