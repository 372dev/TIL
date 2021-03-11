# Java_10_Multithreading(Concurrency)

## :muscle:Multithreading in Java(자바의 멀티 쓰레딩) / Concurrency(동시성)
자바는 Multithread language(멀티 쓰레딩 언어)이다. 멀티 쓰레딩이라, 그러면 싱글 쓰레딩 언어도 있을까? 싱글 쓰레딩 언어도 있는데, Python이나 JavaScript가 이에 속한다. 여기서는 자바의 멀티 쓰레딩이 무엇인지 살펴보자.

멀티 쓰레딩 언어를 효과적으로 활용하기 위해서, monitor와 lock에 대한 기본적인 사실들을 알고 있는 것이 좋다. 아래 리스트에서 이에 대해 나열해 본다.

* Synchronization(동기화)가 보호하는 대상은 코드 자체가 아니라 객체와 메모리이다.
* 동기화는 쓰레드 간의 협력 매커니즘이다. 하나의 버그가 협력 모델을 깰 수 있고 이는 보다 큰 문제를 불러올 수 있다.
* monitor를 acquiring(획득)하는 것은 다른 쓰레드가 해당 모니터를 획득하는 것을 방지할 뿐이다. 객체 자체를 보호하지는 못한다.
* Unsynchronized(비동기성) 메서드는 객체의 monitor가 잠겨있다고 하더라도 can see (and modify) inconsistent state. < inconsistent state란 무엇인가? 먼저 알아보고 돌아오자.
* Object[]를 잠그는 것은 각각의 객체를 잠그는 것은 아니다.
* 기본 자료형은 not mutable(불변)이다. 그러므로 잠글 수 없고 잠글 필요도 없다.
* 인터페이스에서는 메서드 선언부에 synchronized를 사용할 수 없다.
* Inner classes(중첩 클래스)는 syntactic sugar(편의를 위한 구문/구조)일 뿐이다. 그러므로 중첩 클래스에 적용된 lock은 enclosing class(중첩하는 바깥 클래스)에 아무런 영향이 없고 반대로도 마찬가지이다.
* 자바의 lock은 reentrant(동시성이 보장되는 기능)이다. 그러므로 monitor를 갖고있는 쓰레드가 동일한 모니터를 지닌 동기화된 블럭을 만나더라도 충돌 없이 접근할 수 있다.

무슨 말인지 하나도 모르겠다. 하나 하나 자세히 살펴보자.

### :star:Concurrency
동시성은 한번에 한가지 업무를 수행하는 대신 프로그램의 여러 업무를 동시에 수행하는 것이다. 이 동시성을 통해, 활용되지 않고 있는 운영체제와 하드웨어의 잠재력을 수면 위로 끌어올릴 수 있다. 예를들어 요즘 사용되는 CPU는 여러개의 코어를 담고 있다. 프로그램은 업무를 수행하며 여러개의 코어를 활용할 수 있는 경우가 있을것이고 그렇게 함으로 업무를 훨씬 빠르게 끝마칠 수 있을 것이다. 이 <b>동시성의 중심에는 쓰레드가 있다</b>.

### :star:lock
여기서 lock이란 무엇인가? 자바의 모든 객체는 고유한 lock을 지닌다. synchronized 키워드가 사용될 때 마다, lock은 중요한 존재가 된다. 쓰레드가 주어진 객체에 대해 synchronized 메서드를 실행하려 할 때. 쓰레드는 먼저, 해당 객체의 lock을 구해야 한다. 쓰레드는 lock을 구한 이후에 synchronized 메서드를 실행하도록 허용된다. 메서드의 실행이 끝나면 쓰레드는 자동적으로 lock을 버린다. 내부에서 lock을 구하고 버리는 과정은 JVM에 의해 이뤄지며 프로그래머에게는 이에 관여할 책임이 없다.

* lock을 사용하는 이유
  1. 중요 객체 / 메모리에 대하여 Mutual Exclusion(상호 배제) 제공. 즉, 공유하는 데이터에 대해서 여러 스레드 중에 한 스레드만 접근할 수 있도록 허용 및 제한 하는 것.
  2. 스레드 간의 협업 또는 동기화의 역할을 수행. 어떠한 작업을 완료하거나 특정 상태에 도달할 경우 다른 스레드에 알려주어 해당 스레드가 동작할 수 있도록 하는 것.
  3. 부수적인 효과인 데이터의 가시성. lock/unlock을 호출하기 전에 변경된 데이터에 대해서 메모리로 반영하는 것.

