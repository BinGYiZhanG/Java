* 能否在一个```Java```应用程序出现2个以上的无限循环呢？
  * ```代码/例子1```中的```Demo03.java```实现了
```
175
张一冰
张一冰
要长到
张一冰
175
张一冰
要长到
张一冰
175
张一冰
要长到
张一冰
175
张一冰
要长到
张一冰
175
张一冰
要长到
张一冰
175
张一冰
要长到
张一冰
175
张一冰
要长到
张一冰
175
张一冰
要长到
要长到
张一冰
175
张一冰
要长到
张一冰
175
175
张一冰
要长到
175
要长到
175
要长到
175
要长到
175
要长到
175
要长到
175
要长到
要长到
175
要长到
175
要长到
175

自己写的输出的并不好

```

### 习题12
#### 1，问答题
##### （1），线程有几种状态？
* （P361）
* 新建
* 运行
* 中断
* 死亡

##### （2），引起线程中断的常见原因是什么？
* P361
* 


##### （3），一个线程执行完```run```方法后，进入了什么状态？该线程还能再调用```start```方法吗？
* 第一问不知答案，死亡状态
* 在线程没有结束```run()```方法之前，不要让线程再调用```start()```方法，否则将发生```IllegalThreadStateException```异常

##### （4），线程在什么状态时调用```isAlive()```方法返回的值是```false```?
* 线程处于新建状态时，线程调用```isAlive()```方法返回```false```
* 在线程的```run()```方法结束之前，即没有进入死亡状态之前，线程调用```isAlive()```方法返回```true```
* 当线程进入死亡状态后（实体内存被释放），线程仍可以调用方法```isAlive()```，这时返回的值是```false```


##### （5），建立线程有几种方法？
* P365
* 在```Java```语言中，用```Thread```类或子类创建线程对象

##### （6），怎样设置线程的优先级？
* P364
* 线程的优先级可以通过```setPriority(int grade)```方法调整

##### （7），在多线程中，为什么要引入同步进制？
* 当两个或多个线程同时访问同一个变量，并且一些线程需要修改这个变量（P373）

##### （8），在什么方法中```wait()```方法，```notify()```及```notifyAll()```方法可以被使用？
* P375
* 

##### （9），在例子6中```SellTicket```类中的循环条件```while(fiveAmount<3)```改写成```if(fiveAmount<3)```是否合理？


##### （10），线程调用```interrupt()```的作用是什么？
* P372
* ```interrupt```方法经常用来“吵醒”休眠的线程

#### 2，选择题
##### （1），哪个叙述是错误的？ A
* A，线程新建后，不调用```start```方法也有机会获得```CPU```资源
* B，如果两个线程需要调用同一个同步方法，那么一个线程调用该同步方法时，另一个线程必须等待
* C，目标对象中的```run```方法可能不启动多次
* D，默认情况下，所有线程的优先级都是5级

##### （2），正确的是
* A，JVM认这个应用程序共有两个线程
* B，JVM认为这个应该程序只有一个主线程
* C，JVM认为这个应该程序只有一个thread线程

```Target.java
class Target implements Runnable{
 public void run(){
  System.out.println("ok");	
 }	
}

```

```test2_2.java
public class test2_2{
	public static void main(String args[]){
		Target target = new Target();
		Thread thread = new Thread(target);
		thread.start();		
	}
}


```


##### （3），第（2）题与第（3）题没差别


#### 3，阅读程序
##### （1），程序有两个线程：主线程和thread线程

* 注意```yes ok```的输出顺序

```
public class E{
	public static void main(String args[]){
		Target target = new Target();
		Thread thread = new Thread(target);
		thread.start();
		for(int i=0;i<=10;i++){
			System.out.println("Yes");
			try{
					Thread.sleep(1000);	
			}	
			catch(InterruptedException exp){}
		}	
	}	
	
}

class Target implements Runnable{
	public void run(){
		for(int i=0;i<=10;i++){
			System.out.println("ok");
			try{
					Thread.sleep(1000);	
			}	
			catch(InterruptedException exp){}
		}	
	}	
}

Out:

Yes
ok
ok
Yes
ok
Yes
ok
Yes
ok
Yes
ok
Yes
ok
Yes
ok
Yes
ok
Yes
ok
Yes
ok
Yes

```


##### （2），注意该程序中只有一个主线程，```thread```线程并没有启动

* 这个线程直接```run```，没有```start```

```
public class E{
	public static void main(String args[]){
		Target target = new Target();
		Thread thread = new Thread(target);
		thread.run();
		for(int i=0;i<=10;i++){
			System.out.println("Yes");
			try{
					Thread.sleep(1000);	
			}	
			catch(InterruptedException exp){}
		}	
	}	
	
}

class Target implements Runnable{
	public void run(){
		for(int i=0;i<=10;i++){
			System.out.println("ok");
			try{
					Thread.sleep(1000);	
			}	
			catch(InterruptedException exp){}
		}	
	}	
}

Out:
ok
ok
ok
ok
ok
ok
ok
ok
ok
ok
ok
Yes
Yes
Yes
Yes
Yes
Yes
Yes
Yes
Yes
Yes
Yes


```

