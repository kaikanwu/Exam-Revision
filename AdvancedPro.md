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

组合模式（Composite Pattern），**又叫部分整体模式，是用于把一组相似的对象当作一个单一的对象**。组合模式依据树形结构来组合对象，用来表示部分以及整体层次。这种类型的设计模式属于结构型模式，它创建了对象组的树形结构。

这种模式创建了一个包含自己对象组的类。该类提供了修改相同对象组的方式。

In some application, we might need to **perform the same operation on objects or groups of objects.**
Example:

* **file system**: computing the size of files and folders of files
* items and groups of items in an **online shop**

##### Interfaces in the composite pattern

1. component:
2. leaf
3. composite

如何解决：树枝和叶子实现统一接口，树枝内部组合该接口。

关键代码：树枝内部组合该接口，并且含有内部属性 List，里面放 Component。

应用实例： 1、算术表达式包括操作数、操作符和另一个操作数，其中，另一个操作符也可以是操作树、操作符和另一个操作数。 2、在 JAVA AWT 和 SWING 中，对于 Button 和 Checkbox 是树叶，Container 是树枝。

优点： 1、高层模块调用简单。 2、节点自由增加。

缺点：在使用组合模式时，其叶子和树枝的声明都是实现类，而不是接口，违反了依赖倒置原则。

使用场景：部分、整体场景，如树形菜单，文件、文件夹的管理。

**何时采用组合模式**：

     1.需求重要体现部分与整体的层次结构时

     2.你希望用户忽略组合对象与单个对象的不同，用户将统一地使用组合结构中的所有对象。

#### Factory pattern 工厂模式

工厂模式属于创建型模式，提供了一种创建对象的最佳方式。
在Factory pattern中，**我们在创建对象时不会对客户端暴露创建逻辑，并且使通过使用一个共同的接口来指向新创建的对象。**

**意图**：定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行。

**主要解决**：主要解决接口选择的问题。

**何时使用**：我们明确地计划不同条件下创建不同实例时。

**如何解决**：让其子类实现工厂接口，返回的也是一个抽象的产品。

**使用场景**： 1、日志记录器：记录可能记录到本地硬盘、系统事件、远程服务器等，用户可以选择记录日志到什么地方。 2、数据库访问，当用户不知道最后系统采用哪一类数据库，以及数据库可能有变化时。 3、设计一个连接服务器的框架，需要三个协议，"POP3"、"IMAP"、"HTTP"，可以把这三个作为产品类，共同实现一个接口。

#### Visitor pattern 访问者模式

Definition:
封装某些作用于某种数据结构中各元素的操作，它可以在不改变数据结构的前提下定义作用于这些元素的新的操作。**(主要将数据结构与数据操作分离)**。

**使用场景**： 1、对象结构中对象对应的类很少改变，但经常需要在此对象结构上定义新的操作。 2、需要对一个对象结构中的对象进行很多不同的并且不相关的操作，而需要避免让这些操作"污染"这些对象的类，也不希望在增加新操作时修改这些类。

Some times is is useful to keep some methods away from our nice neat class hierarchies.

e.g.

* methods that are platform/device specific that would require multiple definitions in each class.

* Methods that span unrelated classes

* Perhaps we want to make new methods without modifying the classes themselves

#### Proxy pattern 代理模式

在代理模式（Proxy Pattern）中，一个类代表另一个类的功能。这种类型的设计模式属于结构型模式。

在代理模式中，我们创建具有现有对象的对象，以便向外界提供功能接口。

**意图**：为其他对象提供一种代理以控制对这个对象的访问。

**主要解决**：在直接访问对象时带来的问题，比如说：要访问的对象在远程的机器上。在面向对象系统中，有些对象由于某些原因（比如对象创建开销很大，或者某些操作需要安全控制，或者需要进程外的访问），直接访问会给使用者或者系统结构带来很多麻烦，我们可以在访问此对象时加上一个对此对象的访问层。

**何时使用**：想在访问一个类时做一些控制。

**如何解决**：增加中间层。

**关键代码**：实现与被代理类组合。

**应用实例**： 1、Windows 里面的快捷方式。 2、猪八戒去找高翠兰结果是孙悟空变的，可以这样理解：把高翠兰的外貌抽象出来，高翠兰本人和孙悟空都实现了这个接口，猪八戒访问高翠兰的时候看不出来这个是孙悟空，所以说孙悟空是高翠兰代理类。 3、买火车票不一定在火车站买，也可以去代售点。 4、一张支票或银行存单是账户中资金的代理。支票在市场交易中用来代替现金，并提供对签发人账号上资金的控制。 5、spring aop。

