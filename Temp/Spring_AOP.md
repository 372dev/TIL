# Spring AOP

## :muscle:Spring AOP
One of the key components of Spring Framework is the Aspect oriented programming (AOP) framework. Aspect-Oriented Programming entails breaking down program logic into distinct parts called so-called concerns. The functions that span multiple points of an application are called cross-cutting concerns and these cross-cutting concerns are conceptually separate from the application's business logic. There are various common good examples of aspects like logging, auditing, declarative transactions, security, caching, etc.

The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. Dependency Injection helps you decouple your application objects from each other and AOP helps you decouple cross-cutting concerns from the objects that they affect. AOP is like triggers in programming languages such as Perl, .NET, Java, and others.

Spring AOP module provides interceptors to intercept an application. For example, when a method is executed, you can add extra functionality before or after the method execution.

### :star:AOP 용어

1. Aspect

분할(cross-cutting)에 필요한 요소들을 제공하는 API들을 모아놓은 모듈이다. 여러 객체에 공통으로 적용되는 기능을 분리한 것이다. Join point와 Advice를 포함한다. 예를 들어, 로깅 모듈(logging module)은 로깅을 위한 AOP aspect이다. 애플리케이션은 필요에 따라 여러개의 aspect를 가질 수 있다.

2. Join point

애플리케이션에서 aspect를 plug-in할 수 있는 지점을 의미한다. Join point로 정해진 시점에 특정 작업이 시작된다. 메서드 호출지점, 예외 발생시점 등. 스프링 AOP 프레임워크를 사용하는 애플리케이션에서 실제로 기능이 작동하는 위치이다.

3. Advice

메서드가 실행되기 전,후에 작동하는 기능이다. Join point에 삽입될 코드, 메서드이다. 스프링 AOP 프레임워크를 사용하는 애플리케이션이 돌아갈 때 실제 기능의 역할을 수행한다.

4. Pointcut

Advice가 실행되어야 하는 Join point들의 모음이다. 표현식이나 패턴을 통해 Pointcut을 지정할 수 있다.

5. Introduction

존재하고 있는 기존 클래스에 코드를 변경하지 않은 채 새로운 메서드를 추가할 수 있는 정적인 AOP 기술이다.

6. Target object

The object being advised by one or more aspects. This object will always be a proxied object, also referred to as the advised object.

7. Weaving

Aspect와 Target object를 연결하는 작업이다. Weaving을 하고 나면 프록시객체, Advised Object가 만들어진다. Weaving은 컴파일 단계, 로드 단계 혹은 런타임에 이뤄질 수 있다.

#### :mag:Advice
스프링 Aspect는 아래와 같은 다섯가지의 Advice를 활용할 수 있다.

1. before - 메서드 실행 전의 시점에 advice를 수행한다.
2. after - 메서드 실행 후의 시점에 advice를 수행한다. 단, 메서드의 결과에 관계 없이 수행한다.
3. after-returning - 메서드 실행 후의 시점에 advice를 수행한다. 단, 메서드의 결과가 success일 경우에만 수행한다.
4. after-throwing - 메서드 실행 후의 시점에 advice를 수행한다. 단, 메서드가 예외처리를 던지는 경우에만 수행한다.
5. around - 메서드 실행 전, 후의 시점 모두에서 advice를 수행한다. 메서드를 try-catch로 감싸고 proceed 키워드로 실행될 메서드 전후에 기능을 위치시킨다. before, after의 기능을 하나로 합쳐놓았다고 볼 수 있다.

-References :
https://www.tutorialspoint.com/spring/aop_with_spring.htm  