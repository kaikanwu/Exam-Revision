# Advanced Programming

* [一、Thread](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#一thread)
  * Concurrency
  * Thread
  * Blocking methods
  * race condition
  * dead lock
  * synchronized
* [二、Client-server system](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#二client-server-system)
  * protocal
* [三、Design Patterns](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#三designp-atterns)
  * Observer pattern
  * Decorator pattern
* [四、Other questions](https://github.com/kaikanwu/Exam-Revision/blob/master/AdvancedPro.md#四other-questions)

## 一、Thread

### Concurrency

> Multiple parts of program running simultanesouly

**why?**
Make use of multiple processors
Efficient integration with slow devices
Responsive OS

> **In Java, we can use threads to build concurrency programs**

### Thread

1.Two ways to create threads in Java

* **Extends the Thread class**

```Java
public class MainThread extends Thread{
    public void run(){
        try{
            Thread.sleeep(1000);
        }catch(InterruptedException e){
        }
        System.out.println("Thread finished")
    }

    public static void main(String[] args){
        for(int i = 0; i < 10; i++){
            new MainThread().start();
            System.out.println("The end");
        }
    }
}
```

* **Implements the Runnable interface**

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

> must use **.start()** to start the thread

Create many threads:

```java
public static void main(String[] args){
    int nThreads = 2;
    Thread[] threads = new Thread[nThreads];

    for(int i = 0; i < nThreads; i ++){
        Test t = new Test(3);
        threads[i] = new Thread(t);
        threads[i].start();
    }
}

```

> The program stops once all threads are complete.

### Blocking methods

Blocking methods are methods that rely on something else within the system for termination.

**Blocking methods are thoese methods which blocks the executing thread until their operation finished.**

Because these methods rely on something external, they might be waiting forever.

To ensure smooth running, they should be cancelable

1.**Thread.sleep(long time)**
    时间单位是毫秒

```Java
public void run(){
    try{
        Thread.sleep(1000)
    }catch(InterruptedException e){
        System.out.println("you wake me up")
    }

}
```

2.**someThread.Join()**
> In many applicaiton it will be useful to know if a  Therad has finished.

This method pause the current thread until someThread has finished.

```Java
MyThread[] m = new MyThread[5];
for(int i = 0; i < 5; i++){
    m[i] = new Thread();
    m[i].start;
}
for(int i = 0; i < 5; i++){
    m[i].join();

}

```

### The benefits of parallel processing

* Many machine have multiply cores(processors)

* Threads can be placed on different cores
    (JVM do this for us, we cannot control)

* Running things in parallel should give us speed improvements.

### Deadlocks

What is the deadlock?
> Two threads are both waiting for one another to release a lock. In this situation, the program will hang indefinitely.


## 二、Client-server system

## 三、Design Patterns
