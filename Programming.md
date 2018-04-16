#

* [一、Object Oriented Programming](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#一oop)
  * Constructor
  * Polymorphism
  * Collection

* [二、Keywords](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#二keywords)
  * private
  * static
  * protected
  * final

* [三、statement](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#三statement)
  * if
  * while
  * [for](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#for-语句)
  * [switch](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#switch-语句)

* [四、Interface](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#四interfaces)

* [五、Inheritance](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#五inheritance)

* [六、Recursive](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#六recursive)
* [七、GUI](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#七gui)
  * JComponents
  * diagrams
* [八、MVC](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#八mvc)
  * Model, View, Controller
  * Roles

## 一、OOP ##

> Object Oriented Programming

### Constructor ###

构造器可以有任何访问的修饰符，public, private, protected 或者没有。 不同于实例方法，constructor不能有任何非访问性质的修饰符： static, final, synchronized, abstract.

>解释：构造方法用于初始化一个实例对象，所以static修饰是没有任何意义的;多个线程不会同时创建内存地址相同的同一个对象，所以synchronized修饰没有意义;
构造方法不能被子类继承，所以final和abstract修饰没有意义。

**Constructor是没有返回类型的（String, int...)，void 也不行。** 相比较实例方法可以返回任何类型的值或者无返回值void.

**Constructor的命名需要和类名相同，所以构造器方法的第一个字母应该是大写。**（相对的，实例方法的方法名一般都是小写字母）

当我们没有明确写出构造方法的时候，Java类会有一个public修饰的默认构造方法（不显示，没有参数，方法体为空）。 如果我们有重写构造方法，默认构造方法就不会存在

```Java
public class Test{
    // constructor
    public Test(String s){
    }

    public static void main(String[] args){
    //
    }


}
```

### Polymorphism ###

### Collection ###

Definition:
Collection是存储对象的容器，OOP语言对事物的体现都是以对象的方式，所以为了方便对多个对象的操作，存储对象，集合是存储对象的最常用的一种方式。

> **集合可以存储任意类型的对象，而且长度是可变的**。如果在写程序时，无法预知需要多少个对象，那个这时候使用数组就不太方便**（数组在声明是就规定好了长度和数据类型）**，集合在这个时候就可以解决问题。

集合可以做什么：

1. 将对象**添加**到集合 add
1. 从集合中**删除**对象 remove
1. 从集合中**查找**对象
1. 从集合中修改一个对象（其实就是查找删除添加？）

> **集合和数组中存放的都是对象的引用(reference)，而不是对象本身。**

```Java
---|Collection: 单列集合
            ---|List: 有存储顺序, 可重复
                ---|ArrayList:  数组实现, 查找快, 增删慢
                            由于是数组实现, 在增和删的时候会牵扯到数组增容, 以及拷贝元素. 所以慢。数组是可以直接 按索引查找, 所以查找时较快.

                ---|LinkedList: 链表实现, 增删快, 查找慢
                            由于链表实现, 增加时只要让前一个元素记住自己就可以, 删除时让前一个元素记住后一个元素, 后一个元素记住前一个元素. 这样的增删效率较高但查询时需要一个一个的遍历, 所以效率较低
 
                ---|Vector: 和ArrayList原理相同, 但线程安全,效率略低
                             和ArrayList实现方式相同, 但考虑了线程安全问题, 所以效率略低

            ---|Set: 无存储顺序, 不可重复
                ---|HashSet
                ---|TreeSet
                ---|LinkedHashSet
---| Map: 键值对
        ---|HashMap
        ---|TreeMap
        ---|HashTable
        ---|LinkedHashMap
```

为什么出现这么多集合容器，因为每一个容器对数据的存储方式不同，这种存储方式称之为数据结构（data structure）。

什么时候使用什么样的集合：

|Collection |我们需要保存若干个对象的时候使用集合  |
|---------|---------|
|List     |  如果我们需要保留存储顺序，并且保留重复元素，使用List.  1.其中如果查询较多，使用ArrayList。 2.如果存储较多，使用LinkedList。 3.如果需要线程安全，那么使用Vector。       |
|Set     |   如果我们不需要保留存储顺序，并且需要去掉重复元素，那么使用Set。 1.如果我们需要将元素排序，那么使用TreeSet。2.如果我们不需要排序，使用HashSet,HashSet比TreeSet效率更高。 3.s如果我们需要保留存储顺序，又要过滤重复元素，那么使用LinkedHashSet      |




#### 




## 二、Keywords ##

> 1. 访问控制修饰符: private, public, protected, default
> 2. 非访问修饰符: static, final, abstract, synchronized, volatile
> 3. (qualifier) 关键词，限定词

```form
            | Class | Package | Subclass | Subclass | World
            |       |         |(same pkg)|(diff pkg)|
————————————+———————+—————————+——————————+——————————+————————
public      |   +   |    +    |    +     |     +    |   +
————————————+———————+—————————+——————————+——————————+————————
protected   |   +   |    +    |    +     |     +    |
————————————+———————+—————————+——————————+——————————+————————
no modifier |   +   |    +    |    +     |          |
————————————+———————+—————————+——————————+——————————+————————
private     |   +   |         |          |          |

+ : accessible
blank : not accessible
no modifier = default (没有修饰符)
```

### default(没有修饰符) ###

使用默认访问修饰符声明的变量和方法，对同一个包内的类是可见的。**接口里的变量都隐式声明为 public static final**,而接口里的方法默认情况下访问权限为 public。

```java
String s = "123";
boolean process(){
    return true;
}
```

### private ###

> *can be used*: **method, variable**

The qualifier “private” means that the method(variable) can be used only in the class in which it is declared.

Private variable can be get/set by get/set method

```java
public class Logger{
    private String format;
    //get
    public String getFormat(){
        return this.format;
    }
    //set
    public void setFromat(String format){
        this.format = format;

    }
}
```

### public ###

> can be used: **class, interface, method, variable**

```java
public static void main(String[] args){
    //
}
```

### protected ###

> 1. can be used: **method, variable**
> 2. can be see in subclass and same package(被protected修饰的成员对于本包和其子类可见)

### static ###

> can be used: **variable, method**

1. The qualifier “static” means that the method is a member of the class in which it is defined, and not of any object of that class. (In particular it is not necessary to create an object of the class in order to use the method.)

2. static variable： static声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。

3. static method： static 声明独立于对象的静态方法。静态方法不能使用类的非静态变量(因为静态变量在类加载时就已经生成,而非静态变量在创建实例对象时才生成)。静态方法从参数列表得到数据，然后计算这些数据。

4. 访问静态变量和静态方法：classname.staticmethodname, classname.staticvariablename

```java
public class InstanceCounter{
    private static int numInstances = 0;

    protected static int getCount(){
        return numInstances;
    }
}

```

### final ###

* final method

>类中的 final 方法可以被子类继承，但是不能被子类修改。声明 final 方法的主要目的是防止该方法的内容被修改。

```java
public class Test{
    public final void testmethod(){
    //内容可以使用，但是不能修改
    }
}
```

* final variables

> final 变量能被显式地初始化并且只能初始化一次。**被声明为 final 的对象的引用不能指向不同的对象。但是 final 对象里的数据可以被改变。也就是说 final 对象的引用不能改变，但是里面的值可以改变**。
final 修饰符通常和 static 修饰符一起使用来创建类常量。

```java
public class Test{
    final int i = 6;
    // 和 static一起声明-->常量
    public static final int n = 99;
    static fianl String s = "hello";

}
```

* final class

>final 类不能被继承，没有类能够继承 final 类的任何特性。
> cannot be extend

```java
//final class
public final class Test{
    //
}
```

### abstract ###

> can be used: **class, method**
* abstract class
> 抽象类**不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充**。
一个类不能同时被 abstract 和 final 修饰。**如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误**。
抽象类可以包含抽象方法和非抽象方法。

```java
// abstract class
abstract class Test{
    private String name;
    public int number;
    public void eat();
    //abstract method
    public abstract void go();
}
```

* abstract method

抽象方法是一种没有任何实现的方法，该方法的的具体实现由子类提供。
抽象方法不能被声明成 final 和 static。
任何继承抽象类的子类必须实现父类的所有抽象方法，**除非该子类也是抽象类。**
如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法。
抽象方法的声明以分号结尾，例如：public abstract sample(); 。

```java
public abstract class SuperTest{
    //抽象方法没有具体实现
    abstract void m ();

}


public class Test extends SuperTest{
    void m(){
        //在子类中具体实现 父类中的抽象方法
    }
}

```

* synchronized

> can be used: **method**
synchronized 关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。

```java
public synchronized void test(){
    //
}
```

## 三、statement ##

### for 语句 ###

```java
for(initializaiton;termination; increment){
    statement(s)
}
```

* examples:

1.基础

```java
for(int i = 0; i < 100; i++){
    ...
    System.out.println("Count is: " + i );
}
```

2.infinate loop 无限循环

```java
for(;;){
    //code
}
```

3.遍历数组

```java
// used for array

int[] numbers = {1,2,3,4,5,6,7,8,9};

for(int x : numbers){
    System.out.println(x);
}
//output of this program:
// 1
// 2
// 3
// ...
```

#### switch 语句 ###

```java


public class SwitchDemo {
    public static void main(String[] args) {

        int month = 8;
        String monthString;
        switch (month) {
            case 1:  monthString = "January";
                     break;
            case 2:  monthString = "February";
                     break;
            case 3:  monthString = "March";
                     break;
            ...

            case 8:  monthString = "August";
                     break;
            ...
            default: monthString = "Invalid month";
                     break;
        }
        System.out.println(monthString);
    }
}
```

## 四、Interfaces ##

> Using interfaces to make your code re-useable
1. Interface declaration （接口声明）

```java
//example 1
public interface Measurable{
    int getMeasure();
}
```

```java
// example 2 with parameters
public interface OperateCar {
   // An enum with values RIGHT, LEFT
   int turn(Direction direction,
            double radius,
            double startSpeed,
            double endSpeed);
   int changeLanes(Direction direction,
                   double startSpeed,
                   double endSpeed);
   int signalTurn(Direction direction,
                  boolean signalOn);
   int getRadarFront(double distanceToCar,
                     double speedOfCar);
   int getRadarRear(double distanceToCar,
                    double speedOfCar);
         ......
   // more method signatures
}
```

2.Implements an interface (实现一个接口）
> keyworkds: **implements**
> class **must** define all the methods 必须重写接口中的所有方法

```java
public class BankAccount implements Measurable{
    //
    public int getMeasure(){
        return balance;
    }
    // could add additional methods
}
```

3.Interface vs. classes

    * All methods in an interface type are **abstract**; they don’t have an implementation

    * All methods in an interface type are automatically public

    * An interface type does not have instance fields (though it can have constants)

4.Other
    > A class can implement more than one interface

## 五、Inheritance ##

> 1. Reuse and extend your code
> 2. Inheritance hierarchies

## 六、Recursive ##

Recursive(递归)
a example of factorial funciton (阶乘函数):

```java
public static long factorial(int n){
    if(n==1) return 1;
    return n*factorial(n-1);
}
```

>output

```java
factorial(5)
    factorial(4)
        factorial(3)
            factorial(2)
                factorial(1)
                return 1
            return 2*1 =2
        return 3*2 =6
    return 4*6 =24
return 5*24 = 120

```

## 七、GUI ##

## 八、MVC ##

1. Model, View, Controller

* Models: The model maintains the application logic -the key data structure for the program.

* View: The View is responsible for the laying out the components and displaying information for the user.

* Controller: The Controller is responsible for the listening to user input and take appropriate actions.