**优点**： 1、职责清晰。 2、高扩展性。 3、智能化。

**缺点**： 1、由于在客户端和真实主题之间增加了代理对象，因此有些类型的代理模式可能会造成请求的处理速度变慢。 2、实现代理模式需要额外的工作，有些代理模式的实现非常复杂。

**使用场景**：按职责来划分，通常有以下使用场景： 1、远程代理。 2、虚拟代理。 3、Copy-on-Write 代理。 4、保护（Protect or Access）代理。 5、Cache代理。 6、防火墙（Firewall）代理。 7、同步化（Synchronization）代理。 8、智能引用（Smart Reference）代理。

#### Decorator pattern 装饰器模式

装饰器模式（Decorator Pattern）**允许向一个现有的对象添加新的功能，同时又不改变其结构**。这种类型的设计模式属于结构型模式，它是作为现有的类的一个包装。
用来包装原有的类，并在保持类方法签名完整性的前提下，提供了额外的功能。


**意图**：动态地给一个对象添加一些额外的职责。就增加功能来说，装饰器模式相比生成子类更为灵活。

**主要解决**：一般的，我们为了扩展一个类经常使用继承方式实现，由于继承为类引入静态特征，并且随着扩展功能的增多，子类会很膨胀。

**何时使用**：在不想增加很多子类的情况下扩展类。

**如何解决**：将具体功能职责划分，同时继承装饰者模式。

**关键代码**： 1、Component 类充当抽象角色，不应该具体实现。 2、修饰类引用和继承 Component 类，具体扩展类重写父类方法。

**应用实例**： 1、孙悟空有 72 变，当他变成"庙宇"后，他的根本还是一只猴子，但是他又有了庙宇的功能。 2、不论一幅画有没有画框都可以挂在墙上，但是通常都是有画框的，并且实际上是画框被挂在墙上。在挂在墙上之前，画可以被蒙上玻璃，装到框子里；这时画、玻璃和画框形成了一个物体。

**优点**：装饰类和被装饰类可以独立发展，不会相互耦合，装饰模式是继承的一个替代模式，装饰模式可以动态扩展一个实现类的功能。

**缺点**：多层装饰比较复杂。

使用场景： 1、扩展一个类的功能。 2、动态增加功能，动态撤销。

#### Observer pattern 观察者模式

**当对象间存在一对多关系时，则使用观察者模式（Observer Pattern）**。比如，当一个对象被修改时，则会自动通知它的依赖对象。观察者模式属于行为型模式。

**意图**：定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。

**主要解决**：一个对象状态改变给其他对象通知的问题，而且要考虑到易用和低耦合，保证高度的协作。

**何时使用**：一个对象（目标对象）的状态发生改变，所有的依赖对象（观察者对象）都将得到通知，进行广播通知。

**如何解决**：使用面向对象技术，可以将这种依赖关系弱化。

**关键代码**：在抽象类里有一个 ArrayList 存放观察者们。

**应用实例**： 1、拍卖的时候，拍卖师观察最高标价，然后通知给其他竞价者竞价。

**优点**： 1、观察者和被观察者是抽象耦合的。 2、建立一套触发机制。

**缺点**： 1、如果一个被观察者对象有很多的直接和间接的观察者的话，将所有的观察者都通知到会花费很多时间。 2、如果在观察者和观察目标之间有循环依赖的话，观察目标会触发它们之间进行循环调用，可能导致系统崩溃。 3、观察者模式没有相应的机制让观察者知道所观察的目标对象是怎么发生变化的，而仅仅只是知道观察目标发生了变化。

**使用场景**：
一个抽象模型有两个方面，其中一个方面依赖于另一个方面。将这些方面封装在独立的对象中使它们可以各自独立地改变和复用。
一个对象的改变将导致其他一个或多个对象也发生改变，而不知道具体有多少对象将发生改变，可以降低对象之间的耦合度。
一个对象必须通知其他对象，而并不知道这些对象是谁。
需要在系统中创建一个触发链，A对象的行为将影响B对象，B对象的行为将影响C对象……，可以使用观察者模式创建一种链式触发机制。

**注意事项**： 1、JAVA 中已经有了对观察者模式的支持类。 2、避免循环引用。 3、如果顺序执行，某一观察者错误会导致系统卡壳，一般采用异步方式。