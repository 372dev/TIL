# Java_10_Multithreading(Concurrency)

## :muscle:Multithreading in Java(자바의 멀티 쓰레딩) / Concurrency(동시성)

### :star:Runnable 인터페이스
자바의 동시성에서 Thread 클래스 다음으로 알아야 할 것은 ```java.lang.Runnable``` 인터페이스이다.

Runnable은 멀티 쓰레딩 프로그래밍을 위해 사용되는 인터페이스이다. 객체가 쓰레드를 통해 실행되기 원할 때, Runnable 인터페이스를 구현하여 클래스를 작성할 수 있다.

이 인터페이스는 리턴타입이 void고 내용이 비어있고 argument(전달 인자)도 없는 run() 메서드를 갖고 있다.

* public void run() : 전달 인자를 받지 않는다. Runnable을 구현하는 클래스가 쓰레드를 만들 때, run 메서드가 쓰레드에서 호출되며 이는 따로 실행된다.

Runnable 인터페이스는 해당 클래스의 인스턴스들에게 실행될 때 따를 규칙을 제공한다. 가장 흔한 사용 방식을 예로 들자면, run 메서드만 오버라이드 하도록 하는 것이다. Runnable을 구현하는 객체가 하나의 쓰레드를 시작할 때 마다 매번 run 메서드가 실행된다.

Runnable을 구현하는 클래스는 개별의 쓰레드에서 실행 된다. 쓰레드를 인스턴스화 하기 때문에 따로 상속된 쓰레드를 이용할 필요가 없다. 쓰레드를 상속하지 않는 것이 중요한 이유는, 클래스의 내용의 변경을 의도하는게 아니라면 상속을 사용할 이유가 없기 때문이다.

Runnable 클래스는 network programming에서 광범위하게 사용된다. 각각의 쓰레드가 서로 다른 flow of control을 담담하기 때문이다. Runnable 클래스는 또한 멀티 쓰레딩 프로그래밍에서 사용된다.

#### :mag:Runnable의 구현
Runnable을 구현하는 것은 쓰레드를 생성하는 가장 쉬운 방법이다. 어떤 객체에서든 Runnable을 구현하면 쓰레드를 생성할 수 있다. 해야할 것은 한가지, run() 메서드를 구현하는 것이다.

>public void run()

이 메서드의 내용에는 동시성을 갖는 쓰레드에서 실행하게 하고 싶은 코드를 입력한다. 메서드 안에서 변수를 사용할 수도, 클래스를 인스턴스화 할 수도, 그리고 메인 쓰레드와 마찬가지로 업무를 수행하게 할 수도 있다. run()메서드가 쓰레드의 시작점을 찍어주며 이 메서드가 작동하는 동안 쓰레드는 유지된다.

##### Runnable 인터페이스를 이용한 쓰레드 생성
Runnable을 이용해서 쓰레드를 생성할 때, 다음과 같은 구문이 사용된다.

>Runnable runnable = new MyRunnable();  
>Thread thread = new Thread(runnable);  
>thread.start();  

쓰레드는 참조 변수로 전달된 Runnable 객체가 갖고있는 run() 메서드 안에 작성된 코드를 실행한다.

* Runnable을 이용한 간단한 쓰레드 예제

```java
public class ExampleClass implements Runnable {  
  
    @Override  
    public void run() {  
        System.out.println("쓰레드 종료.");  
    }  
   
    public static void main(String[] args) {  
        ExampleClass ex = new ExampleClass();  
        Thread t1= new Thread(ex);  
        t1.start();  
        System.out.println("안녕?");  
    }  
}  
```

* 실행 결과

>안녕?  
>쓰레드 종료  

##### 람다식을 이용한 쓰레드 생성

```java
public class LambdaExampleClass {  
    
    public void method() {
      Thread thread;
      thread = new Thread(() -> {
        System.out.println("람다식을 사용한 Thread 생성 예제");
      });

      thread.start();
    }
     
    public static void main(String[] args) {  
      new LambdaExampleClass().method();
    }  
  }  
```

##### Thread vs Runnable
역할 수행, 메모리 사용, 구조 등에 있어서 Thread 클래스와 Runnable 인터페이스 사이에 몇가지 차이점이 있다.

