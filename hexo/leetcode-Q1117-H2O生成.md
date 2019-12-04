---
title: leetcode Q1117 H2O生成
date: 2019-10-13 16:26:43
tags:
	--leetcode
---
题目链接:https://leetcode-cn.com/problems/building-h2o/  

关键代码如下:

/*
 *	执行用时 :16 ms, 在所有 java 提交中击败了94.77%的用户
 *	内存消耗 :36.9 MB, 在所有 java 提交中击败了100.00%的用户
 * */
```java
public H2O() { }
		
volatile int hnum = 0;
volatile int onum = 0;

public void hydrogen(Runnable releaseHydrogen) throws InterruptedException {
	while(hnum/2 > onum) {
	    Thread.yield();
	}
	    	
	// releaseHydrogen.run() outputs "H". Do not change or remove this line.
	releaseHydrogen.run();
		    
	hnum++;
}

public void oxygen(Runnable releaseOxygen) throws InterruptedException {
	while(onum > hnum/2) {
		Thread.yield();
	}
	    	
	// releaseOxygen.run() outputs "O". Do not change or remove this line.
	releaseOxygen.run();
			
	onum++;
}
```

使用hnum和onum对线程执行次数进行记录  
当线程当前不应该输出"O"或者"H"时,使用yeild()方法保证当前线程让出并让另一个线程继续运行  

注意:不要将releaseHydrogen.run()方法放在循环当中,这可能会导致程序超时
例如:  
```java
for(int i = 0;i < 2;i++){				//将会导致程序超时
	// releaseHydrogen.run() outputs "H". Do not change or remove this line.
	releaseHydrogen.run();
}
```