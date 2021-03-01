# Java_10_Multithreading(Concurrency)

## :muscle:Multithreading in Java(자바의 멀티 쓰레딩) / Concurrency(동시성)
자바는 Multithread language(멀티 쓰레딩 언어)이다. 멀티 쓰레딩이라, 그러면 싱글 쓰레딩 언어도 있을까? 싱글 쓰레딩 언어도 있는데, Python이나 JavaScript가 이에 속한다. 여기서는 자바의 멀티 쓰레딩이 무엇인지 살펴보자.

멀티 쓰레딩 언어를 효과적으로 활용하기 위해서, 우선 monitor와 lock에 대한 기본적인 사실들을 알고 있는 것이 좋다. 아래 리스트에서 이에 대해 나열해 본다.

* Synchronization(동기화)가 보호하는 대상은 코드 자체가 아니라 객체와 메모리이다.
* 동기화는 쓰레드 간의 협력 매커니즘이다. 하나의 버그가 협력 모델을 깰 수 있고 이는 보다 큰 문제를 불러올 수 있다.
* monitor를 acquiring(획득)하는 것은 다른 쓰레드가 해당 모니터를 획득하는 것을 방지할 뿐이다. 객체 자체를 보호하지는 못한다.
* Unsynchronized(비동기성) 메서드는 객체의 monitor가 잠겨있다고 하더라도 can see (and modify) inconsistent state. < inconsistent state란 무엇인가? 먼저 알아보고 돌아오자.
* Object[]를 잠그는 것은 각각의 객체를 잠그는 것은 아니다.
* 기본 자료형은 not mutable(불변)이다. 그러므로 잠글 수 없고 잠글 필요도 없다.
* 인터페이스에서는 메서드 선언부에 synchronized를 사용할 수 없다.
* Inner classes are just syntactic sugar, so locks on inner classes have no effect on
the enclosing class (and vice versa).
• Java’s locks are reentrant. This means that if a thread holding a monitor
encounters a synchronized block for the same monitor, it can enter the block.

### :star:Concurrency
동시성은 한번에 한가지 업무를 수행하는 대신 프로그램의 여러 업무를 동시에 수행하는 것이다. 이 동시성을 통해, 활용되지 않고 있는 운영체제와 하드웨어의 잠재력을 수면 위로 끌어올릴 수 있다. 예를들어 요즘 사용되는 CPU는 여러개의 코어를 담고 있다. 프로그램은 업무를 수행하며 여러개의 코어를 활용할 수 있는 경우가 있을것이고 그렇게 함으로 업무를 훨씬 빠르게 끝마칠 수 있을 것이다. 이 <b>동시성의 중심에는 쓰레드가 있다</b>.

### :star:lock
여기서 lock이란 무엇인가? 자바의 모든 객체는 고유한 lock을 지닌다. synchronized 키워드가 사용될 때 마다, lock은 중요한 존재가 된다. 쓰레드가 주어진 객체에 대해 synchronized 메서드를 실행하려 할 때. 쓰레드는 먼저, 해당 객체의 lock을 구해야 한다. 쓰레드는 lock을 구한 이후에 synchronized 메서드를 실행하도록 허용된다. 메서드의 실행이 끝나면 쓰레드는 자동적으로 lock을 버린다. 내부에서 lock을 구하고 버리는 과정은 JVM에 의해 이뤄지며 프로그래머에게는 이에 관여할 책임이 없다.

#### :mag:Object level lock vs Class level lock

1. Object level lock : 객체 lock을 사용한다는 것은 non-static 메서드 혹은 블락을 동기화 한다는 것이다. 이는 해당 "객체"의 메서드나 블럭이 한번에 하나의 쓰레드에 의해서만 접근할 수 있게 하는 것이다. non-static 데이터를 보호하기 위해서 사용된다. 객체 단위로 locking 할 수 있다.

2. Class level lock : 클래스 lock을 사용한다는 것은 static 메서드 혹은 블락을 동기화 한다는 것이다. 이는 해당 "클래스"의 메서드나 블럭이 한번에 하나의 쓰레드에 의해서만 접근할 수 있게 하는 것이다. static 데이터를 보호하기 위해서 사용된다. 클래스 단위로 locking 할 수 있다.

읽어 보아도, 예제를 보아도 이해를 못했는데, 두가지 방식을 바꿔가며 코드를 돌려보니 차이가 보였다!

```java
class Main implements Runnable {

    public void run() {
        Lock();
    }

    public void Lock() {
        System.out.println(Thread.currentThread().getName());
        synchronized(Main.class) {
//        synchronized(this) {
            System.out.println("in block "
                    + Thread.currentThread().getName() + " start");
            System.out.println("in block "
                    + Thread.currentThread().getName() + " end");
        }
    }

    public static void main(String[] args) {
        Main m1 = new Main();
        Thread t1 = new Thread(m1);
        Thread t2 = new Thread(m1);
        Main m2 = new Main();
        Thread t3 = new Thread(m2);
        t1.setName("t1");
        t2.setName("t2");
        t3.setName("t3");
        t1.start();
        t2.start();
        t3.start();
    }
} 
```

