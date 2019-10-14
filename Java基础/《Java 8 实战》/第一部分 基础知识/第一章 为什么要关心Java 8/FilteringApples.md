```
ort java.util.*;
import java.util.function.Predicate;

public class FilteringApples{

    public static void main(String ... args){

        List<Apple> inventory = Arrays.asList(new Apple(80,"green"),
                                              new Apple(155, "green"),
                                              new Apple(120, "red"));	

        // [Apple{color='green', weight=80}, Apple{color='green', weight=155}]
        List<Apple> greenApples = filterApples(inventory, FilteringApples::isGreenApple);
        //方法作为Predicate参数p传递进去
        //isGreenApple是方法，即函数
        
        System.out.println("方法1绿苹果："+greenApples);//打印绿苹果
        
        // [Apple{color='green', weight=155}]
        List<Apple> heavyApples = filterApples(inventory, FilteringApples::isHeavyApple);
        System.out.println("方法1重苹果："+heavyApples);//打印重苹果
        
        ///另一种方法
        
        // [Apple{color='green', weight=80}, Apple{color='green', weight=155}]
        List<Apple> greenApples2 = filterApples(inventory, (Apple a) -> "green".equals(a.getColor()));
        System.out.println("方法2绿苹果："+greenApples2);//打印
        
        // [Apple{color='green', weight=155}]
        List<Apple> heavyApples2 = filterApples(inventory, (Apple a) -> a.getWeight() > 150);
        System.out.println("方法2重苹果："+heavyApples2);
        
        // []
        List<Apple> weirdApples = filterApples(inventory, (Apple a) -> a.getWeight() < 80 || 
                                                                       "brown".equals(a.getColor()));
        System.out.println("方法2烂苹果："+weirdApples);
    }

    public static List<Apple> filterGreenApples(List<Apple> inventory){
        List<Apple> result = new ArrayList<>();
        for (Apple apple: inventory){
            if ("green".equals(apple.getColor())) {
                result.add(apple);
            }
        }
        return result;
    }

    public static List<Apple> filterHeavyApples(List<Apple> inventory){
        List<Apple> result = new ArrayList<>();
        for (Apple apple: inventory){
            if (apple.getWeight() > 150) {
                result.add(apple);
            }
        }
        return result;
    }

    //苹果是否是绿苹果
    public static boolean isGreenApple(Apple apple) {
        return "green".equals(apple.getColor()); 
    }
    
    //苹果重量是否大于150
    public static boolean isHeavyApple(Apple apple) {
        return apple.getWeight() > 150;
    }

    
    public static List<Apple> filterApples(List<Apple> inventory, Predicate<Apple> p){
        List<Apple> result = new ArrayList<>();
        for(Apple apple : inventory){
            if(p.test(apple)){
                result.add(apple);
            }
        }
        return result;
    }       

    ///初始化苹果
    public static class Apple {
        private int weight = 0;
        private String color = "";

        ///初始化苹果重量
        public Apple(int weight, String color){
            this.weight = weight;
            this.color = color;
        }
        
        ///返回苹果重量
        public Integer getWeight() {
            return weight;
        }
        
        ///设置苹果重量
        public void setWeight(Integer weight) {
            this.weight = weight;
        }

        //返回苹果颜色
        public String getColor() {
            return color;
        }
        
        ///设置苹果颜色
        public void setColor(String color) {
            this.color = color;
        }
        
        ///将苹果的颜色和重量设置成字符串返回
        public String toString() {
            return "Apple{" +
                   "color='" + color + '\'' +
                   ", weight=" + weight +
                   '}';
        }
    }
}
Out:
方法1绿苹果：[Apple{color='green', weight=80}, Apple{color='green', weight=155}]
方法1重苹果：[Apple{color='green', weight=155}]
方法2绿苹果：[Apple{color='green', weight=80}, Apple{color='green', weight=155}]
方法2重苹果：[Apple{color='green', weight=155}]
方法2烂苹果：[]


```
