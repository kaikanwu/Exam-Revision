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

### Race condition

**A race condition occurs when two or more threads can access shared data and they try to change it at the same time.** Because the thread scheduling algortithms can swap between threads at any time, you don't know the order in which the threads will attempt to access the shared data.

**To avoid Race condition:**
1.The easiest way is with synchonized blocks and methods.
> When any thread is volking a synchronized method, all other threads trying to are paused until it has finished.

```Java
public void run(){
    for(int i = 0; i< n; i ++){
        synchronized(count){
            count.increment();
        }
    }

}
```

> These code causes the thread to lock the **count** object
No other threads can modify **count** when the thread is in this block

2.Another approach involves creating Lock objects.

```Java
public static class MyCounter{
    private int count = 0;
    private ReentrantLock counterLock = new ReentrantLock();
    public void incream(){
        counterLock.lock();
        count ++;
        counterLock.unlock();
    }
}
```

> When counterLock is locked, no other thread can lock it unitl it has been unlocked.

**There is a problem: between lock() and unlock(), the code may throws an exception that make the unlock() never happens.**

So we need a better way use lock object.
The following code make sure the lock will release finally.

```Java
someLock.lock();
try{
// some code

}catch(){
}
finally{
    someLock.unlock();
}
```

### Deadlocks

What is the deadlock?

> Two or more threads are both waiting for each other to release a lock. In this situation, the program will hang indefinitely.(will block forever)

### Conditions

Definition: **Conditions allow threads to temporarily unlock locks whilst they await some condition to be fulfiled**

```Java
private ReentrantLock counterLock = new ReentrantLock();

private Condition bigEnough = counterLock.newCondition();
```

> Threads can await the condition through the Condition.await() method

```Java
public void decrement(int amount){
    counterLock.lock();
    try{
        while(count < amount){
        bigEnough.await();
        }
        count -= amount;
    }catch(InterruptedException e){
        //fall through
    }finally{
        counterLock.unlock();
    }
}
```

### Threads in Swing

SwingWorker

**Why Swing isn't Thread safe**
[http://www.asjava.com/swing/why-isn%E2%80%99t-the-swing-toolkit-multi-thread-safe/](http://www.asjava.com/swing/why-isn%E2%80%99t-the-swing-toolkit-multi-thread-safe/)

## 二、Client-server system

### Distributed Systems 分布式系统

**Threads**: Code run in multiple processes on one machine

**Distributed System**: Processes communicating across machines

### Servers and Clients

Java inbuilt objects:
**ServerSocket --> Server**
**Socket --> Client**

#### Building a server

```Java
import java.net.*;
import java.io.*;

public class SimpleServer{
    // The PORT here is an abstract thing, they are produced in software
    private static int PORT = 8765;
    public static void main(String[] args) throws IOException{
        //make a server object
        ServerSocket listener = new ServerSocket(PORT);
        // wait for a connection and create a client
        Socket client = listener.accept();
        // close the connection
        client.close();

    }
}
```

#### IP addresses and ports

IP: **Internet Protocal** is a set of rules used for connecting devices in a network

All devices on the network are assigned an IP address.

e.g. 192.167.1.122

* each portion goes form 0 - 255

* special address: 127.0.0.1 - localhost: use this address to access your own machine form your own machine

* find your IP address: **ifconfig**

#### PORT

```Java
private static int PORT = 8765;

```

> The PORT here must be unused.
Client need to know which port to access the server
Commonly used ports:
20,21: FTP
22: SSH
80: HTTP

#### Building a client

```Java
import java.net.*;
import java.io.*;

public class SimpleClient{
    private static int PORT = 8765;
    private static String server = "127.0.0.1";
    public static void main(String[] args) throws IOException{
        // make a socket and try and connect
        Socket socket = new Socket(server, PORT);
        // close the socket
        socket.close();
    }
}
```

#### Sending message form the Server to Client

Useing the following Stream classes:

* PrintWriter

In the Server we create a PrintWriter

```Java
PrintWriter writer = new PrintWriter(client.getOutputStream(), true);

```

* BufferedReader: in the client

```Java
BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
```

## 三、Design Patterns

### What are patterns

Sets of rules that, if followed, allow easy code understanding and re-use

Separation of tasks: iterators decouple algorithms from data objects

Can operate at many levels:
whole applications: (Model-View-Controller)
small parts of an application(Iterators)迭代器

### Some userful patterns

#### Iterators Pattern 迭代器模式

这种模式用于顺序访问集合对象的元素，不需要知道集合对象的底层表示。
（迭代器可能是Java 中使用最多的一种模式）

说明迭代器之前先得说说**集合collection**, 集合可以看成一个可以包容对象的容器，例如 List, Set, Map, 甚至数组都可以叫做集合，**迭代器的作用就是把容器中的对象一个一个遍历出来**

Iterable接口：Iteratoriterator();
Iterator接口：boolean hasNext(); E next(); void remove();

Many algorithms require the ability to move through a collection of objects.

* Finding
* Sorting, etc

#### Composite pattern 组合模式

In some application, we might need to **perform the same operation on objects or groups of objects.**
Example:

* **file system**: computing the size of files and folders of files
* items and groups of items in an **online shop**

##### Interfaces in the composite pattern

1. component:
2. leaf
3. composite

**何时采用组合模式**：

     1.需求重要体现部分与整体的层次结构时

     2.你希望用户忽略组合对象与单个对象的不同，用户将统一地使用组合结构中的所有对象。

#### Factory pattern 工厂模式

工厂模式属于创建型模式，提供了一种创建对象的最佳方式。
在Factory pattern中，**我们在创建爱你对象时不会对客户端暴露创建逻辑，并且使通过使用一个共同的接口来指向新创建的对象。**

**意图**：定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行。

**主要解决**：主要解决接口选择的问题。

**何时使用**：我们明确地计划不同条件下创建不同实例时。

**如何解决**：让其子类实现工厂接口，返回的也是一个抽象的产品。

#### Visitor pattern 访问者模式

#### Proxy pattern 代理模式

#### Decorator pattern 装饰器模式

#### Observer pattern 观察者模式

