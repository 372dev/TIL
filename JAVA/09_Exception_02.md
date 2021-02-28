# Java_09_Exception_02

## :muscle:Exception Handling(예외 처리)

### :star:자바의 예외 처리 방법

#### :mag:try-catch
* try 블럭
자바의 try 코드 블럭은 예외를 발생시킬 가능성이 있는 코드를 담는데 사용되며, 메서드 내부에서 사용된다.
try 블럭 내부의 특정 구문이 예외를 발생시킬 경우, 블럭 내부의 나머지 코드들은 작동되지 않는다. 그러므로, 예외를 발생시키지 않는 코드는 블럭 내부에 작성하지 않는 것이 좋다.
try 블럭에는 catch 혹은 finally 블럭이 꼭 뒤따라야 한다.

* catch 블럭
자바의 catch 코드 블럭은 파라미터 범위 안에서 예외의 타입을 선언해주는 방식으로 예외를 처리한다. 예외의 선언은 해당 예외가 상속하는 상위 클래스(Exception 클래스) 혹은 해당 예외를 사용할 수 있으나, 가급적 상세하게 해당 예외를 선언해 주는 것이 좋다.
catch 블럭은 try 블럭 뒤에 온다. 이 때, 하나의 try 블럭에 여러개의 catch 블럭이 뒤따를 수 있다.

* 다중 catch 블럭
하나의 try 블럭에 여러개의 catch 블럭이 뒤따를 수 있다. 각각의 catch 블럭은 서로 다른 예외 처리를 담당해야 한다.
그러므로, 서로 다른 예외 상황에 서로 다른 작업을 명령하고 싶다면 다중 catch 블럭을 사용하면 된다.
  * 한번에 한가지의 예외만 발생하게 되므로 한번에 한가지의 catch 블럭만 실행될 수 있다.
  * 모든 catch 블럭은 하위 클래스의 예외에 대한 처리부터 상위 클래스의 예외에 대한 처리의 순서로 정렬되어야 한다. 예를 들어 ArithmeticException의 예외처리는 Exception의 예외처리보다 먼저 와야 한다.

```java
public class MultipleCatchBlock {  
  
  public static void main(String[] args) {          

    try{    
      int a[] = new int[5];    
      a[5] = 30 / 0;

    } catch(ArithmeticException e) {
      System.out.println("Arithmetic Exception 예외 발생.");

    } catch(ArrayIndexOutOfBoundsException e) {
      System.out.println("ArrayIndexOutOfBounds 예외 발생.");  

    } catch(Exception e) {
      System.out.println("Exception 예외 발생.");  

    }

    System.out.println("예외 처리 종료. 다음 코드 수행...");    
    
  }  
}  
```

* 실행 결과

>Arithmetic Exception 예외 발생.  
>예외 처리 종료. 다음 코드 수행...  

* 중첩 try
try 블럭 내에 다른 try 블럭이 들어가 있는 경우, 중첩된 try 블럭이라고 한다.
  * 언제 try 블럭을 중첩해서 사용할까?
  상황에 따라, 코드 일부가 예외를 발생시킬 가능성이 있고 동시에 블럭 전체가 또 다른 예외를 발생시킬 수 도 있다. 이런 경우 예외처리를 중첩하여 사용한다.

#### :mag:finally
자바의 finally 코드 블럭은 connection이나 stream을 종료하는 등 중요한 코드를 수행하기 위해서 사용한다.
finally 블럭은 예외의 처리 여부와 관계 없이 무조건 실행된다.
finally 블럭은 try나 catch 블럭의 다음에 자리한다.

* 언제 finally 블럭을 사용할까?
파일을 닫고, connection을 종료하는 등의 cleanup(청소) 코드를 작성할 때 사용한다.

* final vs finally vs finalize

|   | final   | finally   | finalize  |
|-  |-  |-  |-  |
| 종류  | 키워드   | 코드 블럭   | 메서드   |
| 용도  | 클래스나 메서드, 변수 등에 대한 접근 제어를 위해<br>사용된다. final 클래스는 상속되지 못하고, final<br>메서드는 오버라이드 되지 못하며, final 변수는<br>수정이 불가능하다.  | 꼭 실행되어야 하는 중요한 코드를<br>담기 위해 사용된다. 예외 처리<br>여부에 상관없이 실행된다.   | 객체가 garbage collector에<br>의해 제거되기 전에 청소를<br>수행하는 메서드이다.   |

#### :mag:throw
자바의 throw 키워드는 예외를 명시적으로 던지기 위해서 사용된다.

checked 타입 그리고 uncheked 타입의 예외 모두 throw 키워드를 이요하여 던질 수 있다. 특히나, throw 키워드는 custom exception(커스텀 설정된 예외)를 던지는데 주로 사용된다. custom exception은 뒤에서 살펴보자.

#### :mag:throws
자바의 throws 키워드는 예외를 선언하기 위해서 사용된다. 프로그래머가 예외 처리 코드를 작성하여 정상적인 코드 흐름을 유지할 수 있도록 예외 발생의 가능성에 대한 정보를 프로그래머에게 제공한다.

* 언제 throws 키워드를 사용할까?
throws 키워드를 통해 Checked 타입의 예외를 던질 수 있다(상위 호출 계층으로 전파된다).
해당 메서드의 호출자에게 예외 정보를 전달한다.

