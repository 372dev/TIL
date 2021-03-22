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
쓰레드의 상태는 다섯가지로 나뉜다. 다만 sun에 의하면, 자바 쓰레드의 life cycle에는 네가지 상태만 존재하며 이는 new, runnable, non-runnable, terminated 이다. running은 인정되지 않는다.

그러나 쓰레드에 대한 이해도를 높이기 위해서 여기서는 다섯가지 상태로 나누어 학습해보자. 쓰레드의 상태는 JVM에 의해서 통제 된다. 다섯가지 상태는 아래와 같다.

1. New
start() 메서드가 실행되기 전에 쓰레드 클래스의 인스턴스만 생성된 상태이면 쓰레드가 new 상태에 있다고 할 수 있다.

2. Runnable
start() 메서드의 실행 이후에 쓰레드는 runnable 상태가 된다. 그러나 쓰레드 스케쥴러는 아직 해당 쓰레드를 running 쓰레드가 되도록 선택하지 않은 상태이다.

3. Running
쓰레드 스케쥴러가 해당 쓰레드를 선택하면 running 상태가 된다.

4. Non-Runnable (Blocked)
쓰레드가 아직 살아있지만 작동하지 못하는 상태를 non-runnable이라고 한다.

5. Terminated
run() 메서드가 종료되면 해당 쓰레드는 terminated 혹은 dead 상태가 된다. 

* 쓰레드를 두번 실행할 수 있을까?
불가능하다. 한번 실행된 쓰레드는 다시 실행될 수 없다. 이미 실행된 쓰레드를 다시 실행하려 시도할 경우, IllegalThreadStateException이 발생한다. 그런 경우, 쓰레드는 처음 실행에서 정상적으로 작동하지만 두번째 실행 시도에서 예외를 던진다.

### :star:쓰레드의 우선 순위
각가의 쓰레드는 우선 순위를 갖는다. 그 우선 순위는 1에서 10까지의 숫자중 하나로 부여 받는데, 대부분의 경우에 쓰레드 스케쥴러가 정한다 (이를 preemptive scheduling 선점적 스케쥴링 이라 한다). 그러나 이 방식의 스케쥴링이 항상 보장되는 것은 아닌데 이는 선점적 스케쥴링이 JVM 설정에 의존적이기 때문이다.

* Thread class에 정의된 3 가지 상수

```java
public static int MIN_PRIORITY
public static int NORM_PRIORITY
public static int MAX_PRIORITY
```

쓰레드의 우선 순위 기본값은 5이다 (NORM_PRIORITY). MIN_PRIORITY 의 값은 1 이고 MAX_PRIORITY 의 값은 10이다.

* 예제

```java
class TestThreadPriority extends Thread {  
  public void run() {
    System.out.println("실행중인 쓰레드의 이름 : " + Thread.currentThread().getName());
    System.out.println("실행중인 쓰레드의 우선 순위 : " + Thread.currentThread().getPriority());  
  }

  public static void main(String args[]) {
    TestThreadPriority t1 = new TestThreadPriority();  
    TestThreadPriority t2 = new TestThreadPriority();  
    t1.setPriority(Thread.MIN_PRIORITY);  
    t2.setPriority(Thread.MAX_PRIORITY);  
    t1.start();
    t2.start();
  }  
}     
```

* 실행 결과

>실행중인 쓰레드의 이름 : Thread-0  
>실행중인 쓰레드의 우선 순위 : 10  
>실행중인 쓰레드의 이름 : Thread-1  
>실행중인 쓰레드의 우선 순위 : 1  

* 사용자 정의 쓰레드 우선 순위

>t1.setPriority(4);  
>t2.setPriority(7);  

#### :mag:thread scheduler
자바의 쓰레드 스케쥴러는 어떤 쓰레드가 먼저 작동해야 하는지 결정하는 기능을 하며 JVM의 일부분이다. 쓰레드 스케쥴러에 의해 어떤 러너블 쓰레드가 선택되고 먼저 실행될 지 알 수 없다. 다만 하나의 프로세스에서 한개의 쓰레드만 작동이 가능하다. 쓰레드 스케쥴러는 쓰레드의 순서를 정하기 위해 preemptive scheduling(선점적 스케쥴링) 혹은 time slicing(우선완료순 스케쥴링)을 이용한다.