##### （3），注意程序的输出结果
```
public class E{
	public static void main(String args[]){
		Target target = new Target();
		Thread thread1 = new Thread(target);
		Thread thread2 = new Thread(target);
		thread1.start();
		try{
			Thread.sleep(1000);
		}
		catch(Exception exp){}
		thread2.start();
	}	
	
}


class Target implements Runnable{
	int i=0;
	public void run(){
		i++;
		System.out.println("i="+i);	
	}
}

Out:
i=1
i=2


```

##### （4），注意与（3）的不同


```
public class E{
	public static void main(String args[]){
		Target target1 = new Target();
		Target target2 = new Target();
		Thread thread1 = new Thread(target1);
		Thread thread2 = new Thread(target2);
		thread1.start();
		try{
			Thread.sleep(1000);
		}
		catch(Exception exp){}
		thread2.start();
	}	
	
}

class Target implements Runnable{
	int i=0;
	public void run(){
		i++;
		System.out.println("i="+i);	
	}
}

Out:

i=1
i=1

```

##### （5），计时器启动成功

```
import javax.swing.*;
import java.util.Date;

public class Ex{
	public static void main(String args[]){
		javax.swing.Timer time = new javax.swing.Timer(500,new A());
		time.setInitialDelay(0);
		time.start();	
	}	
}

class A extends JLabel implements java.awt.event.ActionListener{
	public void actionPerformed(java.awt.event.ActionEvent e){
		System.out.println(new Date());	
	}	
}

Out:
C:\Users\Administrator\Desktop\正在学\Java\习题代码\ch12\3，阅读程序>java Ex
Fri Oct 18 20:25:16 CST 2019
Fri Oct 18 20:25:17 CST 2019
Fri Oct 18 20:25:17 CST 2019
Fri Oct 18 20:25:18 CST 2019
Fri Oct 18 20:25:18 CST 2019
Fri Oct 18 20:25:19 CST 2019
Fri Oct 18 20:25:19 CST 2019
Fri Oct 18 20:25:20 CST 2019
Fri Oct 18 20:25:20 CST 2019
Fri Oct 18 20:25:21 CST 2019
Fri Oct 18 20:25:21 CST 2019
Fri Oct 18 20:25:22 CST 2019
Fri Oct 18 20:25:22 CST 2019
Fri Oct 18 20:25:23 CST 2019
Fri Oct 18 20:25:23 CST 2019
Fri Oct 18 20:25:24 CST 2019
Fri Oct 18 20:25:24 CST 2019
Fri Oct 18 20:25:25 CST 2019

```


##### （5），计时器启动失败

```
import javax.swing.*;
import java.util.Date;

public class Ex{
	public static void main(String args[]){
		javax.swing.Timer time = new javax.swing.Timer(500,new A());
		time.setInitialDelay(0);
		time.start();	
	}	
}

class A implements java.awt.event.ActionListener{
	public void actionPerformed(java.awt.event.ActionEvent e){
		System.out.println(new Date());	
	}	
}


Out:
C:\Users\Administrator\Desktop\正在学\Java\习题代码\ch12\3，阅读程序>javac Ex.java

C:\Users\Administrator\Desktop\正在学\Java\习题代码\ch12\3，阅读程序>java Ex


```


##### （7），

```
import java.awt.*;
import java.awt.event.*;

public class E implements Runnable{
	StringBuffer buffer = new StringBuffer();
	Thread t1,t2;
	E(){	t1 = new Thread(this);
		t2 = new Thread(this);
	}

	public synchronized void addChar(char c){
		if(Thread.currentThread() == t1){
			while(buffer.length() == 0){
				try{
						wait();	
				}	
				catch(Exception e){};
			}
			buffer.append(c);	
		}	
		if(Thread.currentThread()==t2){
			buffer.append(c);
			notifyAll();	
		}
	}

	public static void main(String args[]){
		E hello = new E();
		hello.t1.start();
		hello.t2.start();
		while(hello.t1.isAlive()||hello.t2.isAlive()){}
		System.out.println(hello.buffer);
	}	
	public void run(){
		if(Thread.currentThread()==t1)
			addChar('A');
		if(Thread.currentThread()==t2)
			addChar('B');	
	}
	
}

Out:
BA


```

##### （8），
```
import java.awt.*;
import java.awt.event.*;

public class E{
	public static void main(String args[]){
		Bank b = new Bank();
		b.thread1.start();
		b.thread2.start();
	}	
		
}

class Bank implements Runnable{
	Thread thread1,thread2;
	Bank(){
		thread1 = new Thread(this);
		thread2 = new Thread(this);	
	}

	public void run(){
		printMess();	
	}

	public void printMess(){
		System.out.println(Thread.currentThread().getName()+"正在使用这个方法");
		synchronized(this){
			try{
				Thread.sleep(2000);	
			}	
			catch(Exception exp){}
			System.out.println(Thread.currentThread().getName()+"正在使用这个同步块");
		}	
	}
			
}

Out:
Thread-0正在使用这个方法
Thread-1正在使用这个方法
Thread-0正在使用这个同步块
Thread-1正在使用这个同步块

```