#### :mag:Object level lock vs Class level lock

1. Object level lock : 객체 lock을 사용한다는 것은 non-static 메서드 혹은 블락을 동기화 한다는 것이다. 이는 해당 "객체"의 메서드나 블럭이 한번에 하나의 쓰레드에 의해서만 접근할 수 있게 하는 것이다. non-static 데이터를 보호하기 위해서 사용된다. 객체 단위로 locking 할 수 있다.

2. Class level lock : 클래스 lock을 사용한다는 것은 static 메서드 혹은 블락을 동기화 한다는 것이다. 이는 해당 "클래스"의 메서드나 블럭이 한번에 하나의 쓰레드에 의해서만 접근할 수 있게 하는 것이다. static 데이터를 보호하기 위해서 사용된다. 클래스 단위로 locking 할 수 있다.

읽어 보아도, 예제를 보아도 이해를 못했는데, 두가지 방식을 번갈아 가며 코드를 돌려 실행 결과를 보니 차이가 보였다!

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
lock과 monitor의 차이점이 무엇일까?

* 모니터는 Intrinsic Lock 혹은 Built-in Lock이라고 하며, 자바 1.5 부터 제공되는 락은 Explicit Lock 혹은 Reentrant Lock이라 한다.
* 두가지 모두 공유되는 객체와 메모리를 보호하기 위해 사용된다.
* 기능상의 차이점

|   | Monitor<br>(Intrinsic Lock)   | ReentrantLock<br>(Explicit Lock)  |
|-  |-  |-  |
| 재진입   | 가능    | 가능    |
| 락 시도  | 미제공   | 제공    |
| Fairness  | 미제공   | 제공    |
| Interruption in locked    | 불가능   | 가능    |
| Lock 접근 스레드 정보    | 미제공   | 제공    |

### :star:자바의 쓰레딩 모델
자바의 멀티 쓰레딩은 다수의 쓰레드를 동시에 실행하는 과정이다. 

쓰레드는 lightweight process(LWP / 경량 프로세스)이다. 반대 개념은 heavyweight process(HWP)가 되겠는데, 운영체제 아래 처리되는 보통의 프로세스가 HWP이다. 쓰레드는 가장 작은 프로세싱 단위이다.
멀티 프로세싱 그리고 멀티 쓰레딩 모두 멀티 태스킹을 위해서 쓰인다. 그러나 멀티 쓰레딩이 멀티 프로세싱보다는 우선적으로 사용되는데 이는 멀티 쓰레딩이 공유되는 메모리 공간을 사용하고 그에 따라 메모리를 절약할 수 있기 때문이다. 또한 쓰레드간 작업을 전환하는 것도 멀티 프로세싱의 방식보다 시간이 적게 걸린다.

#### :mag:Multi Threading vs Multi Processing

| 성격    | Multi Processing  | Multi Threading   |
|-  |-  |-  |
| 정의    | 시스템이 다수의 프로세서를<br>사용하고, 그 프로세서들이 <br>다수의 작업을 각각 수행하는 것    | 작업을 다수의 하위 작업(쓰레드)로<br>나누고 각각의 쓰레드는<br>각각의 경로로 작업을 수행하는 것     |
| 목적/수단     | 성능을 높이기 위해 CPU를 추가한다  | 성능을 높이기 위해 하나의<br>작업을 여러개로 나눈다    |
| 동시성   | 두개 이상의 작업이 동시에<br>진행된다    | 하나의 작업에 대한 하위 작업들이<br>동시에 진행된다    |
| 경제성   | 경제적이지 않다  | 경제적이다     |
| 효율성   | 효율적이다     | 효율적이지 않다  |

#### :mag:Advantages of Java Multithreading(멀티 쓰레딩의 장점)
* 성능의 향상
* 간략화 되고 흐름을 볼 수 있는 코딩
* 동시적이고 병행적인 작업의 수행
* 향상된 cache 공간 자원 활용
* 유지보수 비용의 절감
* 향상된 CPU 자원 활용

#### :mag:Disadvantages of Java Multithreading(멀티 쓰레딩의 단점)
* 복잡한 디버깅 / 테스팅 절차
* 작업의 배경에서 Context switch가 요구된다
  * Context switch? CPU가 한 개의 Task(Process / Thread) 를 실행하고 있는 상태에서 Interrupt 요청에 의해 다른 Task 로 실행이 전환되는 과정에서 기존의 Task 상태 및 Register 값들에 대한 정보 (Context)를 저장하고 새로운 Task 의 Context 정보로 교체하는 작업
  * see https://jins-dev.tistory.com/entry/컨텍스트-스위치Context-Switching-에-대한-정리