쓰레드를 상속하면, 추가적인 메서드들이 요구된다. 예를 들어, 과도하거나 비효율적인 메모리를 사용하거나, 시간적으로 비효율적이거나, 다른 리소스를 잡아먹는다.
자바에서는 하나의 클래스만 상속이 가능하므로 Thread 클래스를 상속한 경우 다른 어떤 클래스도 상속할 수 없다. 이는 Runnable 인터페이스를 구현해서 쓰레드를 생성하는 이유가 된다.
Runnable은 코드를 더욱 유연하게 만든다. Thread 클래스를 상속하면 코드는 쓰레드 안에서만 존재하겠지만 Runnable의 경우 다양한 서비스를 활용하거나, 싱글-쓰레드 환경에서의 사용도 가능하다. 유지보수도 비교적 수월하다.

### :star:쓰레드의 상태 (라이프 사이클)
A thread can be in one of the five states. According to sun, there is only 4 states in thread life cycle in java new, runnable, non-runnable and terminated. There is no running state.

But for better understanding the threads, we are explaining it in the 5 states.

The life cycle of the thread in java is controlled by JVM. The java thread states are as follows:

1. New
The thread is in new state if you create an instance of Thread class but before the invocation of start() method.

2. Runnable
The thread is in runnable state after invocation of start() method, but the thread scheduler has not selected it to be the running thread.

3. Running
The thread is in running state if the thread scheduler has selected it.

4. Non-Runnable (Blocked)
This is the state when the thread is still alive, but is currently not eligible to run.

5. Terminated
A thread is in terminated or dead state when its run() method exits.

* Can we start a thread twice?
No. After starting a thread, it can never be started again. If you does so, an IllegalThreadStateException is thrown. In such case, thread will run once but for second time, it will throw exception.

### :star:쓰레드의 우선순위
Each thread have a priority. Priorities are represented by a number between 1 and 10. In most cases, thread schedular schedules the threads according to their priority (known as preemptive scheduling). But it is not guaranteed because it depends on JVM specification that which scheduling it chooses.
3 constants defined in Thread class:
public static int MIN_PRIORITY
public static int NORM_PRIORITY
public static int MAX_PRIORITY
Default priority of a thread is 5 (NORM_PRIORITY). The value of MIN_PRIORITY is 1 and the value of MAX_PRIORITY is 10.

Example of priority of a Thread:
class TestMultiPriority1 extends Thread{  
 public void run(){  
   System.out.println("running thread name is:"+Thread.currentThread().getName());  
   System.out.println("running thread priority is:"+Thread.currentThread().getPriority());  
  
  }  
 public static void main(String args[]){  
  TestMultiPriority1 m1=new TestMultiPriority1();  
  TestMultiPriority1 m2=new TestMultiPriority1();  
  m1.setPriority(Thread.MIN_PRIORITY);  
  m2.setPriority(Thread.MAX_PRIORITY);  
  m1.start();  
  m2.start();  
   
 }  
}     


Output:running thread name is:Thread-0
       running thread priority is:10
       running thread name is:Thread-1
       running thread priority is:1

* User define Priority Thread

  t1.setPriority(4);
  t2.setPriority(7);

#### :mag:thread scheduler
https://www.javatpoint.com/thread-scheduler-in-java

### :star:Main 쓰레드
https://www.geeksforgeeks.org/main-thread-java/

#### :mag:sleep 메서드
https://www.javatpoint.com/sleep()-method

#### :mag:Daemon 쓰레드

### :star:Synchronization
https://www.javatpoint.com/synchronization-in-java

#### :mag:Atomic

#### :mag:Compare-And-Swap

#### :mag:Volatile



### :star:Deadlock(교착상태)
https://www.javatpoint.com/deadlock-in-java
https://rightnowdo.tistory.com/entry/JAVA-concurrent-programming-교착상태Dead-Lock

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/runnable-interface-in-java  
https://www.javatpoint.com/life-cycle-of-a-thread  
https://www.javatpoint.com/can-we-start-a-thread-twice  
https://www.javatpoint.com/priority-of-a-thread  
https://www.javatpoint.com/java-thread-setpriority-method  
