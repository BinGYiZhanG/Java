#### 表3-1 ```Lambda```示例
##### 我的错误代码，输出不了，没理解```Lambda```语句的真正含义
```
public class test3_1{
	
		public static void main(String [] args) throws Exception{
			System.out.println(""+(List<String> list) -> list.isEmpty());
			Apple Test_a=() -> new Apple(10);
			Apple Test_b=() -> new Apple(15);
			
			//消费一个对象
			//(Apple Test_a) -> {
			//	System.out.println("苹果重量："+a.getWeight());
			//}
			
			String s="计算机网络";
			System.out.println("从一个对象中选择/抽取："+(String s) -> s.length());
			
			int a=3,b=5;
			System.out.println("组合两个值："+(int a, int b) -> a * b);
			
			//比较两个对象
			System.out.println("比较两个对象："+(Apple Test_a, Apple Test_b) ->
				Test_a.getWeight().compareTo(Test_b.getWeight()));
		}
    
    

```


#### 3.2 在哪里以及如何使用Lambda
* 对于P39上半页的代码展示
```java
import java.util.*;
import java.nio.charset.IllegalCharsetNameException;
import java.io.*;

public class test3_2{
	
		public static void main(String [] args) throws Exception{
				Runnable r1 = () -> System.out.println("Hello World 1");
			
				Runnable r2 = new Runnable(){
						public void run(){
								System.out.println("Hello World 2");	
						}	
				};
				
				
				process(r1);
				process(r2);
				process(() -> System.out.println("Hello World 3"));
			
		}
		
		public static void process(Runnable r){///要在main函数之外定义函数否则报错
				r.run();
		}
		
}

一开始出现的错误：
test3_2.java:16: 错误: 非法的表达式开始
                                public static void process(Runnable r){
                                ^
test3_2.java:19: 错误: 方法声明无效; 需要返回类型
                                process(r1);
                                ^
test3_2.java:19: 错误: 需要<标识符>
                                process(r1);
                                          ^
test3_2.java:20: 错误: 方法声明无效; 需要返回类型
                                process(r2);
                                ^
test3_2.java:20: 错误: 需要<标识符>
                                process(r2);
                                          ^
test3_2.java:21: 错误: 方法声明无效; 需要返回类型
                                process(() -> System.out.println("Hello World 3"));
                                ^
test3_2.java:21: 错误: 非法的类型开始
                                process(() -> System.out.println("Hello World 3"));
                                        ^
test3_2.java:25: 错误: 需要class, interface或enum
}
^
8 个错误


Out:
Hello World 1
Hello World 2
Hello World 3


```