* 선점적 스케쥴링과 우선완료순 스케쥴링의 차이가 무엇인지 가볍게 알아보자
  * 선점적 스케쥴링 - 가장 높은 우선순위의 업무가 먼저 처리되며 해당 업무가 대기 상태에 들어가거나 완료가 되어야만 다음 우선순위의 업무가 처리된다. 다만 업무 처리 중에 더 높은 우선순위의 업무가 나타나면 더 높은 우선순위의 업무를 먼저 수행한다.
  * 타임 슬라이싱 - 우선순위의 업무가 정해진 짧은 시간동안 처리되다가 다시 업무 풀로 돌아간다. 다음 처리할 업무를 결정해야 하는데, 무조건 우선순위의 업무만 처리하는 것이 아니라 처리 시간이 짧은 다른 업무도 돌아가면서 처리한다. 우선순위의 업무가 우선적으로 처리되지만 금방 처리를 완료할 수 있는 다른 업무에게도 기회가 돌아가게 된다.

### :star:Main 쓰레드
자바 프로그램이 실행될 때, 쓰레드 하나가 곧바로 실행된다. 이 쓰레드는 보통 프로그램의 메인 쓰레드라고 불려진다.

* 특성
  * 다른 "자식" 쓰레드들이 갈라져 나오는 "부모" 쓰레드이다.
  * 다양한 shutdown actions(종료 작업)을 수행하기 떄문에 종종 가장 마지막에 실행을 마치게 된다.