* synchronized(this)를 사용한 경우, object level lock이 쓰인다.
* synchronized(Main.class) 사용한 경우, class level lock이 쓰인다.
* 실행 결과는 다르다.

* 실행 결과

> object level lock : synchronized(this)  
>  
>t1  
>t3  
>t2  
>in block t3 start  
>in block t1 start  
>in block t1 end  
>in block t3 end  
>in block t2 start  
>in block t2 end  

쓰레드 1, 2, 3 실행의 순서는 그때 그때 바뀔 수 있고, 각각의 객체에 한번에 하나씩 쓰레드가 접근하므로 각각의 start와 end도 쓰레드마다 따로 이뤄진다.

> class level lock : synchronized(Main.class)  
>  
>t2  
>t1  
>t3  
>in block t2 start  
>in block t2 end  
>in block t3 start  
>in block t3 end  
>in block t1 start  
>in block t1 end  

쓰레드 1, 2, 3 실행의 순서는 그때 그때 바뀔 수 있으나, 해당 클래스에 한번에 하나의 쓰레드만 접근하므로 하나의 쓰레드의 start와 end가 끝나기 전까지 다음 쓰레드는 대기한다.

#### :mag:lock vs monitor
lock과 monitor의 차이점이 무엇일까? 이 질문에 정확하게 대답하기 있기 위해서는 아직 자바 멀티 쓰레딩이 어떻게 이뤄지는지 더 깊이 알아야 한다. 우선은 몇가지 먼저 짚고 넘어가보자.

### :star:자바의 쓰레딩 모델
자바의 멀티 쓰레딩은 다수의 쓰레드를 동시에 실행하는 과정이다. 

A thread is a lightweight sub-process, the smallest unit of processing. Multiprocessing and multithreading, both are used to achieve multitasking.

However, we use multithreading than multiprocessing because threads use a shared memory area. They don't allocate separate memory area so saves memory, and context-switching between the threads takes less time than process.

Java Multithreading is mostly used in games, animation, etc.

#### :mag:Advantages of Java Multithreading
Enhanced performance by decreased development time
Simplified and streamlined program coding
Improvised GUI responsiveness
Simultaneous and parallelized occurrence of tasks
Better use of cache storage by utilization of resources
Decreased cost of maintenance
Better use of CPU resource

#### :mag:Disadvantages of Java Multithreading
Complex debugging and testing processes
Overhead switching of context
Increased potential for deadlock occurrence
Increased difficulty level in writing a program
Unpredictable results

#### :mag:Java’s threading model is based on three fundamental concepts:

1. Shared, visible-by-default mutable state
This means that objects are easily shared between different threads in a process,
and that they can be changed (“mutated”) by any thread holding a reference to
them.

2. Preemptive thread scheduling
The OS thread scheduler can swap threads on and off cores at more or less any
time.

3. Object state can only be protected by locks
Locks can be hard to use correctly, and state is quite vulnerable—even in unex‐
pected places such as read operations.

Taken together, these three aspects of Java’s approach to concurrency explain why
multithreaded programming can cause so many headaches for developers.

### :star:Thread 클래스
자바 클래스에 동시성을 부여하기 위해서 가장 먼저 필요한 클래스는 ```java.lang.Thread``` 클래스이다. 이는 자바에서의 모든 동시성 개념의 기반이다.
https://www.javatpoint.com/creating-thread

#### :mag:Thread safety
https://howtodoinjava.com/java/multi-threading/what-is-thread-safety/

### :star:Runnable 인터페이스
자바의 동시성에서 Thread 클래스 다음으로 알아야 할 것은 ```java.lang.Runnable``` 인터페이스이다.
https://www.javatpoint.com/runnable-interface-in-java

#### :mag:Process vs Thread
https://www.geeksforgeeks.org/difference-between-process-and-thread/

### :star:쓰레드의 상태(쓰레드의 라이프 사이클)
https://www.javatpoint.com/life-cycle-of-a-thread
https://www.javatpoint.com/can-we-start-a-thread-twice
https://www.javatpoint.com/sleep()-method

### :star:쓰레드의 우선순위
https://www.javatpoint.com/thread-scheduler-in-java
https://www.javatpoint.com/priority-of-a-thread

### :star:Main 쓰레드
https://www.geeksforgeeks.org/main-thread-java/

#### :mag:Daemon 쓰레드

### :star:Synchronization
https://www.javatpoint.com/synchronization-in-java

#### :mag:Atomic

#### :mag:Compare-And-Swap

#### :mag:Volatile



### :star:데드락
https://www.javatpoint.com/deadlock-in-java

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/multithreading-in-java  
https://howtodoinjava.com/java-concurrency-tutorial/  
https://www.geeksforgeeks.org/object-level-class-level-lock-java/  
https://java2blog.com/object-level-locking-vs-class-level-locking-java/  
https://www.multisoftvirtualacademy.com/blog/common-advantages-and-disadvantages-of-multithreading-in-java/  