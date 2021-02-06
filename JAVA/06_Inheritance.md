# Java_06_Inheritance

## :muscle:상속
상속은 객체지향 프로그래밍의 가장 중요한 요소중 하나이며, 객체나 클래스를 다른 객체나 클래스에 기반하여 만드는 과정이다.

### :star:자바 상속의 특징
상속은 하나의 객체가 상위 객체의 요소와 특성을 모두 갖게되는 것이다. 자바에서 상속은 이미 존재하는 클래스를 이용하여 새로운 클래스를 만들기 위함인데, 이미 존재하는 클래스를 상속하게 되면 해당 클래스의 메서드와 필드를 가져와서 사용할 수 있다. 나아가 상속을 받은 클래스에 추가적으로 다른 메서드와 필드를 작성할 수 있다.
상속은 IS-A 관계이며 이는 부모-자식 관계로도 불리운다.

상속을 이용하는 근본적 이유
* 메서드 오버라이딩 (런타임 다형성을 위해서).
* 코드의 재사용을 위해서.

상속 용어
* 클래스(Class): 클래스는 공통적인 속성을 지닌 객체들의 집합이다. 객체의 생성을 위한 틀이라고 할수도 설계도면이라고 할수도 있다.
* 하위클래스/자식클래스(Sub Class/Child Class) : 하위클래스는 다른 클래스로부터 상속을 받는다. 파생(derived)클래스, 확장(extended)클래스, 또는 자식클래스 라고도 한다.
* 상위클래스/부모클래스(Super Class/Parent Class) : 하위클래스는 상위클래스로부터 요소들을 상속받는다. (base)클래스, 또는 부모클래스 라고도 한다.
* 재사용성(Reusability) : As the name specifies, reusability is a mechanism which facilitates you to reuse the fields and methods of the existing class when you create a new class. You can use the same fields and methods already defined in the previous class.
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

### :star:메서드 오버라이딩
If subclass (child class) has the same method as declared in the parent class, it is known as method overriding in Java.

In other words, If a subclass provides the specific implementation of the method that has been declared by one of its parent class, it is known as method overriding.

* Usage of Java Method Overriding
  * Method overriding is used to provide the specific implementation of a method which is already provided by its superclass.
  * Method overriding is used for runtime polymorphism.

* Rules for Java Method Overriding
  1. The method must have the same name as in the parent class.
  2. The method must have the same parameter as in the parent class.
  3. There must be an IS-A relationship (inheritance).

### :star:다이나믹 메서드 디스패치 (Dynamic Method Dispatch)

### :star:추상 클래스

#### :mag:인터페이스와 추상클래스
인터페이스는 추상클래스와 비슷하나 추상클래스 보다 추상화 정도가 더 높다. 08_Interface에서 자세히 알아보자.

### :star:final 키워드

### :star:Object 클래스

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/inheritance-in-java  