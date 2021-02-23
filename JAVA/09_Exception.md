# Java_09_Exception

## :muscle:Exception Handling(예외 처리)
* Exception(예외)란 무엇일까? 사전적인 의미로 Abnormal condition(비정상적인 상태)를 말한다. 자바에서의 예외는 장상적인 프로그램의 흐름을 방해하는 상황이다.
* Exception handling(예외 처리)는 무엇일까? 애플리케이션의 정상적인 흐름을 유지하도록 하기 위해 사용하는 기술이다. Exception(예외)는 애플리케이션의 정상적인 흐름을 방해하며 때문에 이를 방지하고자 Exception handling(예외 처리)를 사용한다.

### :star:자바가 제공하는 예외 계층 구조
![Exception_Throwable_Diagram](https://raw.githubusercontent.com/372dev/TIL/main/JAVA/img/09_Exception_Throwable_Diagram.jpg)

위 다이어그램은 Throwable 클래스의 구조를 보여준다. Throwable은 예외 클래스들의 공통적인 조상이다. 모든 예외 클래스들이 가지고 있는 공통 메서드를 정의하지만, 이 클래스를 직접 사용하지는 않는다. 이 클래스 외에도 Exception(예외)와 Error(에러)를 관장하는 클래스는 여러가지가 있다.

* Package java.util
  * InavlidPropertiesFormatException - (checked)
  * IllegalFormatException
  * ...
* Package java.io
  * IOError
  * IOException - (checked)
  * UncheckedIOException
* Package java.awt
  * AWTError
  * AWTException - (checked)
  * ...
* Package java.awt.color, java.awt.datatransfer, java.awt.dnd, java.awt.geom, java.awt.image, java.awt.image
* Package java.beans
  * IntrospectionException - (checked)
  * PropertyVetoException - (checked)
* ... see [reference](https://programming.guide/java/list-of-java-exceptions.html)

#### :mag:Exception vs Error
* Error(에러)는 정상적인 애플리케이션에서 Handling(예외 처리) 할 수 없는 심각한 문제를 가진 Condition(상태)를 지칭한다.  
에러와 예외는 모두 java.lang.Throwable class를 상속한다. 에러는 예외 처리로는 해결할 수 없는 상태이며 비정상적으로 프로그램이 종료하게 된다. 에러는 unchecked type에 속하며 대부분 런타임에서 발생한다. 대표적인 예로 Out of memory 에러와 System crash 에러가 있다.

* Exceptions(예외)는 정상적인 애플리케이션에서 Handling(예외 처리) 할 수 있는 문제를 가진 Condition(상태)를 지칭한다.  
에외는 런타임에서 발생하며 프로그램의 종료를 야기할 수 있으나 try, catch, throw 등의 예외처리 키워드들로 해결할 수 있다. 에외는 두가지 카테고리로 분류되는데, checked 와 unchecked 로 나뉜다. 다음장에서 두가지 분류에 대해 자세히 알아보겠다.

* 에러와 예외의 비교

| Errors(에러)  | Exception(예외)   |
|-  |-  |
| 핸들링이 불가능하다  | try-catch나 throw를 통해 예외 상태를 복구할 수 있다  |
| 모든 에러는 Unchecked 타입이다   | Checked와 Unchecked 타입이 있다   |
| 에러는 대부분 프로그램 작동 환경에 의해서 발생한다  | 프로그램 자체가 문제를 야기한다   |
| 런타임에서 발생하며 컴파일러는 인지하지 못한다   | 런타임에서 발생하나 Checked 타입은 컴파일러가 인지한다   |
| Package java.lang.Error   | Package java.lang.Exception   |
| e.g.<br>java.lang.StackOverflowError,<br>java.lang.OutOfMemoryError   | e.g.<br>Checked Exceptions - SQLException, IOException<br>Unchecked Exceptions - ArrayIndexOutOfBoundException,<br>NullPointerException, ArithmeticException  |

#### :mag:Checked Exception vs Unchecked Exception
1. Checked 타입의 예외 : 컴파일 단계에서 확인되는 예외. 메서드 안에서 예외가 발생하는 경우, 해당 메서드는 try/catch 등으로 예외처리를 하거나 throws 키워드를 통해 예외를 명시해야 한다.

대표적으로 다음과 같은 예외가 있다.

* ClassNotFoundException
* IOException
* FileNotFoundException
* SQLException
* NoSuchMethodException

메서드가 "C:\test\text.txt"의 경로에서 파일의 내용을 읽어와 출력하려 하는 예제를 살펴보자. 메인 메서드가 FileReader() 객체를 생성하려 하는데 해당 객체는 Checked Exception인 FileNotFoundException을 발생시키기 때문에 프로그램이 컴파일 되지 않는다. 메인메서드는 또한 BufferedReader의 readLine()과 close() 메서드를 이용하는데, 이들 메서드들은 IOException을 발생시킨다.

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class Main {
    public static void main(String[] args) {
        FileReader file = new FileReader("C:\\test\\text.txt");
        BufferedReader fileInput = new BufferedReader(file);

        // "C:\test\text.txt"의 내용을 위에서부터 세줄 출력한다.
        for (int counter = 0; counter < 3; counter++)
            System.out.println(fileInput.readLine());

        fileInput.close();
    }
} 
```

위의 코드를 정상적으로 작동시키기 위해서, throws 키워드를 통해서 예외를 명시하거나, try-catch 구문을 이용해야 한다.

```java
import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;

public class Main {
    public static void main(String[] args) throws FileNotFoundException {
        FileReader file = new FileReader("C:\\test\\text.txt");
        BufferedReader fileInput = new BufferedReader(file);

        // "C:\test\text.txt"의 내용을 위에서부터 세줄 출력한다.
        for (int counter = 0; counter < 3; counter++)
            System.out.println(fileInput.readLine());

        fileInput.close();
    }
} 
```

FileReader 객체에 대한 FileNotFoundException 예외처리가 이뤄졌지만 여전히 BufferedReader 객체의 readLine, close 메서드에서 IOException을 필요로 한다.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException {
        FileReader file = new FileReader("C:\\test\\text.txt");
        BufferedReader fileInput = new BufferedReader(file);

        // "C:\test\text.txt"의 내용을 위에서부터 세줄 출력한다.
        for (int counter = 0; counter < 3; counter++)
            System.out.println(fileInput.readLine());

        fileInput.close();
    }
} 
```

IOException은 FileNotFoundException의 부모 클래스이므로 IOException에 대한 예외처리가 이루어 질 경우 FileNotFoundException은 처리해줄 필요가 없다. 이는 위의 throws 키워드를 이용하는 경우 이외에도 try/catch 키워드 등의 상황에서도 마찬가지이다.
이제 위의 코드는 컴파일 에러 없이 작동한다.

2. Unchecked 타입의 예외 : 컴파일 단계에서 확인되지 않는 예외이다. <b>RuntimeException과 Error가 Unchecked 타입에 해당한다.</b> C++ 에서는 모든 예외가 unchecked 타입이며 그러므로 컴파일러에 의해 예외 처리가 강제되지 않는다. 자바에서는 에러와 RuntimeException(런타임 예외) 클래스들이 unchecked 타입이다. 그 외의 throwable을 상속하는 모든 예외는 checked 타입이다.

대표적으로 다음과 같은 예외가 있다.

* NullPointerException
* IllegalArgumentException
* ArithmeticException
* IndexOutOfBoundsException

아래 예제를 살펴 보면, 컴파일 되는데에는 문제가 없다. 그러나 실행시에 ArithmeticException을 발생시키는데, 이는 ArithmeticException이 unchecked 타입이기 때문이다.

```java
public class Main { 
   public static void main(String args[]) { 
      int x = 10; 
      int y = 0; 
      int z = x/y; 
  } 
} 
```

Unchecked 타입의 예외도 Checked 타입과 마찬가지로 예외 처리를 해줄 수 있다.

```java
public class Main {
    public static void main(String args[]) {
        try {
            int x = 10;
            int y = 0;
            int z = x/y;
        } catch(ArithmeticException e) {
            e.printStackTrace();
            System.out.println("숫자를 0으로 나눌 수 없습니다.");
        }
    }
} 
```

<b>하지만 위의 예제에서 그렇듯, Unchecked 타입의 예외는 개발자의 실수로 발생한 경우가 많으며 코드의 수정으로 해결되는 경우가 많다. 가능하면 코드 수정을 통해 해결하되, 통제 밖의 상황에서 발생할 수 있는 Uncheck 타입의 예외의 경우, 예외 처리 하는 것은 가능하긴 하다.</b>

#### :mag:왜 Checked와 Unchecked 두가지로 예외를 나누어 놨을까?
Because the Java programming language does not require methods to catch or to specify unchecked exceptions (RuntimeException, Error, and their subclasses), programmers may be tempted to write code that throws only unchecked exceptions or to make all their exception subclasses inherit from RuntimeException. Both of these shortcuts allow programmers to write code without bothering with compiler errors and without bothering to specify or to catch any exceptions. Although this may seem convenient to the programmer, it sidesteps the intent of the catch or specify requirement and can cause problems for others using your classes.

Why did the designers decide to force a method to specify all uncaught checked exceptions that can be thrown within its scope? Any Exception that can be thrown by a method is part of the method's public programming interface. Those who call a method must know about the exceptions that a method can throw so that they can decide what to do about them. These exceptions are as much a part of that method's programming interface as its parameters and return value.

The next question might be: "If it's so good to document a method's API, including the exceptions it can throw, why not specify runtime exceptions too?" Runtime exceptions represent problems that are the result of a programming problem, and as such, the API client code cannot reasonably be expected to recover from them or to handle them in any way. Such problems include arithmetic exceptions, such as dividing by zero; pointer exceptions, such as trying to access an object through a null reference; and indexing exceptions, such as attempting to access an array element through an index that is too large or too small.

Runtime exceptions can occur anywhere in a program, and in a typical one they can be very numerous. Having to add runtime exceptions in every method declaration would reduce a program's clarity. Thus, the compiler does not require that you catch or specify runtime exceptions (although you can).

One case where it is common practice to throw a RuntimeException is when the user calls a method incorrectly. For example, a method can check if one of its arguments is incorrectly null. If an argument is null, the method might throw a NullPointerException, which is an unchecked exception.

Generally speaking, do not throw a RuntimeException or create a subclass of RuntimeException simply because you don't want to be bothered with specifying the exceptions your methods can throw.

Here's the bottom line guideline: If a client can reasonably be expected to recover from an exception, make it a checked exception. If a client cannot do anything to recover from the exception, make it an unchecked exception.


### :star:자바에서 예외 처리 방법 (try, catch, throw, throws, finally)

### :star:커스텀한 예외 만드는 방법


-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/exception-handling-in-java  
https://edu.goorm.io/learn/lecture/41/%EB%B0%94%EB%A1%9C%EC%8B%A4%EC%8A%B5-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9-%EC%9E%90%EB%B0%94-java/lesson/39411/%EC%98%88%EC%99%B8%EC%9D%98-%EC%84%A0%EC%A1%B0-throwable  
https://programming.guide/java/list-of-java-exceptions.html  
https://www.geeksforgeeks.org/errors-v-s-exceptions-in-java/  
https://www.geeksforgeeks.org/checked-vs-unchecked-exceptions-in-java/  
https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html  