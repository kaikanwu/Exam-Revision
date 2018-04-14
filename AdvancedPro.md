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

```Java
PrintWriter writer = new PrintWriter(client.getOutputStream(), true);

```

* BufferedReader

```Java
BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
```

1. In the Server we create a PrintWriter





## 三、Design Patterns
