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

    System.out.println("예외 처리 종료. 다음 코드 수행.");    
    
  }  
}  
```

>실행 결과:  
>Arithmetic Exception 예외 발생.  
>예외 처리 종료. 다음 코드 수행.  

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
The Java throw keyword is used to explicitly throw an exception.

We can throw either checked or uncheked exception in java by throw keyword. The throw keyword is mainly used to throw custom exception. We will see custom exceptions later.

#### :mag:throws
The Java throws keyword is used to declare an exception. It gives an information to the programmer that there may occur an exception so it is better for the programmer to provide the exception handling code so that normal flow can be maintained.

Exception Handling is mainly used to handle the checked exceptions. If there occurs any unchecked exception such as NullPointerException, it is programmers fault that he is not performing check up before the code being used.

* Why use java throws?
Now Checked Exception can be propagated (forwarded in call stack).

It provides information to the caller of the method about the exception.

* throw vs throws
https://www.javatpoint.com/difference-between-throw-and-throws-in-java 테이블 작성

#### :mag:Unchecked 예외를 떠넘기기 (throw 없이)
An exception is first thrown from the top of the stack and if it is not caught, it drops down the call stack to the previous method,If not caught there, the exception again drops down to the previous method, and so on until they are caught or until they reach the very bottom of the call stack.This is called exception propagation.
Rule: By default Unchecked Exceptions are forwarded in calling chain (propagated).
Rule: By default, Checked Exceptions are not forwarded in calling chain (propagated).

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

   System.out.println("다음 코드 수행.");  

  }  

}  
```

>실행 결과:  
>예외 처리.  
>다음 코드 수행.  

In the above example exception occurs in m() method where it is not handled,so it is propagated to previous n() method where it is not handled, again it is propagated to p() method where exception is handled.

Exception can be handled in any method in call stack either in main() method,p() method,n() method or m() method.

#### :mag:메서드 오버라이딩과 예외처리
There are many rules if we talk about methodoverriding with exception handling. The Rules are as follows:
* If the superclass method does not declare an exception
  * If the superclass method does not declare an exception, subclass overridden method cannot declare the checked exception but it can declare unchecked exception.
* If the superclass method declares an exception
  * If the superclass method declares an exception, subclass overridden method can declare same, subclass exception or no exception but cannot declare parent exception.

### :star:커스텀한 예외 만드는 방법
If you are creating your own Exception that is known as custom exception or user-defined exception. Java custom exceptions are used to customize the exception according to user need.

By the help of custom exception, you can have your own exception and message.

Let's see a simple example of java custom exception.
```
class InvalidAgeException extends Exception{  
 InvalidAgeException(String s){  
  super(s);  
 }  
}  
```

```
class TestCustomException1{  
  
   static void validate(int age)throws InvalidAgeException{  
     if(age<18)  
      throw new InvalidAgeException("not valid");  
     else  
      System.out.println("welcome to vote");  
   }  
     
   public static void main(String args[]){  
      try{  
      validate(13);  
      }catch(Exception m){System.out.println("Exception occured: "+m);}  
  
      System.out.println("rest of the code...");  
  }  
}  
```

Output:Exception occured: InvalidAgeException:not valid
       rest of the code...

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