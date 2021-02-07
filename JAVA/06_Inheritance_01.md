# Java_06_Inheritance_01

## :muscle:상속
상속은 객체지향 프로그래밍의 가장 중요한 요소중 하나이며, 객체나 클래스를 다른 객체나 클래스에 기반하여 만드는 과정이다.

### :star:자바 상속의 특징
상속은 하나의 객체가 상위 객체의 요소와 특성을 모두 갖게되는 것이다. 자바에서 상속은 이미 존재하는 클래스를 이용하여 새로운 클래스를 만들기 위함인데, 이미 존재하는 클래스를 상속하게 되면 해당 클래스의 메서드와 필드를 가져와서 사용할 수 있다. 나아가 상속을 받은 클래스에 추가적으로 다른 메서드와 필드를 작성할 수 있다.
상속은 IS-A 관계이며 이는 부모-자식 관계로도 불리운다.

기본 신텍스는 다음과 같다  
>class 자식클래스명 extends 부모클래스명 { }  

상속을 이용하는 근본적 이유
* 메서드 오버라이딩 (런타임 다형성을 위해서).
* 코드의 재사용을 위해서.

상속 용어
* 클래스(Class): 클래스는 공통적인 속성을 지닌 객체들의 집합이다. 객체의 생성을 위한 틀이라고 할수도 설계도면이라고 할수도 있다.
* 하위클래스/자식클래스(Sub Class/Child Class) : 하위클래스는 다른 클래스로부터 상속을 받는다. 파생(derived)클래스, 확장(extended)클래스 라고도 한다.
* 상위클래스/부모클래스(Super Class/Parent Class) : 하위클래스는 상위클래스로부터 요소들을 상속받는다. 기반(base)클래스 라고도 한다.
* 재사용성(Reusability) : 재사용성이라는 이름에서 알 수 있듯, 하위 클래스에서 상위 클래스의 필드와 메서드를 사용할 수 있다.

#### :mag:클래스의 상속
자바는 C++와 다르게 다중상속을 지원하지 않는다.

#### :mag:인터페이스의 상속
인터페이스는 다른 인터페이스를 상속받을 수 있다. 08_Interface에서 자세히 알아보자.

#### :mag:인터페이스를 상속한 인터페이스를 구현한 클래스
하나 혹은 다수의 인터페이스를 상속받은 인터페이스를 클래스가 구현하게 되면, 클래스는 구현하는 인터페이스의 메서드와 상수를 모두 구현해야 하고, 또한 구현하는 인터페이스의 상위 인터페이스들의 모든 추상메서드와 상수들도 구현해야 한다.
이에 대해서는 08_Interface에서 자세히 알아보자.

### :star:super 키워드
자바의 super 키워드는 부모 클래스의 객체를 의미하는 참조 변수이다. 자식 클래스의 인스턴스를 생성할 때, 부모 클래스의 인스턴스 또한 암묵적으로 생성되며 super 키워드를 통해 접근할 수 있다.

#### :mag:super 키워드의 사용

1. 부모 클래스의 인스턴스 변수를 가리킬 때 사용.
부모 클래스의 필드 혹은 데이터 멤버에 접근하기 위해서 사용할 수 있다. 주로 부모 클래스와 자식 클래스가 같은 필드를 갖고 있는 경우 사용한다.

```java
class 진돗개 {  
	String color = "황구";  
}  

class 강아지 extends 진돗개 {  
	String color = "누렁이";  

	void printColor() {  
		System.out.println(color);
		//강아지 클래스의 "누렁이" 출력
		System.out.println(super.color);
		//진돗개 클래스의 "황구" 출력
	}  
}  

class TestSuper1 {  
	public static void main(String args[]) {  
		강아지 p = new 강아지();  
		p.printColor();  
	}
}  
```

2. 부모 클래스의 메서드를 실행하기 위해 사용.
super 키워드는 또한 부모 클래스의 메서드를 실행하기 위해 사용할 수 있다. 자식 클래스가 부모 클래스와 같은 메서드를 갖고 있을 때 사용한다. 다시 말해, 오버라이드된 메서드가 있을 경우에 사용한다.

