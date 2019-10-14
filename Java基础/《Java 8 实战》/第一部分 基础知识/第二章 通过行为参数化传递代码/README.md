#### 2.1 应对不断变化的需求
* DRY（Don抰 Repeat Yourself，因为它打破了，不要重复自己）的软件工程原则
* 如果这位农民要求你对苹果的不同属性做筛选，比如大小、形状、产地等，又怎么办？而且，如果农民要求你组合属性，做更复杂的查询，比如绿色的重苹果，又该怎么办？

#### 2.2 行为参数化
* 第三次尝试不懂
* 现在你可以创建不同的```ApplePredicate```对象，并将它们传递给```filterApples```方法
* 测验2.1 编写灵活的```prettyPrintApple```方法（基本照着书写的，）
```test2_1.java
import java.util.*;
import java.nio.charset.IllegalCharsetNameException;

public class test2_1{
	
	
	public interface AppleFormatter{
		String accept(Apple a);	
	}
	
	public static class AppleFancyFormatter implements AppleFormatter{
		public String accept(Apple apple){
			String characteristic = apple.getWeight() > 150 ? "heavy" :
				"light";
			return "A " + characteristic +
				" " + apple.getColor() +" apple";
		}
	}
	
	public static class AppleSimpleFormatter implements AppleFormatter{
		public String accept(Apple apple){
			return "An apple of " + apple.getWeight() + "g";
		}
	}

	
	public static void prettyPrintApple(List<Apple> inventory, AppleFormatter formatter){
		for(Apple apple: inventory) {
			String output = formatter.accept(apple);
			System.out.println(output);
		}
	}

	public static void main(String [] args) throws Exception{

		List<Apple> inventory = Arrays.asList(new Apple(80,"green"), new Apple(155, "green"), new Apple(120, "red"));	

		prettyPrintApple(inventory,new AppleFancyFormatter());

		prettyPrintApple(inventory, new AppleSimpleFormatter());

	}

	
	public static class Apple {
		private int weight = 0;
		private String color = "";

		public Apple(int weight, String color){
			this.weight = weight;
			this.color = color;
		}

		public Integer getWeight() {
			return weight;
		}

		public void setWeight(Integer weight) {
			this.weight = weight;
		}

		public String getColor() {
			return color;
		}

		public void setColor(String color) {
			this.color = color;
		}

		public String toString() {
			return "Apple{" +
					"color='" + color + '\'' +
					", weight=" + weight +
					'}';
		}
	}

}

Out:
A light green apple
A heavy green apple
A light red apple
An apple of 80g
An apple of 155g
An apple of 120g

错误：
test2_1.java:43: 错误: 无法从静态上下文中引用非静态 变量 this
                prettyPrintApple(inventory,new AppleFancyFormatter());
                                           ^
test2_1.java:43: 错误: 无法从静态上下文中引用非静态 方法 prettyPrintApple(List<Apple>,AppleFormatter)
                prettyPrintApple(inventory,new AppleFancyFormatter());
                ^
2 个错误

需要把public static class AppleFancyFormatter implements AppleFormatter中的static加上才行
public static class AppleSimpleFormatter implements AppleFormatter{也是

```



#### 2.3 匿名类
* 测验2.2 匿名类谜题
```
public class MeaningOfThis
{
  public final int value = 4;
  public void doIt()
  {
    int value = 6;
    Runnable r = new Runnable(){
        public final int value = 5;
        public void run(){
          int value = 10;
          System.out.println(this.value);
        }
      };
      r.run();
    }
    public static void main(String...args)
    {
      MeaningOfThis m = new MeaningOfThis();
      m.doIt();
    }
}

```

#### 2.4 真实的例子

##### 2.4.1 用Comparator 来排序

##### 2.4.2 用Runnable 执行代码块

##### 2.4.3 GUI 事件处理

