# Advanced Programming

* [一、Thread](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#一thread)
  * Concurrency
  * race condition
  * dead lock
  * synchronized
* [二、Client-server system](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#二client-serversystem)
  * protocal
* [三、Design Patterns](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#三designpatterns)
  * Observer pattern
  * Decorator pattern
* [四、Other questions](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#四otherquestions)

## 一、Thread

1.Two ways to create threads in Java

* Extends the Thread class

* Implements the Runnable interface

> The Runnable interface

```java
public interface Runnable{
    public void run();
}

```

> implements a Runnable interface

```Java
public class Test implements Runnable{
    private int n;

    public Test(int n){
        this.n = n;

    }
    // must override the run method
    public void run(){
        for(int i = 0; i < 100; i++){
            System.out.println(n);
        }
    }
}
```

> To use the thread

```Java
public class RunnableTest{
    public static void main(String[] args){
        Test t = new Test(3);
        //we must create an instance and then place this instance within an instance of the Thread object
        Thread thread1 = new Thread(t);
        //thread1.start() will start the thread by invoking the run() method of Test
        thread1.start();
    }
}

```




## 二、Client-server system

## 三、Design Patterns