* deadlock 발생의 가능성이 늘어난다
* 코드 작성의 난이도가 높아진다
* 예측하기 어려운 결과물

#### :mag:자바 쓰레딩 모델의 세가지 핵심 컨셉

1. 공유되고, 가시적이고, 가변적인 상태
프로세스가 진행되는 중에 객체들이 여러 쓰레드들에 의해 자유롭게 공유돤다는 것이고, 객체와 연결된 어느 쓰레드에 의해서든 객체가 변화(상태의 변경)될 수 있다는 것이다.

2. 선점적인 쓰레드 스케쥴링
운영체제의 쓰레드 스케쥴러는 여러 쓰레드들의 작업량과 순서를 마음대로 변경할 수 있다.

3. lock에 의한 객체의 보호
lock은 올바르게 사용하기 쉽지 않다. 그리고 lock의 state(상태)는 vulnerable(예민하고 불안정)해서 심지어 read operations(읽어오기 작업)을 할 때에도 주의해야 한다.

이 세가지 동시성 컨셉을 통해서, 멀티 쓰레딩 프로그래밍이 왜 개발자에게 두통을 안겨 주는지 알 수 있다.

### :star:Thread 클래스
자바 클래스에 동시성을 부여하기 위해서 가장 먼저 필요한 클래스는 ```java.lang.Thread``` 클래스이다. 이는 자바에서의 모든 동시성 개념의 기반이다.
Thread 클래스는 다수의 생성자와 메서드를 제공하며 이는 쓰레드 안에 작업을 생성하고 수행하기 위해 이용된다. Thread 클래스는 Object 클래스를 상속하며 Runnable 인터페이스를 구현한다.

* 흔히 사용되는 Thread 클래스 생성자
  * Thread()
  * Thread(String name)
  * Thread(Runnable r)
  * Thread(Runnable r,String name)

* 흔히 사용되는 Thread 클래스 메서드
  * public void run(): is used to perform action for a thread.
  * public void start(): starts the execution of the thread.JVM calls the run() method on the thread.
  * public void sleep(long miliseconds): Causes the currently executing thread to sleep (temporarily cease execution) for the specified number of milliseconds.
  * public void join(): waits for a thread to die.
  * public void join(long miliseconds): waits for a thread to die for the specified miliseconds.
  * public int getPriority(): returns the priority of the thread.
  * public int setPriority(int priority): changes the priority of the thread.
  * public String getName(): returns the name of the thread.
  * public void setName(String name): changes the name of the thread.
  * public Thread currentThread(): returns the reference of currently executing thread.
  * public int getId(): returns the id of the thread.
  * public Thread.State getState(): returns the state of the thread.
  * public boolean isAlive(): tests if the thread is alive.
  * public void yield(): causes the currently executing thread object to temporarily pause and allow other threads to execute.
  * public void suspend(): is used to suspend the thread(depricated).
  * public void resume(): is used to resume the suspended thread(depricated).
  * public void stop(): is used to stop the thread(depricated).
  * public boolean isDaemon(): tests if the thread is a daemon thread.
  * public void setDaemon(boolean b): marks the thread as daemon or user thread.
  * public void interrupt(): interrupts the thread.
  * public boolean isInterrupted(): tests if the thread has been interrupted.
  * public static boolean interrupted(): tests if the current thread has been interrupted.

#### :mag:Thread safety
Thread safety(쓰레드 안전성)이 무엇인지 설명하는 것은 정말 어렵다. 구글에서 검색을 해봐도 아래와 비슷한 수많은 "정의"들이 나온다.

1. Thread-safe code(쓰레드 세이프 코드)는 여러 쓰레드가 동시에 해당 작업을 하더라도 문제 없이 작동하는 코드이다.
2. 공유되는 data structures(자료 구조)에 대해 여러 쓰레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음을 뜻한다.

이외에도 비슷한 정의가 많이 검색된다.

