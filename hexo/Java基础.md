---
title: Java基础
date: 2019-11-12 15:48:03
tags:
	-IT TECH
---
Q:有哪些不同的线程生命周期？
NEW					新建(只出现一次)
TERMINATED			结束/死亡(只出现一次)
RUNNABLE.RUNNING	运行中
RUNNABLE.READY		等待运行
WAITING				线程等待
TIMED_WAITING		线程等待(时限)
BLOCKED				线程阻塞

Q:什么是ThreadLocal?
ThreadLocal是一个线程内部的存储类,可以看作维护一个Map,当前线程为key,每个线程可以内部储存数据,不同线程之间数据相互独立

Q:IO与NIO区别,ByteBuffer相关?
阻塞式IO:在IO未完成时线程阻塞,等待IO完成
非阻塞式IO:在未完成IO时不等待并继续执行语句,并在其他线程轮询IO是否完成,IO完成后在执行IO语句
多路复用IO(NIO):与非阻塞式IO相差不大,但是非阻塞式IO是用户进程轮询,而多路复用IO是系统进程轮询,比非阻塞式IO更快
其他IO方式还有信号驱动式 I/O和异步io

IO面向流,NIO面向缓冲区

Q:Java中的同步集合与并发集合有什么区别?
同步集合:使用synchronized实现同步的集合,如vector,stack和hashtable等
并发集合:使用Java内存模型,volatile,AbstractQueuedSynchronizer(AQS同步器)实现并发的集合,如ConcurrentHashMap,LinkedBlockingQueue等集合

Q:什么是Timer类?
Timer类用于实现延迟执行任务
继承一个TimerTask类并重写run() 并调用Timer.schedule(TimerTask t,args...)来实现延迟执行run()
注意schedule函数有多个重载