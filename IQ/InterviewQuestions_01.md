# Interview Questions 01
* IQ : 면접 예상 질문과 답변을 기록합니다.

## 면접 질문 01

### 프로그래밍 패러다임

* 명령형 프로그래밍
  * 절차적 프로그래밍
    * 객체를 사용하지 않는 명령형 프로그래밍
    * 프로시저를 사용하여 함수를 통해 코드의 재활용성 높임
    * Basic, C
  * 객체지향 프로그래밍
    * 객체 중심적 사고, 프로그램의 상호작용을 표현
    * 객체에 기반하여 추상화, 캡슐화, 상속성, 다형성 등 특징
    * 객체와 메서드 중심
    * C++, C#, Visual Basic .Net, Java, Python, Ruby, Swift
* 선언형 프로그래밍
  * 논리형 프로그래밍
  * 함수형 프로그래밍
    * 불변
    * 변수와 함수 중심

함수형 프로그래밍은 순수 함수들로 프로그래밍 하며 불변의 데이터, 투명성, ...
상태의 변화를 피하고... 같은 값을 입력받은 함수는 항상 같은 값을 도출해야 한다...
객체지향보다 코드가 간결하고 비절차형이라 평가시점이 중요하지 않다.
테스트가 쉽다(1회 테스트로 신뢰성 보장)

차이점? 함수형 프로그래밍의 데이터는 불변, 객체지향 프로그래밍의의 데이터는 변화할 수 있다.
함수형 프로그래밍의 구문은 아무런 순서로 실행되어도 상관 없으나 객체지향 프로그래밍 구문에는 순서가 있다.
함수형 프로그래밍의 핵심 요소는 변수와 함수이다. 객체지향 프로그래밍의 핵심 요소는 객체와 메서드이다.

함수형 언어같아 보이는 자바스크립트에도 프로토타입이라는 객체가 있고, 객체지향 언어같아 보이는 자바에도 람다식이 있습니다.

### DBMS는 무엇?
데이터베이스를 만들고, 다수의 사용자가 DB의 데이터에 접근, 저장 및 관리할 수 있는 기능들을 제공하는 도구.
기존의 파일 시스템이 갖는 데이터 종속성과 중복성의 문제를 해결하기 위해 제안된 시스템.
중복 제어, 접근 통제, 관계 표현, 제약 조건 등의 기능을 갖고 있다.
오라클 DB, MySQL, Microsoft SQL, PostgreSQL, MongoDB 등이 있고
대부분 DB SQL을 이용하나 MongoDB처럼 일부 NoSQL DB도 있다.

* SQL?
Structured Query Language, 구조화 질의어, DBMS의 데이터 관리를 위해서 설계된 언어이다.
문법은 크게 세가지로 나뉜다. 정의(DDL), 조작(DML), 제어(DCL).
  * DDL - CREAT, DROP, ALTER
  * DML - INSERT, UPDATE, DELETE, SELECT
  * DCL - COMMIT, ROLLBACK, SAVEPOINT

* NoSQL DB 종류
1. Document Store, Document Database
2. Wide Column Store, Wide Column Database
3. Key Value Store, Key Balue Database
4. Graph Database

### Servlet과 JSP의 차이

### JDBC는 무엇?

### 라이브러리와 프레임워크는 무엇?

### Spring은 무엇?

### MyBatis는 무엇?

### Ajax는 무엇?

### HTTP는 무엇?

### Git은 무엇?