위와 같은 정의들은 사실 핵심적인 의미를 담지 못하고 있다고 생각되지 않은가? 틀린 말은 아니기에 이런 정의들이 필요 없다고 할 수는 없지만, 실용적인 도움이나 의미있는 관점을 제공하지 못하는게 사실이다. thread-safe class(쓰레드 세이프한 클래스)와 안전하지 않은 것의 차이는 무엇인가? "safe(안전)"하다는게 무슨 의미인가?

##### thread safety에서의 Correctness(올바름)이란?

Thread safety에 대한 설명의 중심에는 correctness(올바름)이라는 컨셉이 있다. 그러므로 thread safety를 정의하기 전에 나는 먼저 "올바름"이 무엇인지 알아야 한다.

>Correctness(올바름)은 class가 스스로의 specification(규격/명세)를 준수하는 것이다.

잘 작성된 class specification(클래스 명세)는 클래스의 변경되는 상태에 대한 모든 정보를 담고 있어야 하며, 기능을 수행한 이후의 상태에 대한 정보도 가지고 있어야 한다. 나는 명세에 대한 개념이 부족하며 정확하게 클래스의 명세를 작성하지 않는데, 명세가 정확한지 아닌지 알 수나 있을까? 알 수 없지만 그렇다고 해서 클래스를 사용하지 않을 수는 없다. 일단 코드가 문제 없이 작동한다고 생각되면 올바르다고 생각한다. 이 "자신감"이 내 수준에서 "올바름"에 그나마 근접할 수 있는 것이다.

"올바름"이 무엇인지 그나마 이해할 수 있는 수준에서 정의해 보았으니 이제 thread safety를 조금이라도 더 또렷하게 정의해보자.

>클래스는 (런타임 환경에서 스케쥴링이 이뤄지고 쓰레드 순서가 바뀌는 것과 상관 없이, 그리고 코드가 호출될 때 추가적인 동기화나 조율이 필요 없이) 여러 개의 쓰레드가 동시에 접근해도 정상적으로 작동한다면, thread-safe 하다.

여기에 정의된 "올바름"이 너무 두루뭉술하다고 느껴진다면, 그 대신 "thread safe한 클래스는 멀티 쓰레딩 환경에서 작업을 해도 싱글 쓰레딩 환경에서 작업을 하는 것과 차이가 없는 클래스이다" 라고 생각해도 괜찮다. Thread safe인 클래스들은 동기화 작업을 캡슐화 하기 떄문에 클라이언트는 직접 동기화 작업을 할 필요가 없다.

##### 예제, A Stateless Servlet

thread safe인 클래스의 좋은 예는 필드값, 다른 클래스의 필드값, 참조변수 등이 없는 Stateless 서블릿이다.

```java
public class StatelessFactorizer implements Servlet {
    public void service(ServletRequest req, ServletResponse resp) {
        BigInteger i = extractFromRequest(req);
        BigInteger[] factors = factor(i);
        encodeIntoResponse(resp, factors);
    }
}
```

특정 연산에서의 임시적인 상태는 해당 쓰레드의 스택에 있는 로컬 변수에만 존재한다. 그리고 작업중인 쓰레드에 의해서만 접근이 가능하다. ```StatelessFactorizer``` 클래스에서 작업중인 하나의 쓰레드는 동일한 ```StatelessFactorizer``` 클래스에서 작업하는 다른 쓰레드의 결과물에 영향을 주지 못한다. 이는 두개의 다른 쓰레드가 서로 상태를 공유하지 않기 떄문이다. 마치 서로 다른 인스턴스에서 작업하는 것 마냥 행동한다. stateless인 객체에 접근한 쓰레드의 작업이 다른 쓰레드의 작업에 대한 "올바름"에 영향을 주지 못하기 때문에, stateless 객체는 thread safe 하다.

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/multithreading-in-java  
https://howtodoinjava.com/java-concurrency-tutorial/  
https://www.geeksforgeeks.org/object-level-class-level-lock-java/  
https://bestugi.tistory.com/40  
https://www.geeksforgeeks.org/difference-between-multiprocessing-and-multithreading/  
https://www.javatpoint.com/multiprogramming-vs-multiprocessing-vs-multitasking-vs-multithreading  
https://java2blog.com/object-level-locking-vs-class-level-locking-java/  
https://www.multisoftvirtualacademy.com/blog/common-advantages-and-disadvantages-of-multithreading-in-java/  
https://jins-dev.tistory.com/entry/컨텍스트-스위치Context-Switching-에-대한-정리  
https://www.javatpoint.com/creating-thread  
https://howtodoinjava.com/java/multi-threading/what-is-thread-safety/  