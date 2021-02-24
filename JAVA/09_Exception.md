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
에러와 예외는 모두 java.lang.Throwable class를 상속한다. 에러는 예외 처리로는 해결할 수 없는 상태이며, 발생할 경우 비정상적으로 프로그램이 종료하게 된다. 에러는 unchecked type에 속하며 대부분 런타임에서 JVM이나 시스템 문제에 의해 발생한다. 대표적인 예로 StackOverFlow, Out of memory, System crash 등이 있다.

* Exceptions(예외)는 정상적인 애플리케이션에서 Handling(예외 처리) 할 수 있는 문제를 가진 Condition(상태)를 지칭한다.  
에외는 런타임에서 발생하며 프로그램의 종료를 야기할 수 있으나 try, catch, throw 등의 예외처리 키워드들을 통해 프로그램 내에서 해결할 수 있다. 에외는 두가지 카테고리로 분류되는데, checked 와 unchecked 로 나뉜다. 다음장에서 두가지 분류에 대해 자세히 알아보겠다.

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

><b>하지만 위의 예제에서 그렇듯, Unchecked 타입의 예외는 개발자의 실수로 발생한 경우가 많으며 코드의 수정으로 해결되는 경우가 많다. 가능하면 코드 수정을 통해 해결하되, 통제 밖의 상황에서 발생할 수 있는 Uncheck 타입의 예외의 경우, 예외 처리 하는 것은 가능하긴 하다.</b>

#### :mag:왜 Checked와 Unchecked 두가지로 예외를 나누어 놨을까?
Unchecked 타입에 속하는 런타임 예외, 에러, 그리고 그들의 하위 클래스들에 대해서 자바는 예외처리를 강제하지 않는다. 프로그래머의 입장에서, Unchecked 타입의 예외와 에러만 발생시키도록 코드를 짜거나, 모든 하위클래스 예외들을 런타임 예외를 상속하도록 만들게 되는 경우 예외처리를 할 필요가 없다. 그 두가지 꼼수를 사용해서 성가신 컴파일러 에러나 귀찮은 예외처리를 피해갈 수 있다. 언뜻 간편한 코딩 방법으로 보일 수 있지만, 이는 예외 처리 기능의 존재 이유에서 벗어나며, 그렇게 작성된 클래스를 다른 사람이 사용할때 문제를 일으킬 수 있다.

자바를 설계할 때 왜 Checked 예외를 갖는 메서드는 강제적으로 예외처리를 하게 했을까? 메서드로 부터 던져질 수 있는 모든 예외는 해당 메서드의 프로그래밍 인터페이스의 일부이다. 메서드를 호출하는 입장에서는 해당 메서드에서 어떤 예외가 처리될 수 있는지를 알아야 그에 대한 결정을 내릴 수 있다. 메서드의 "예외"는 "변수"나 "리턴값"과 마찬가지로 메서드의 프로그래밍 인터페이스의 일부분이다.

다음으로 떠오르는 질문은, "메서드의 API(application programming interface)에 처리 가능한 예외를 포함해서 작성하는것이 그렇게 중요하다면, 런타임 예외도 작성해야 하는것 아닌가?" 이다. 런타임 예외는 프로그래밍에서 오는 문제에서 발생한다. 그러므로 해당 API의 클라이언트 코드에서 런타임 에러를 해결하거나 예외 처리 하기를 기대하기 어렵다. 예를 들어, 숫자를 0으로 나누려고 시도하여 발생하는 arithmetic exceptions, Null을 통해서 객체에 접근하려 시도하여 발생하는 pointer exceptions, 올바르지 않은 인덱스의 배열에 접근하려 시도하여 발생하는 indexing exceptions등이 있다.

런타임 예외는 프로그램의 어디에서나 발생할 수 있고 얼마든지 많이 발생할 수 있다. 모든 메서드 선언마다 런타임 예외에 대해 예외처리를 해줘야 한다면 프로그램은 너저분해질 수 밖에 없고 역할을 파악하기 어려워 질것이다. 그러므로 런타임 예외를 예외 처리 하는 것이 가능하다고는 하나, 컴파일러가 강제하지는 않는다.

관례적으로 런타임 예외를 던지는 경우도 있는데, 사용자가 메서드를 올바르지 않게 호출할 때 이다. 예를 들어, 메서드는 arguments(인자)에 Null 값이 잘못 들어왔는지 확인할 수 있다. Null 값을 가진 인자가 있다면, 메서드는 NullPointerException을 해결하도록 강제한다. 여기에서 NullPointerException은 Unchecked 예외이다.

대부분의 상황에서, 단순히 예외 처리를 피하려는 목적으로 런타임 예외를 던지거나 상속하면 안된다.

정리해 보자면, 클라이언트가 충분히 처리할 수 있는 예외라면, Checked 예외로 작성하면 된다. 클라이언트가 해결할 수 없는 예외라면, Unchecked 예외로 작성하면 된다.


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