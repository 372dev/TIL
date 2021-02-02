# Java_05_Class_01

## :muscle:클래스
모든 자바 프로그램은 객체를 활용한다. 그리고 그 객체들은 클래스와 인터페이스를 통해서 만들어진다. 어느 프로그램이라도 한개의 클래스는 갖게 되며,
복잡한 프로그램이라면 다수의 클래스와 인터페이스들을 포함하고 있을것이다.
그렇게 클래스는 모든 자바 프로그램의 기본 구조적 요소이다. 클래스를 정의하지 않고는 자바 코드를 짤 수 없다고 보아도 된다.

>클래스  

클래스는 값을 가진 데이터 필드와 그 필드를 이용하는 메소드들의 집합이다. 그 필드와 메소드들을 사용하는 새로운 레퍼런스 타입을 정의하며, 그 타입의 새로운 객체가 생성될 수 있는 블루프린트나 프로토타입의 역할을 하는것이 클래스이다.

>객체  

객체는 클래스의 인스턴스이다. 객체지향 프로그래밍의 기본 요소이며 일반적으로 자바 프로그램은 여러개의 객체를 갖는다. 한 프로그램 안의 여러개의 객체들이 메소드를 통해서 상호작용 하게 된다.

### :star:클래스 정의하는 방법
가장 기본적인 형태의 클래스는 class 키워드에 클래스 이름(MyClass)이 따라오는 형태로 작성할 수 있다. 뒤따르는 대괄호 안에 클래스의 요소가 들어가면 된다.

```java
class MyClass {
    // 필드, 생성자, 메소드 선언
}
```

클래스 키워드의 앞에는 접근지정자(public)나 어노테이션(@Override)이 올 수 있다.
클래스명 뒤로는 extends 키워드와 함께 상속할 클래스 이름(MySuperClass)이 따라올 수 있다. 인터페이스를 구현하는 경우에는 맨 마지막에 implements 키워드와 함께 하나 혹은 다수의 인터페이스 이름을 적어주면 되는데, 다수일 경우엔 콤마로 구분한다(YourInterface, MyInterface).

```java
@Override
public class MyClass extends MySuperClass implements YourInterface, MyInterface {
    // 필드, 생성자, 메소드 선언
}
```

#### :mag:필드, 생성자, 메소드
* 필드(field) - 필드는 해당 클래스 객체의 상태 속성을 나타내며, 멤버 변수라고도 불린다. 여기서 초기화하는 것을 필드 초기화 또는 명시적 초기화라고 한다.
  * 인스턴스 변수 - 이름에서 알 수 있듯이 인스턴스가 갖는 변수이다. 그렇기에 인스턴스를 생성할 때 만들어진다. 서로 독립적인 값을 갖으므로 heap 영역에 할당되고 gc에 의해 관리된다.
  * 클래스 변수 - 정적을 의미하는 static키워드가 인스턴스 변수 앞에 붙으면 클래스 변수이다. 해당 클래스에서 파생된 모든 인스턴스는 이 변수를 공유한다. 그렇기 때문에 heap 영역이 아닌 static 영역에 할당되고 gc의 관리를 받지 않는다. 또한 public 키워드까지 앞에 붙이면 전역 변수라 볼 수 있다.
* 생성자(constructor) - 생성자는 객체가 생성된 직후에 클래스의 객체를 초기화하는 데 사용되는 코드 블록이다. 메서드와 달리 리턴 타입이 없으며, 클래스엔 최소 한 개 이상의 생성자가 존재한다.
* 메서드(method) - 메서드는 해당 객체의 행동을 나타내며, 보통 필드의 값을 조정하는데 쓰인다.
  * 인스턴스 메서드 - 인스턴스 변수와 연관된 작업을 하는 메서드이다. 인스턴스를 통해 호출할 수 있으므로 반드시 먼저 인스턴스를 생성해야 한다.
  * 클래스 메서드 - 정적 메서드라고도 한다. 일반적으로 인스턴스와 관계없는 메서드를 클래스 메서드로 정의한다.

#### :mag:접근지정자
![Class_modifiers](https://raw.githubusercontent.com/372dev/TIL/main/JAVA/img/05_Class_01_modifier.jpg)

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://jeeneee.dev/java-live-study/week5-class/  
https://www.geeksforgeeks.org/classes-objects-java/  
https://docs.oracle.com/javase/tutorial/java/javaOO/classdecl.html  