* throw vs throws

| throw   | throws  |
|-  |-  |
| 명시적으로 예외를 던진다   | 예외를 선언한다  |
| Checked 타입의 예외는 throw 키워드 만으로 전파될 수 없다  | Checked 타입의 예외는 throw 키워드 만으로 전파될 수 있다  |
| throw 키워드에는 인스턴스가 뒤따른다  | throws 키워드에는 클래스가 뒤따른다  |
| 메서드 내부에서 사용된다   | 메서드 선언부에 사용된다   |
| 다수의 예외에 동시에 적용할 수 없다  | 다수의 예외를 동시에 던질 수 있다   |

#### :mag:Unchecked 예외의 전파 (예외를 throws 없이 묵시적으로 던지기)
예외는 콜 스택의 가장 위에서 부터 던져 지는데, 예외를 받아 처리해주지 않는 경우 콜 스택을 따라 이전 메서드로 전파된다. 마찬가지로 거기에서도 예외가 받아져서 처리되지 않는다면 다시 콜 스택을 따라 이전 메서드로 전파고 이는 예외가 처리되거나 아니면 콜 스택의 끝까지 다다를 때 까지 반복된다. 이를 예외의 전파 라고 한다.

* 예외 전파의 규칙
  * 기본적으로 Unchecked 타입의 예외는 calling chain(호출 체인)을 따라 forwarded(전달)된다. (전파된다). Checked 타입의 예외는 그렇지 않다.

```java
class TestExceptionPropagation{  

  void m() {  
    int data = 50 / 0;  
  }  

  void n() {  
    m();  
  }  

  void p() {  

    try{  
      n();  

    } catch(Exception e) {
      System.out.println("예외 처리.");

    }  
  }  

  public static void main(String args[]) {  

   TestExceptionPropagation1 obj=new TestExceptionPropagation1();  
   obj.p();  
   System.out.println("다음 코드 수행...");  

  }  
}  
```

* 실행 결과

>예외 처리.  
>다음 코드 수행...  

위의 예에서, m() 메서드에서 예외가 발생한다. 예외 처리가 되지 않았고 이는 콜 스택을 따라 n() 메서드로 전파되었다. 여기에서도 예외 처리는 되지 않았으므로 다시 p() 메서드로 전파된다. p() 메서드에서 마침내 예외 처리가 되었다.

예외는 콜 스택 중의 어느 메서드에서나 처리가 가능하다. main() 메서드, p() 메서드, n() 메서드, m() 메서드 모두 예외 처리가 가능하다.

#### :mag:메서드 오버라이딩과 예외처리
메서드 오버라이딩과 예외처리에 관련해서 몇가지 규칙이 있다.

* 상위 클래스의 메서드가 예외를 선언하지 않는 경우
  * 하위 클래스의 오버라이드 된 메서드는 checked 타입의 예외를 선언할 수 없다. 그러나 unchecked 타입의 예외는 선언할 수 있다.
* 상위 클래스의 메서드가 예외를 선언하는 경우
  * 하위 클래스의 오버라이드 된 메서드는 상위 클래스에서 선언된 예외와 동일한 예외, 혹은 해당 예외를 상속하는 하위 예외를 선언할 수 있다. 그러나 해당 예외 보다 상위 클래스의 예외는 선언할 수 없다.

### :star:커스텀한 예외 만드는 방법
custom exception(커스텀 예외)혹은 user-defined exception(사용자 설정 예외) 라고 알려진 커스텀한 예외를 만들 수 있다. 사용자의 필요에 따라 새로운 예외를 설정하는 것이 가능하다.
사용자만의 새로운 예외는 규칙 설정, 메세지 설정을 자유롭게 할 수 있다.

아래의 예에서 확인해보자.

```java
class InvalidAgeException extends Exception {  

 InvalidAgeException(String s) {  
  super(s);    
 }  
}  
```

```java
class TestCustomException{  
  
   static void validate(int age) throws InvalidAgeException {  

     if(age < 18) {
      throw new InvalidAgeException("아직 투표할 수 없어요");

      } else {
        System.out.println("투표할 수 있어요");  
        
        }

   }  
     
   public static void main(String args[]) {  

      try {  
      validate(13);  

      } catch(Exception m) {
        System.out.println("예외 발생: " + m );

      }  
  
      System.out.println("다음 코드 수행...");  
  }  
}  
```

* 실행 결과

>예외 발생: InvalidAgeException:아직 투표할 수 없어요  
>다음 코드 수행...  

-References :
https://www.javatpoint.com/try-catch-block  
https://www.javatpoint.com/multiple-catch-block-in-java  
https://www.javatpoint.com/nested-try-block  
https://www.javatpoint.com/finally-block-in-exception-handling  
https://www.javatpoint.com/difference-between-final-finally-and-finalize  
https://www.javatpoint.com/throw-keyword  
https://www.javatpoint.com/throws-keyword-and-difference-between-throw-and-throws  
https://www.javatpoint.com/difference-between-throw-and-throws-in-java  
https://www.javatpoint.com/exception-propagation  
https://www.javatpoint.com/exception-handling-with-method-overriding  
https://www.javatpoint.com/custom-exception