#### 4，编程题
##### （1），
```
public class TicketHouse implements Runnable {
   int fiveAmount=3,tenAmount=0,twentyAmount=0; 
   public void run() {
      if(Thread.currentThread().getName().equals("张飞")) {
          saleTicket(20);
      }
      else if(Thread.currentThread().getName().equals("李逵")) {
          saleTicket(10);
      }
      else if(Thread.currentThread().getName().equals("赵敏")) {
          saleTicket(5);
      }
   }
   private synchronized void saleTicket(int money) {
       if(money==5) {  //如果使用该方法的线程传递的参数是5,就不用等待
        fiveAmount=fiveAmount+1; 
        System.out.println( "给"+Thread.currentThread().getName()+"入场卷,"+
                            Thread.currentThread().getName()+"的钱正好");
       }
       else if(money==10){
       		while(fiveAmount<1) {
            try { System.out.println("\n"+Thread.currentThread().getName()+"靠边等...");
                  wait();       //如果使用该方法的线程传递的参数是20须等待
                  System.out.println("\n"+Thread.currentThread().getName()+"继续买票");
            }
            catch(InterruptedException e){}
         }
         fiveAmount=fiveAmount-1;
         tenAmount=tenAmount+1;
         System.out.println("给"+Thread.currentThread().getName()+"入场卷,"+
                            Thread.currentThread().getName()+"给10，找赎5元");
       }
       else if(money==20) {           
         while(fiveAmount<1||tenAmount<1) {
            try { System.out.println("\n"+Thread.currentThread().getName()+"靠边等...");
                  wait();       //如果使用该方法的线程传递的参数是20须等待
                  System.out.println("\n"+Thread.currentThread().getName()+"继续买票");
            }
            catch(InterruptedException e){}
         }
         fiveAmount=fiveAmount-1;
         tenAmount=tenAmount-1;
         twentyAmount=twentyAmount+1;
         System.out.println("给"+Thread.currentThread().getName()+"入场卷,"+
                            Thread.currentThread().getName()+"给20，找赎15元");
       }
       
       
       notifyAll();
   } 
}


public class test_001 {
   public static void main(String args[ ]) {
      TicketHouse officer = new TicketHouse();
      Thread zhangfei,likui,zhaomin;
      zhangfei = new Thread(officer); 
      zhangfei.setName("张飞");
      likui = new Thread(officer);  
      likui.setName("李逵");
      zhaomin = new Thread(officer);
      zhaomin.setName("赵敏");
      zhangfei.start();
      likui.start();
      zhaomin.start();
   }
}


Out:
张飞靠边等...
给李逵入场卷,李逵给10，找赎5元
给赵敏入场卷,赵敏的钱正好

张飞继续买票
给张飞入场卷,张飞给20，找赎15元

我的理解是：
找15块给张飞
让李逵靠边等
给赵敏入场券
李逵钱正好

而答案的意思在输出中已经很明确了

```

##### （2），
```
public class ClassRoom implements Runnable {
   Thread  student1,student2,teacher;
   ClassRoom() {
       teacher=new Thread(this); 
       student1=new Thread(this); 
       student2=new Thread(this);
       teacher.setName("王教授");
       student1.setName("张三");
       student2.setName("李四");
   } 
   public void run(){     
      if(Thread.currentThread()==student1) {
         try{  System.out.println(student1.getName()+"正在睡觉，不听课");
               Thread.sleep(1000*60*10);
         }
         catch(InterruptedException e) {
              System.out.println(student1.getName()+"被老师叫醒了");
         }
         System.out.println(student1.getName()+"开始听课");
         student2.interrupt();           //吵醒student
       }
       else if(Thread.currentThread()==student2) {
       	try{  System.out.println(student2.getName()+"正在睡觉，不听课");
               Thread.sleep(1000*60*60);
         }
         catch(InterruptedException e) {
              System.out.println(student2.getName()+"被"+student1.getName()+"叫醒了");
         }
         System.out.println(student2.getName()+"开始听课");
       
     }
      else if(Thread.currentThread()==teacher)  {
         for(int i=1;i<=3;i++) {
            System.out.println("上课!");
            try{ Thread.sleep(500);
            }
            catch(InterruptedException e){} 
         }
         student1.interrupt();           //吵醒student
      }
   }
}


public class test_002 {
   public static void main(String args[]) {
      ClassRoom room6501=new ClassRoom();
      room6501.student1.start();
      room6501.student2.start();
      room6501.teacher.start();
   }
}


Out:
上课!
李四正在睡觉，不听课
张三正在睡觉，不听课
上课!
上课!
张三被老师叫醒了
张三开始听课
李四被张三叫醒了
李四开始听课


```

##### （3），

