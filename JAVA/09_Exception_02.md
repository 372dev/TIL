# Java_09_Exception_02

## :muscle:Exception Handling(예외 처리)

### :star:자바의 예외 처리 방법

#### :mag:try-catch

* try block
Java try block is used to enclose the code that might throw an exception. It must be used within the method.

If an exception occurs at the particular statement of try block, the rest of the block code will not execute. So, it is recommended not to keeping the code in try block that will not throw an exception.

Java try block must be followed by either catch or finally block.

* catch block
Java catch block is used to handle the Exception by declaring the type of exception within the parameter. The declared exception must be the parent class exception ( i.e., Exception) or the generated exception type. However, the good approach is to declare the generated type of exception.

The catch block must be used after the try block only. You can use multiple catch block with a single try block.

* Multiple Catch Block
A try block can be followed by one or more catch blocks. Each catch block must contain a different exception handler. So, if you have to perform different tasks at the occurrence of different exceptions, use java multi-catch block.
  * At a time only one exception occurs and at a time only one catch block is executed.
  * All catch blocks must be ordered from most specific to most general, i.e. catch for ArithmeticException must come before catch for Exception.

```
public class MultipleCatchBlock1 {  
  
    public static void main(String[] args) {  
          
           try{    
                int a[]=new int[5];    
                a[5]=30/0;    
               }    
               catch(ArithmeticException e)  
                  {  
                   System.out.println("Arithmetic Exception occurs");  
                  }    
               catch(ArrayIndexOutOfBoundsException e)  
                  {  
                   System.out.println("ArrayIndexOutOfBounds Exception occurs");  
                  }    
               catch(Exception e)  
                  {  
                   System.out.println("Parent Exception occurs");  
                  }             
               System.out.println("rest of the code");    
    }  
}  
```

Arithmetic Exception occurs
rest of the code

* Nested Try
The try block within a try block is known as nested try block in java.
  * Why use nested try block?
  Sometimes a situation may arise where a part of a block may cause one error and the entire block itself may cause another error. In such cases, exception handlers have to be nested.


#### :mag:finally
Java finally block is a block that is used to execute important code such as closing connection, stream etc.

Java finally block is always executed whether exception is handled or not.

Java finally block follows try or catch block.

* Why use java finally?
Finally block in java can be used to put "cleanup" code such as closing a file, closing connection etc.

* final vs finally vs finalize
https://www.javatpoint.com/difference-between-final-finally-and-finalize 테이블 작성

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

```
class TestExceptionPropagation1{  
  void m(){  
    int data=50/0;  
  }  
  void n(){  
    m();  
  }  
  void p(){  
   try{  
    n();  
   }catch(Exception e){System.out.println("exception handled");}  
  }  
  public static void main(String args[]){  
   TestExceptionPropagation1 obj=new TestExceptionPropagation1();  
   obj.p();  
   System.out.println("normal flow...");  
  }  
}  
```

Output:exception handled
       normal flow...

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