* 다이어그램
![Thread_Diagram](https://raw.githubusercontent.com/372dev/TIL/main/JAVA/img/10_Multithreading_Thread_Diagram.jpg)

프로그램이 실행됨과 동시에 자바 메인 쓰레드가 시작된다. 메인 쓰레드를 사용하기 위해서는 reference가 필요하다. 레퍼런스를 얻기 위해 Thread 클래스에 있는 currentThread() 메서드를 사용할 수 있다. 이 메서드는 자기가 호출된 쓰레드에 대한 reference를 리턴한다. 메인 쓰레드의 우선순위 기본값은 5 이다. 우선순위 값은 자녀 쓰레드로 상속되기 때문에 유저가 생성한 쓰레드들도 이 기본값을 갖게 된다.

* main() 메서드와 메인 쓰레드와의 관계
각각의 프로그램에서 JVM은 메인 쓰레드를 생성한다. 메인 쓰레드가 가장 먼저 하는 것은 main() 메서드를 찾는 것이다. 그 이후에 쓰레드는 클래스를 초기화한다. 참고로 JDK 6 부터 독립 어플리케이션에 main() 메서드는 필수이다.

#### :mag:Daemon 쓰레드
옥스포드 사전에서 Daemon을 찾아보면, 악마라는 첫번째 사전적 의미 말고 두번째 사전적 의미(컴퓨팅에서의 의미)가 있고 이는 "a background process that handles requests for services such as print spooling and file transfers, and is dormant when not required." 이라고 설명되어 있다. 우리가 흔히 데몬툴이라고 하며 많이 사용하는 유틸리티 들에서 사용하는 개념은 "파일의 전송이나 프린트 스풀링(*프린트 속도와 컴퓨터 속도의 차이를 중재하기 위해 프린트할 자료를 기기로 전송받아 두고 작업하는 것*) 등의 요청을 처리하며 요구되지 않을 시 수면상태가 되는 백그라운드 프로세스" 라고 할 수 있겠다. 디먼 쓰레드도 이와 같은 역할을 할까?

자바 디먼 쓰레드가 무엇인가 하는 질문에 대하여 전능하신 스택 오버플로우의 b_erb님이 답변해주시고 Gray님이 수정해주신 내용을 간추리면 다음과 같다.

>디먼 쓰레드는 프로그램이 종료되더라도 계속 필요한 업무를 수행하는 쓰레드이다. 프로그램이 명시적으로 JVM을 종료시키지 않는 이상, JVM은 프로그램 종료 후 디먼 쓰레드가 작업을 마치길 기다렸다가 종료된다. 디먼 쓰레드의 예를 들자면 가비지 컬렉터가 있다. 특정 쓰레드 실행 이전에 setDaemon(boolean) 메서드를 이용하면 해당 쓰레드를 디먼 쓰레드로 설정할 수 있다.  
출처 : https://stackoverflow.com/questions/2213340/what-is-a-daemon-thread-in-java

자바의 디먼 쓰레드는 유저 쓰레드에게 서비스를 제공하는 쓰레드이다. 이에 따라 디먼 쓰레드의 라이프 사이클은 유저 쓰레드를 따라 간다. 예를 들어, 모든 유저 쓰레드가 종료된 경우 JVM이 디먼 쓰레드를 종료시킨다.

자바는 자동으로 시작되고 돌아가는 디먼 쓰레드를 여러가지 갖고 있다. 앞서 언급된 가비지 컬렉터 외에도 finalizer 등이 있다.

CMD에서 jconsole을 입력하면 상세한 내용을 볼 수 있다. jconsole 툴은 현재 불러와져 있는 클래스, 메모리 사용, 실행중인 쓰레드 등을 보여준다. - 한번 실행해 봤는데 어째 접속에 실패했다. 다음에 다시 시도해보자.

* 디먼 쓰레드에 대해 기억할 점 몇가지
  * 디먼 쓰레드는 유저 쓰레드에 대해 서포터의 역할을 한다. 그 외의 목적은 없다.
  * 디먼 쓰레드의 라이프 사이클은 결국 유저 쓰레드의 라이프 사이클에 의해 결정된다.
  * 우선순위가 낮은 쓰레드이다.

* 유저 쓰레드가 없을 때 JVM이 디먼 쓰레드를 종료시키는 이유?
디먼 쓰레드의 유일한 역할은 유저 쓰레드에 대한 서포팅이다. 유저 쓰레드가 더이상 없다면 JVM이 디먼 쓰레드를 계속해서 실행할 이유가 없다.

#### :mag:sleep 메서드
Thread 클래스의 sleep() 메서드는 어느 쓰레드를 특정 시간동안 수면 상태로 만든다.

* sleep() 메서드 신택스
  1.
  ```java
  public static void sleep(long miliseconds) throws InterruptedException
  ```  
  2.
  ```java
  public static void sleep(long miliseconds, int nanos) throws InterruptedException
  ```  

#### :mag:Compare-And-Swap
Compare and swap은 동시성을 가진 알고리즘을 설계할 때 사용하는 테크닉이다. 기본적으로, compare and swap은 변수의 expected value(예상값)과 concrete value(확정값)을 비교한 뒤 두 값이 같은 경우 변수의 값을 새로운 변수로 교환한다. Compare and swap에 대한 설명은 언뜻 복잡하게 들릴 수 있는데, 일단 이해하고 나면 간단한 컨셉이다.

#### :mag:Volatile
자바의 volatile 키워드는 변수를 "메인 메모리에 보관된다"고 표시하기 위해 사용된다. 더 자세히 말하자면, volatile 변수는 CPU 캐쉬가 아니라 컴퓨터의 메인 메모리가 읽고 쓰게 된다.

### :star:Deadlock(교착상태)
Deadlock(교착상태)는 두개 이상의 쓰레드가 lock을 얻기 위해 blocked 상태로 대기하고 있는데 해당 락을 교착상태의 다른 쓰레드가 들고있는 상태이다. 하나의 락을 여러개의 쓰레드가 필요로 하고, 동시에 접근하나 서로 다른 순서로 얻어가는 상황에서 발생할 수 있다.

더 자세히 알아보기 위해 아래 글도 살펴보자.
https://rightnowdo.tistory.com/entry/JAVA-concurrent-programming-교착상태Dead-Lock

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/runnable-interface-in-java  
https://www.javatpoint.com/life-cycle-of-a-thread  
https://www.javatpoint.com/can-we-start-a-thread-twice  
https://www.javatpoint.com/priority-of-a-thread  
https://www.javatpoint.com/java-thread-setpriority-method  
https://www.javatpoint.com/thread-scheduler-in-java  
https://www.geeksforgeeks.org/main-thread-java/  
https://stackoverflow.com/questions/2213340/what-is-a-daemon-thread-in-java  
https://www.javatpoint.com/daemon-thread  
https://www.javatpoint.com/sleep()-method  
http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html  
http://tutorials.jenkov.com/java-concurrency/volatile.html  
http://tutorials.jenkov.com/java-concurrency/deadlock.html  