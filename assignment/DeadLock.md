##Lab4死锁 实验报告##

###死锁原因
在多线程编程中，我们通常会有复数个线程在同时进行数据的读写操作。如果多个线程对同一地址的数据进行读写，通常容易发生错误，例如写操作还未完成就开始了数据的读取。
因此我们会设置某些代码段为临界区，同时只能有一个线程运行在临界区，运行在临界区的权利称为锁（资源），当某些线程一直无法拿到资源时，就会产生死锁，下列是死锁的几个原因：

- **因为系统资源不足。**
- **进程运行推进的顺序不合适。**
- **资源分配不当等。**

###死锁的必要条件
下列是产生死锁的四个必要条件：

- **互斥条件：**一个资源每次只能被一个进程使用。
- **请求与保持条件：**一个进程因请求资源而阻塞时，对已获得的资源保持不放。
- **不剥夺条件:**进程已获得的资源，在末使用完之前，不能强行剥夺。
- **循环等待条件:**若干进程之间形成一种头尾相接的循环等待资源关系。

上述条件只要有任何一条不满足，都不会产生死锁。

###实验代码解释 
两个类A和B，其中两个类的方法都被声明为了synchronized，因此对于同一个类的方法（包括构造器），有且仅有一条线程能执行。
   
    class A{
		synchronized void methodA(B b){
			b.last();
		}
		synchronized void last(){
			System.out.println("Inside A.last()");
		}
	}

	class B{
		synchronized void methodB(A a){
			a.last();
		}
		synchronized void last(){
			System.out.println("Inside B.last()");
		}
	}

主类Deadlock实现了多线程编程的Runable接口。构造Deadlock时，会新建一个线程，并运行该线程一次，该线程会通过实例b调用方法methodA。而主线程则隔一段时间调用实例a的methodB方法。
	
	class Deadlock implements Runnable{
		A a = new A();
		B b = new B();
		Deadlock(){
			Thread t = new Thread(this);
			int count = 20000;
			t.start();
			while(count --> 0);
			a.methodA(b);
		}
		public void run(){
			b.methodB(a);
		}
		public static void main(String args[]){
			new Deadlock();
		}
	}

再来看看TA提供的批处理文件。这个批处理文件会连续运行Deadlock这个class文件1000次。在运行过程中会输出当前运行到第几次。

	cd /d %~dp0
	@echo off
	:start
	set /a var+=1
	echo %var%
	java Deadlock
	if %var% leq 1000 GOTO start
	pause

因此实际上，产生死锁的时间是随机的。因为主线程调用a.methodA(b)时，这个方法会调用B类的b.last()函数。但此时另外一个线程也在运行，另外一个线程会调用b.methodB(a)函数，这个函数和b.last()有且仅能有一个被执行。<br>
但基于操作系统调度队列的不同，这个过程具有随机性，只有当主线程while循环结束时，子线程也刚好执行这个函数，才会产生死锁。

###实验结果展示
进入dol文件夹，修改build_zip.xml文件

<img src = "https://raw.githubusercontent.com/Roryfu/ES2016_14353044/master/res/Deadlock/停在79.jpg">

###Experimental experience
JAVA的资源控制实现起来比C语言简单很多，而且在学习了操作系统的相关概念之后，这次实验还是蛮好理解的。不知道死锁的概念用在有嵌入式编程里面是不是还是差不多。