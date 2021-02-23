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
| Errors(에러)                                                  | Exception(예외)                                                                                                                                     |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| 핸들링이 불가능하다                                           | try-catch나 throw를 통해 예외 상태를 복구할 수 있다                                                                                                 |
| 모든 에러는 Unchecked 타입이다                                | Checked와 Unchecked 타입이 있다                                                                                                                     |
| 에러는 대부분 프로그램 작동 환경에 의해서 발생한다            | 프로그램 자체가 문제를 야기한다                                                                                                                     |
| 런타임에서 발생하며 컴파일러는 인지하지 못한다                | 런타임에서 발생하나 Checked 타입은 컴파일러가 인지한다                                                                                              |
| Package java.lang.Error                                       | Package java.lang.Exception                                                                                                                         |
| e.g. java.lang.StackOverflowError, java.lang.OutOfMemoryError | e.g. Checked Exceptions - SQLException, IOException Unchecked Exceptions - ArrayIndexOutOfBoundException, NullPointerException, ArithmeticException |

#### :mag:Checked Exception vs Unchecked Exception

### :star:자바에서 예외 처리 방법 (try, catch, throw, throws, finally)

### :star:RuntimeException과 RE가 아닌 것의 차이는?

### :star:커스텀한 예외 만드는 방법


-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/exception-handling-in-java  
https://edu.goorm.io/learn/lecture/41/%EB%B0%94%EB%A1%9C%EC%8B%A4%EC%8A%B5-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9-%EC%9E%90%EB%B0%94-java/lesson/39411/%EC%98%88%EC%99%B8%EC%9D%98-%EC%84%A0%EC%A1%B0-throwable  
https://programming.guide/java/list-of-java-exceptions.html  
https://www.geeksforgeeks.org/errors-v-s-exceptions-in-java/  