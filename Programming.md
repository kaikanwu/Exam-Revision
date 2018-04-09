* [一、Object Oriented Programming](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#一oop)

* [二、Keywords](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#二keywords)
    - private
    - static
    - protected
    - final

* [三、statement](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#三statement)
    - if
    - while 
    - [for](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#for-语句)
    - [switch](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#switch-语句)

* [四、Interface](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#四interfaces)

* [五、Inheritance](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#五inheritance)

* [六、Recursive](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#六recursive)
* [七、GUI](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#七gui)
    - JComponents
    - diagrams
* [八、MVC](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#八mvc)
    - Model, View, Controller
    - Roles



# 一、OOP
> Object Oriented Programming

# 二、Keywords
> (qualifier) 关键词，限定词
## private

> The qualifier “private” means that the method can be used only in the class in which it is declared. 

## static

>  The qualifier “static” means that the method is a member of the class in which it is defined, and not of any object of that class. (In particular it is not necessary to create an object of the class in order to use the method.) 

## final
* final method
* final variables





# 三、statement

## for 语句 
```
for(initializaiton;termination; increment){
    statement(s)
}
```
* examples:
1. 基础
```java
for(int i = 0; i < 100; i++){
    ...
    System.out.println("Count is: " + i );
}
```
2. infinate loop 无限循环
```java
for(;;){
    //code
}
```
3. 遍历数组
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

## switch 语句

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

# 四、Interfaces
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
2. Implements an interface (实现一个接口）
> keyworkds: **implements**

> 

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
3. Interface vs. classes
    * All methods in an interface type are **abstract**; they don’t have an implementation 
    * All methods in an interface type are automatically public
    * An interface type does not have instance fields (though it can have constants)
4. Other 
    > A class can implement more than one interface


# 五、Inheritance
> 1. Reuse and extend your code 
> 2. Inheritance hierarchies



# 六、Recursive

# 七、GUI

# 八、MVC
1. Model, View, Controller
> Models: The model maintains the application logic -the key data structure for the program.

> View: The View is responsible for the laying out the components and displaying information for the user.

>Controller: The Controller is responsible for the listening to user input and take appropriate actions.