```java
class 진돗개 {  
	void eat() {
		System.out.println("쩝쩝...");
	}  
}  

class 강아지 extends 진돗개 {  
	void eat() {
		System.out.println("냠냠...");
	}  

	void bark() {
		System.out.println("멍멍...");
	}  

	void work() {  
		super.eat();  
		//진돗개 클래스의 "쩝쩝..." 출력
		bark();  
		//강아지 클래스의 "멍멍..." 출력
	}  
}  

class TestSuper2 {  
	public static void main(String args[]) {  
		강아지 p = new 강아지();  
		p.work();  
	}
}  
```

3. 부모 클래스의 생성자를 실행하기 위해 super()를 사용.
super 키워드는 또한 부모 클래스의 생성자를 실행하기 위해 사용된다.

```java
class 진돗개 {  
	진돗개() {
		System.out.println("진돗개 생성");
	}  
}  

class 강아지 extends 진돗개 {  
	강아지() {  
		super();  
		//진돗개 클래스의 "진돗개 생성" 출력
		System.out.println("강아지 생성");  
		//강아지 클래스의 "강아지 생성" 출력
	}  
}  

class TestSuper3 {  
	public static void main(String args[]) {  
		강아지 p = new 강아지();  
	}
}  
```

### :star:추상 클래스
자바에서는 abstract 키워드와 함께 클래스가 선언되면 이를 추상 클래스라 한다. 추상 클래스는 추상 메서드를 가질 수 있고 일반 메서드도 가질 수 있다.

일단 추상화가 무엇인지 먼저 알아보자.

#### :mag:추상화
추상화는 사용자로부터 구현 디테일을 감추고 기능성만을 보여주는 것이다.

필수적인 요소만 노출되며 세부적인 사항은 보이지 않게 된다. 예를 들어, 친구에게 문자를 보낸다고 했을 때, 문자를 작성하고 보내는 기능은 눈에 보이지만 입력된 값이 어떻게 저장되어서 전송되는지의 과정은 사용자에게 보이지 않는다.

추상화를 통해 사용자는 객체의 작동원리 대신 기능에 집중할 수 있다.

* 자바에서 추상화를 이루기 위해서, 비슷하지만 다르게 두가지 방법이 있다.
  1. 추상 클래스 (0 ~ 100% 추상화)
  2. 인터페이스 (100% 추상화)

#### :mag:인터페이스와 추상 클래스
이렇듯 인터페이스는 추상클래스와 비슷하나 추상클래스 보다 추상화 정도가 더 높다. 08_Interface에서 자세히 알아보자.

#### :mag:추상 클래스
abstract 키워드와 함께 클래스가 선언되면 이를 추상 클래스라 한다. 추상 클래스는 추상 메서드를 가질 수 있고 일반 메서드도 가질 수 있다. 추상 클래스는 상속되고 나서야 사용될 수 있고, 그 자체만으로는 인스턴스화 될 수 없다.

>abstract class A {}  

* 자바 추상 클래스의 규칙
  1. 추상 클래스는 abstract 키워드로 선언된다.
  2. 추상 메서드와 일반 메서드를 가질 수 있다.
  3. 추상 클래스만으로는 인스턴스화 될 수 없다.
  4. 생성자를 가질 수 있고 static 메서드도 가질 수 있다.
  5. final 메서드를 가질 수 있고, 이 경우엔 자식 클래스에서 해당 메서드의 내용을 변경할 수 없다.

#### :mag:추상 메서드
abstract 키워드와 함께 선언되며 내용이 작성되지 않은 메서드를 추상 메서드라고 한다.

```java
abstract class 자전거 {  
	abstract void run();
	void park() {
		System.out.println("주차했습니다");
	}
}  

class 삼천리 extends 자전거 {  
	void run() {
		System.out.println("속도 3000 m/h");
	}
}

class Test {
	public static void main(String args[]){  
		자전거 bike = new 삼천리();
		bike.run(); // "속도 3000 m/h"
		bike.park(); // "주차했습니다"
		}  
}  
```

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/inheritance-in-java  
https://www.javatpoint.com/super-keyword   
https://www.javatpoint.com/abstract-class-in-java